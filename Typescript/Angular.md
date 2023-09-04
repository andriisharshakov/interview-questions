## Advantages and disadvantages of Angular framework

Pros:
- first-class Typescript support
- powerful CLI
- DI
- all-in solution (routing, animations, forms, ...)

Cons:
- complexity (Typescript, RxJS knowledge)
- bundle size
- community size

## Change detection

By default:
- javascript event: click, mouseEnter, mouseMove, ...
- AJAX call performed
- setInterval or setTimeout tick

NgOnPushStrategy:
- input value has changed
- template event fired
- manually triggered change detection, see:
```typescript
import { Component, Input, ChangeDetectorRef } from '@angular/core';

@Component({
  selector: 'app-custom-component',
  template: `
    <div>
      <p>{{ data }}</p>
      <button (click)="updateData()">Update Data</button>
    </div>
  `,
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class CustomComponent {
  @Input() data: string;

  constructor(private cdr: ChangeDetectorRef) {}

  updateData() {
    // Update the data and trigger change detection manually
    this.data = 'Updated Data';
    this.cdr.markForCheck();
  }
}
```


By utilizing **NgZone**, you can manage asynchronous operations more effectively and ensure that your application's view is updated correctly in response to changes caused by these operations. NgZone provides two primary functions:

- *Zone Management*: Zones are execution contexts that track asynchronous operations. NgZone is responsible for managing these zones and understanding when tasks within a zone are completed.

- *Change Detection Triggers*: When an asynchronous task is executed, NgZone can automatically trigger Angular's change detection mechanism. This ensures that the view is updated to reflect any changes caused by the asynchronous operation.

## Optimization techniques

- using ngZone, runOutsideAngular() heavy scripts and third-party libs
```typescript
import { Component, NgZone } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <button (click)="startAsyncTask()">Start Async Task</button>
    <p>{{ message }}</p>
  `
})
export class AppComponent {
  message = 'Initial Message';

  constructor(private ngZone: NgZone) {}

  startAsyncTask() {
    this.message = 'Task started...';

    // Running the asynchronous task within the NgZone: the runOutsideAngular() method is used to ensure that the task is executed outside Angular's change detection zone...
    this.ngZone.runOutsideAngular(() => {
      setTimeout(() => {
        // ... and the run() method is used to bring the execution back inside Angular's zone once the task is complete. This way, Angular knows to trigger change detection when the asynchronous task finishes.
        this.ngZone.run(() => {
          this.message = 'Async Task Completed';
        });
      }, 2000);
    });
  }
}
```

- detach view from change detection
```typescript
import { Component, ChangeDetectorRef } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `...`
})
export class AppComponent {
  constructor(private cdr: ChangeDetectorRef) {}

  detachView() {
    this.cdr.detach(); // Detach view from change detection
  }

  reattachView() {
    this.cdr.reattach(); // Reattach view to change detection
  }
}
```

- lazy-load components via dynamic imports
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `...`
})
export class AppComponent {
  async loadLazyComponent() {
    const lazyModule = await import('./lazy/lazy.module');
    const lazyComponentFactory = lazyModule.lazyComponentFactory;

    // Dynamically load and render the lazy component
    this.vcRef.createComponent(lazyComponentFactory);
  }
}
```

- avoid too many `*ngIf`s and `*ngSwitch`es in templates and use dynamic components
```typescript
import { Component, ComponentFactoryResolver, ViewContainerRef } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `...`
})
export class AppComponent {
  constructor(
    private cfr: ComponentFactoryResolver,
    private vcRef: ViewContainerRef
  ) {}

  loadDynamicComponent(componentType: Type<any>) {
    const componentFactory = this.cfr.resolveComponentFactory(componentType);
    this.vcRef.createComponent(componentFactory);
  }
}
```

- virtual scroll for large lists
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `...`
})
export class AppComponent {
  items = [...]; // Large list of items

  trackByFn(index: number, item: any) {
    return item.id; // Provide a unique identifier for tracking
  }
}
```

- server-side pagination
```typescript
import { Component } from '@angular/core';
import { DataService } from './data.service';

@Component({
  selector: 'app-root',
  template: `...`
})
export class AppComponent {
  currentPage = 1;

  constructor(private dataService: DataService) {}

  loadPage(pageNumber: number) {
    this.currentPage = pageNumber;
    this.dataService.getDataForPage(pageNumber).subscribe(data => {
      // Update UI with data
    });
  }
}
```

- caching and memoization
```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  private cachedData: any;

  getData() {
    if (this.cachedData) {
      return of(this.cachedData);
    } else {
      return this.http.get('...');
    }
  }
}
```

- service workers (for features like offline caching, background synchronization, and more)
```typescript
// app.module.ts
import { NgModule } from '@angular/core';
import { ServiceWorkerModule } from '@angular/service-worker';
import { environment } from '../environments/environment';

