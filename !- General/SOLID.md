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

**Q: Identify which SOLID principle is violated in Example 1 and explain why.**
```python   
class Customer:
    def place_order(self, order):
        # Logic to place an order

    def send_confirmation_email(self, order):
        # Logic to send an email
```

The Single Responsibility Principle states that a class should have only one reason to change. In Example 1, the Customer class violates SRP by handling both placing an order and sending a confirmation email. To adhere to SRP, these responsibilities should be separated into different classes.

**Q: In Example 2, how does the code violate the Open/Closed Principle, and how could it be improved?**
```java
class PaymentProcessor {
    public void processPayment(Order order) {
        if (order.paymentMethod == PaymentMethod.CREDIT_CARD) {
            // Process credit card payment
        } else if (order.paymentMethod == PaymentMethod.PAYPAL) {
            // Process PayPal payment
        }
    }
}
```

The Open/Closed Principle states that software entities (classes, modules, functions) should be open for extension but closed for modification. In Example 2, the PaymentProcessor violates OCP by directly checking the payment method type and adding more code for each new payment method. A better approach would be to use polymorphism and create separate payment processor classes for each payment method, extending a common interface.

**Q: Discuss the Liskov Substitution Principle violation in Example 3 and propose a solution to adhere to the principle.**
```c#
class Bird {
    public virtual void Fly() {
        // Logic for flying
    }
}

class Ostrich : Bird {
    public override void Fly() {
        throw new NotImplementedException("Ostrich cannot fly");
    }
}
```

The Liskov Substitution Principle states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. In Example 3, the Ostrich class violates LSP by throwing an exception for the Fly method. To adhere to LSP, the Ostrich class should either implement a different behavior for flying or not include the Fly method.

**Q: Explain how the code in Example 4 fails to follow the Interface Segregation Principle, and suggest a better design.**
```python
class Worker:
    def work(self):
        pass

    def eat(self):
        pass
```

The Interface Segregation Principle states that a class should not be forced to implement interfaces it does not use. In Example 4, the Worker class violates ISP by forcing implementations of both the work and eat methods. To adhere to ISP, the Worker class should be split into smaller, more focused interfaces based on specific behaviors.

**Q: In Example 5, what issue with the Dependency Inversion Principle is present, and how can it be rectified?**
```java
class LightBulb {
    public void turnOn() {
        // Turn on the light bulb
    }
}

class Switch {
    private LightBulb bulb;

    public Switch() {
        bulb = new LightBulb();
    }

    public void operate() {
        bulb.turnOn();
    }
}
```

The Dependency Inversion Principle states that high-level modules should not depend on low-level modules; both should depend on abstractions. In Example 5, the Switch class violates DIP by directly creating an instance of LightBulb. To adhere to DIP, the Switch class should depend on an abstraction (interface or abstract class) for the light bulb and receive the actual instance through constructor injection.

___

**Q: Where is the "inversion" in dependency inversion?**

_Credit: [Craig Walls](https://www.javaworld.com/article/2071914/excellent-explanation-of-dependency-injection--inversion-of-control-.html)_

Any nontrivial application is made up of two or more classes that collaborate with each other to perform some business logic. Traditionally, each object is responsible for obtaining its own references to the objects it collaborates with (its dependencies). When applying DI, the objects are given their dependencies at creation time by some external entity that coordinates each object in the system. In other words, dependencies are injected into objects.

The reason it's called "inversion" is because the normal control sequence would be the object finds the objects it depends on by itself and then calls them. Here, this is reversed: The dependencies are handed to the object when it's created.
