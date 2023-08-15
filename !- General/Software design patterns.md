# Software design patterns

**Q: What software design patterns do you know?**

## Creational

- Abstract factory

Instead of manually instantiating an object, it's retrieved from an abstraction (factory). This allows for complex and replaceable instantiation logic that is separate from the consuming code.

- Factory method

Instead of manually instantiating an object, it's created using a supplied function (method), passed by the calling code.

- Builder

Instead of manually instantiating an object, its construction is delegated to another type (builder) which allows for deferred instantiation of an object. This is useful with immutable types that have a large set of parameters, most of which are optional, or when an instance of an immutable type is partially constructed by different methods.

- Object pool

Instead of manually instantiating an object, an instance is requested from an object pool, which may return a previously instantiated object suitable for reuse. This is used in performance-critical paths where additional memory allocation is undesired. Objects in the pool have a lifecycle: Creation - Validation - Destroy.

- Prototype (aka Clone)

Instead of manually instantiating an object, a previously instantiated and configured instance of an object is copied.

- Singleton

Instead of manually instantiating an object, a single instance is reused across different parts of the program:
 - Make the default constructor private, to prevent other objects from using the new operator with the Singleton class.
 - Create a static creation method that acts as a constructor. Under the hood, this method calls the private constructor to create an object and saves it in a static field. All following calls to this method return the cached object.

## Structural

- Adapter

Abstraction is implemented by wrapping an existing type to match the contract defined by the target interface.

- Bridge

Bridge is a structural design pattern that lets you split a large class or a set of closely related classes into two separate hierarchies—abstraction and implementation—which can be developed independently of each other.

- Composite

Composite is a structural design pattern that lets you compose objects into tree structures and then work with these structures as if they were individual objects.

- Decorator (aka Wrapper)

Abstraction is implemented by combining multiple types into a hierarchy of responsibilities. A wrapper (= a decorator) is an object that can be linked with some target object. The wrapper contains the same set of methods as the target and delegates to it all requests it receives. However, the wrapper may alter the result by doing something either before or after it passes the request to the target.

- Facade

Abstraction is implemented by subclassing it to a higher-level abstraction with fewer dependencies. In other words, Facade provides a simplified interface to a library, a framework, or any other complex set of classes.

- Flyweight

Flyweight is a structural design pattern that lets you fit more objects into the available amount of RAM by sharing common parts of state (= intrinsic state, constant data of an object) between multiple objects instead of keeping all of the data in each object.

- Private class data

Private class data pattern prevents manipulation of data that is meant to be immutable by separating the data from the methods that use it into a class that maintains the data state. Use it when you want to prevent write access to class data members.

- Proxy

Proxy is a structural design pattern that lets you provide a substitute or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request gets through to the original object.

- Chain of responsibility

Behavior of a system is dynamically implemented by a chained sequence of handlers.

- Command

Behavior of a system is separated from the parameters associated with the request.

- Interpreter

Behavior of a system is based on a hierarchy of domain objects that represents a query formulated as a string of text.

- Iterator

Common abstraction for types that implement enumeration of elements. This allows traversing elements in a container without knowing the implementation of the container.

- Mediator

Communication between services through intermediary that allows publishing and subscribing to messages. This lets services communicate with each other without explicitly referring to one another and, as a result, not depending on one another.

- Memento

???

- Null object

Stub implementation of an abstraction that doesn't do anything. This is typically used in places where a dependency is optional, in order to avoid conditional logic that handles cases where it's not set.

- Observer

???

- State

Behavior of an object is dependent on its internal state.

- Strategy

Set of interchangeable algorithms.

- Template method

Public non-virtual method which is implemented by calling other (usually private) virtual or abstract methods on the same type. This can be used to let clients extend or override object's behavior by changing a subset of its workflow.

- Visitor

Behavior associated with data objects is extracted to a different type (visitor).