@NgModule({
  imports: [
    // ...
    ServiceWorkerModule.register('ngsw-worker.js', { enabled: environment.production })
  ],
  // ...
})
export class AppModule { }
```

## DI and how it works

Dependency Injection is an application design pattern (in Angular it has itsown implementation). When a class is declaring some external dependencies, there's two types of injectors:
- module injector
- component injector

When a component has a dependency injected, Angular will traverse the tree of component's parents, looking for a resolution of that dependency. If a root has been reached, next place to look is the module.

The *resolution modifiers* allow you to fine-tune the dependency resolution process and control how Angular searches for and injects dependencies. Here's a breakdown of how they work:
- If you only want to use the dependency provided by the current component's injector, use `@Self()`. It prevents Angular from traversing up the component tree and looking in parent components or the module injector.
- If the dependency is optional, and you want to gracefully handle the absence of the dependency, use `@Optional()`. It tells Angular not to throw an error if the dependency cannot be resolved. If the dependency is found, it's injected; if not, `null` is injected instead.
- If you want to skip the current component's injector and search in parent components or the module injector, use `@SkipSelf()`.
- If you're dealing with directives and want to search for the dependency in the host element's component injector, use `@Host()`.

These decorators are especially useful when working with complex component trees, where different components might provide similar dependencies at various levels. They help ensure that the correct dependency is resolved based on your specific requirements.

## What is RxJS

This is a library which implements the concept of *reactive programming*. It's heavily used in Angular apps.

## Observable vs Promise

- Observables are lazy
- Observables are cancelable
- Observables can be sync and async (Promises are always async)
- Observables can emit multiple values
- Observable has different operators to transform the data (Promises only have `.then()`, `catch()` and `finally()` methods and few more)

## Memory leaks (and how to prevent them)

- kill the subscriptions upon destroying a particular component
- async pipe cares about unsubscription for us

## Bundle optimizations

- **AOT compilation**. Unlike JIT (Just-in-Time) compilation, where the compiler is included in the bundle, AOT compilation eliminates the need for the compiler in the final bundle. This reduces the bundle size and improves loading times, making your application more efficient. The AOT-compiled code is also more predictable and less error-prone, as many issues are caught during the compilation process itself.
- **Lazy Loading** is a powerful technique that allows you to load parts of your application only when they are needed. This can significantly improve the initial load time of your application, as it loads only the essential components initially and defers loading the rest until they are required.
- **Differentiated Loading** takes this further by loading different versions of a module or component based on the user's device or network conditions. This helps provide an optimal experience for users across various devices and network speeds.
- `providedIn` for Services. Angular's providedIn metadata option for services allows you to define where a service should be provided. This can be `'root'` for a singleton service at the application level, or `'any'` for a new instance of the service for each component. Properly utilizing providedIn helps manage the lifecycle and scope of your services effectively, optimizing memory usage and preventing unnecessary service instances.

## Tree shaking

Tree shaking is a technique used in modern JavaScript build processes, including those for Angular applications, to eliminate unused code from the final bundle. The term "tree shaking" comes from the idea of "shaking out" the dead or unused branches of the code tree, similar to how a tree might shed its dead leaves.

In the context of an Angular application, tree shaking involves identifying and removing parts of the code that are not actually used or referenced. This includes functions, classes, modules, and variables that are imported but never used in the application. Removing this dead code has several benefits:

1. **Reduced Bundle Size:** Removing unused code reduces the size of the JavaScript bundle that needs to be downloaded by the user's browser. This leads to faster loading times and improved performance.

2. **Optimized Performance:** With a smaller bundle size, the browser spends less time parsing and executing JavaScript, resulting in faster page rendering and improved user experience.

3. **Less Maintenance Overhead:** By removing unused code, the codebase becomes cleaner and easier to maintain. Developers can focus on the relevant code without being distracted by unnecessary artifacts.

Tree shaking is possible due to the static nature of modern JavaScript module systems like ES6 modules. These modules provide information about the dependencies between modules at build time, which makes it possible for the build tools to identify and eliminate code that is not actually used.

In Angular applications, tree shaking is an essential part of the build process when using the production build mode. By default, when you build your Angular application for production using the Angular CLI, the build tool (such as Webpack) automatically performs tree shaking. However, it's important to ensure that your code adheres to practices that make tree shaking effective, such as not importing unnecessary parts of libraries or modules.

## Runtime performance optimizations

- **NgOnPushStrategy**. The NgOnPush change detection strategy is a powerful way to optimize your component's performance. It reduces the number of change detection cycles by checking for changes only in inputs or explicit events. This can lead to significant performance improvements, as Angular won't perform unnecessary checks on components that haven't been impacted by changes.
- **trackByFn**. When working with lists or collections using Angular's *ngFor directive, using the trackByFn function can greatly enhance rendering performance. The trackByFn allows Angular to keep track of each item's identity, minimizing unnecessary DOM updates and enhancing overall list rendering efficiency.
trackByFn for Lists
- **Avoid Function Calls Inside Templates**. To improve template rendering performance, it's advisable to avoid heavy function calls directly within templates. Instead, use **pure pipes** to transform and format data. Pure pipes are optimized for change detection, and Angular will only re-evaluate them when their input values change, helping reduce the load on change detection.
- **Content Delivery Networks (CDNs)**. Leveraging CDNs for serving static assets, such as Angular libraries and third-party dependencies, can speed up the loading of your application. CDNs offer distributed delivery networks that serve content from servers closer to the user's location, reducing latency and improving page load times.

## How are you staying up-to-date with Angular ecosystem?

- https://blog.angular.io/
- https://indepth.dev/