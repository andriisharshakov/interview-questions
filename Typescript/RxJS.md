There are various operators and factory functions available in RxJS that allow you to create, transform, and combine observables in different ways. Some of the commonly used observables and operators include:

### Creation Operators:

`of`: Creates an observable that emits a sequence of values.
`from`: Converts an array, promise, or iterable into an observable.
`interval`: Emits sequential numbers at a specified time interval.
`timer`: Emits values in a sequence after a specified delay.

### Transformation Operators:

`map`: Transforms emitted values using a mapping function.
`filter`: Filters emitted values based on a condition.
`mergeMap` (`flatMap`): Flattens observables by merging multiple inner observables.

### Combination Operators:

`combineLatest`: Combines multiple observables and emits when any of them emit.
`merge`: Merges multiple observables into a single stream.
`forkJoin`: Waits for multiple observables to complete and emits their last values.

### Conditional Operators:

`take`: Emits a specified number of values from the beginning of an observable.
`skip`: Skips a specified number of values from the beginning of an observable.

### Error Handling Operators:

`catchError`: Catches errors emitted by an observable and continues with a fallback.

---

## Now, let's illustrate some common RxJS operators with examples:

### of

```javascript
import { of } from 'rxjs';

const source = of(1, 2, 3, 4, 5);
source.subscribe(value => {
  console.log(value);
});

// Output:
// 1
// 2
// 3
// 4
// 5
```

### from

```javascript
import { from } from 'rxjs';

const arraySource = from([1, 2, 3, 4, 5]);
arraySource.subscribe(value => {
  console.log(value);
});

// Output:
// 1
// 2
// 3
// 4
// 5
```

### interval

```javascript
import { interval } from 'rxjs';

const intervalSource = interval(1000); // Emits every 1 second
intervalSource.subscribe(value => {
  console.log(value);
});

// Output:
// 0 (after 1 second)
// 1 (after 2 seconds)
// 2 (after 3 seconds)
// ...
```

### timer

```javascript
import { timer } from 'rxjs';

const timerSource = timer(2000, 1000); // Initial delay: 2 seconds, Interval: 1 second
timerSource.subscribe(value => {
  console.log(value);
});

// Output:
// 0 (after 2 seconds)
// 1 (after 3 seconds)
// 2 (after 4 seconds)
// ...
```

### map

```javascript
import { of } from 'rxjs';
import { map } from 'rxjs/operators';

const source = of(1, 2, 3);

const mapped = source.pipe(
  map(value => value * 2)
);

mapped.subscribe(result => {
  console.log(result);
});

// Output:
// 2
// 4
// 6
```

### filter

```javascript
import { of } from 'rxjs';
import { filter } from 'rxjs/operators';

const source = of(1, 2, 3, 4, 5);

const filtered = source.pipe(
  filter(value => value % 2 === 0)
);

filtered.subscribe(result => {
  console.log(result);
});

// Output:
// 2
// 4
```

### mergeMap (aka flatMap)

```javascript
import { of } from 'rxjs';
import { mergeMap } from 'rxjs/operators';

const source = of(1, 2, 3);
source.pipe(
  mergeMap(value => of(value * 2))
).subscribe(result => {
  console.log(result);
});

// Output:
// 2
// 4
// 6
```

### combineLatest

```javascript
import { combineLatest, of } from 'rxjs';

const source1 = of('A', 'B', 'C');
const source2 = of(1, 2, 3);

combineLatest(source1, source2).subscribe(combined => {
  console.log(combined);
});

// Output:
// ['C', 1]
// ['C', 2]
// ['C', 3]
```

### merge

```javascript
import { merge, interval } from 'rxjs';

const source1 = interval(1000);
const source2 = interval(500);

merge(source1, source2).subscribe(value => {
  console.log(value);
});

// Output:
// 0 (from source2, after 500ms)
// 0 (from source1, after 1000ms)
// 1 (from source2, after 1000ms)
// 2 (from source2, after 1500ms)
// 1 (from source1, after 2000ms)
// ...
```

### forkJoin

```javascript
import { forkJoin, of } from 'rxjs';

const source1 = of(1);
const source2 = of(2);

forkJoin(source1, source2).subscribe(results => {
  console.log(results);
});

// Output:
// [1, 2]
```

### take

```javascript
import { interval } from 'rxjs';
import { take } from 'rxjs/operators';

const source = interval(1000);
source.pipe(
  take(3) // Emit only the first 3 values
).subscribe(value => {
  console.log(value);
});

// Output:
// 0
// 1
// 2
```

### skip

```javascript
import { interval } from 'rxjs';
import { skip } from 'rxjs/operators';

const source = interval(1000);
source.pipe(
  skip(3) // Skip the first 3 values
).subscribe(value => {
  console.log(value);
});

// Output:
// 3 (after 3 seconds)
// 4 (after 4 seconds)
// 5 (after 5 seconds)
// ...
```

### catchError

```javascript
import { of } from 'rxjs';
import { catchError } from 'rxjs/operators';

const source = of(1, 2, 'three', 4);

source.pipe(
  catchError(error => of('Error occurred'))
).subscribe(result => {
  console.log(result);
});

// Output:
// 1
// 2
// Error occurred
// 4
```