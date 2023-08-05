# SOLID

___

**Q: What do you know about SOLID?**

SOLID is an acronym for 5 design principles in OOP.

- **S** - Single responsibility principle

A class should have only one responsibility and only one reason to change. A class should have a clear and well-defined purpose.

- **O** - Open-closed principle

Software entities should be open for extension (meaning that their behavior can be changed by adding new code) but closed for modification (which would mean changing existing code).

- **L** - Liskov substitution principle

Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program. In other words, subclasses should honor the contract of their superclasses snd not violate the expectations.

- **I** - Interface segregation principle

No client should be forced to depend on methods it does not use. This means that we should avoid creating large and monolithic interfaces that contain many methods, and instead split them into smaller and more cohesive ones that are specific to each client's needs.

- **D** - Dependency inversion principle

One should depend upon abstractions, not concretions.

_Hint: if you're worried you will forget the names, you can always ask the interviewer to name the principles so that you can explain what they mean. This has worked for me a bunch of times._

___

**Q: Where is the "inversion" in dependency inversion?**

_Credit: [Craig Walls](https://www.javaworld.com/article/2071914/excellent-explanation-of-dependency-injection--inversion-of-control-.html)_

Any nontrivial application is made up of two or more classes that collaborate with each other to perform some business logic. Traditionally, each object is responsible for obtaining its own references to the objects it collaborates with (its dependencies). When applying DI, the objects are given their dependencies at creation time by some external entity that coordinates each object in the system. In other words, dependencies are injected into objects.

The reason it's called "inversion" is because the normal control sequence would be the object finds the objects it depends on by itself and then calls them. Here, this is reversed: The dependencies are handed to the object when it's created.
