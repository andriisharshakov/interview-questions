# Fundamental questions

___

**Q: .NET Framework vs .NET Core  vs .NET 5.0**

*.NET Framework 4.x*:
- only for Windows
- slow compared to .NET Core
- packaged as one bulky framework
- rather IDE based

*.NET Core*:
- cross platform
- better performance
- delivered modularly using Nuget
- full CLI command supported

*.NET 5.0+* is a unified platform which unifies all .NET runtime like .NET Framework, .NET Core, Mono and other.

___

**Q: What is IL Code? What's the use of JIT compiler?**

IL Code is a partially compiled code. JIT compiles IL code to machine language. This allows to optimize the code depending on the runtime environment.

___

**Q: What is CRL?**

Common Language Runtime is the runtime execution environment for .NET.
- it invokes JIT to compile to IL code
- it cleans any unused objects by using GC

Code that executes under CLR execution environment is called as *managed code*. *Unmanaged code* executes outside CRL boundary.

___

**Q: What is Garbage Collector?**

GC is a background process which keeps running continuously and cleans any kind of *unused managed resources*.

___

**Q: What is CTS?**

Common Types System ensures that data types defined in two different languages get compiled to a common data type.

___

**Q: What is CLS?**

Common Language Specification is a specification, i.e. a set of rules or guidelines. While any .NET programming language adheres to these set of rules it can be consumed by any other language following .NET specifications.

___

**Q: What is casting?**

```C#
    int i = 99;
    // implicit casting, from lower to higher data type, no data loss
    double d1 = i;

    double d2 = 100.01;
    // explicit casting, from higher to lower data type, data loss expected
    int j = (int) d2;
```

___

**Q: Array vs ArrayList?**

```C#
    // Array is fixed length and strongly typed:
    int[] array = { 1, 2, 3 };
    
    // ArrayList is flexible length and NOT strongly typed (though, boxing/unboxing impacts the performance):
    ArrayList list = new ArrayList();
    list.Add(1);
    list.Add(2);
    list.Add("III");
```

___

**Q: Generic collections**

```C#
    // they combine pros of Array and ArrayList, being strongly typed but flexible length, and they perform better then ArrayList:
    List<int> list = new List<int>();
    list.Add(1);
    list.Add(2);
    list.Add(3);
```

___

**Q: Thread**

```C#
using System.Threading;
    ...
    Thread a = new Thread(MethodA);
    a.Start();
    Thread b = new Thread(MethodB);
    b.Start();
```

___

**Q: Thread vs Task**

Task is introduced in TPL, it allows us to abstract from Process, ProcessorAffinity etc, and rely on TPL when running parallel code. *Three "P"* provided by TPL:
- Parallel Processing
- Pooling Threads
- Plus! (return, result, cancel, chain, async/await)

```C#
using System.Threading.Tasks;
    ...
    Task a = new Task(MethodA);
    a.Start();
    Task b = new Task(MethodB);
    b.Start();
```

___

**Q: What's the need of Delegates?**

Delegate is a pointer to a function. Delegates are useful as callbacks to communicate between threads.

___

**Q: What are Events?**

These are encapsulation over Delegates. Events change Delegates to a publisher/subscriber model.

```C#
using System;

// Define an event handler delegate
public delegate void TemperatureChangeHandler(object sender, TemperatureChangedEventArgs e);

// Define event arguments
public class TemperatureChangedEventArgs : EventArgs
{
    public double NewTemperature { get; set; }
}

// Publisher class with an event
public class Thermostat
{
    // Declare the event
    public event TemperatureChangeHandler TemperatureChanged;

    private double currentTemperature;

    public double CurrentTemperature
    {
        get { return currentTemperature; }
        set
        {
            if (value != currentTemperature)
            {
                currentTemperature = value;
                OnTemperatureChanged(new TemperatureChangedEventArgs { NewTemperature = value });
            }
        }
    }

    protected virtual void OnTemperatureChanged(TemperatureChangedEventArgs e)
    {
        // Raise the event
        TemperatureChanged?.Invoke(this, e);
    }
}

// Subscriber class
public class HomeOwner
{
    public HomeOwner(Thermostat thermostat)
    {
        thermostat.TemperatureChanged += Thermostat_TemperatureChanged;
    }

    private void Thermostat_TemperatureChanged(object sender, TemperatureChangedEventArgs e)
    {
        Console.WriteLine($"HomeOwner: Temperature changed to {e.NewTemperature}°C");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Thermostat thermostat = new Thermostat();
        HomeOwner homeOwner = new HomeOwner(thermostat);

        // Simulate temperature change
        thermostat.CurrentTemperature = 22.5;

        // Output:
        // HomeOwner: Temperature changed to 22.5°C
    }
}
```

___

**Q: What's the difference between Abstract class and Interface?**

*Interface* is a **contract to be implemented**, whilst *Abstract class* is a half-defined **parent class to be inherited** forcing certain aspects to be followed by child classes.

___

** Q: What are the class types in C#?**

- **Abstract classes** are meant to be inherited and can contain a mix of abstract and non-abstract members.
- **Partial classes** allow a class to be split across multiple files for collaborative development.
- **Sealed classes** prevent further inheritance of the class.
- **Static classes** cannot be instantiated and contain only static members.

Let's explore each type:

1. **Abstract Class:**
   - An abstract class is a class that cannot be instantiated on its own. It is meant to be used as a base class for other classes.
   - It may contain abstract methods, which are declared without implementation and must be implemented by any non-abstract derived class.
   - Abstract classes can also have non-abstract methods with implementations.
   - Example:

     ```csharp
     public abstract class Shape
     {
         public abstract double Area();  // Abstract method
         public void Display() { Console.WriteLine("Displaying shape"); } // Regular method
     }
     ```

2. **Partial Class:**
   - A partial class allows a class, interface, or struct to be defined in multiple files. The compiler combines all the partial class definitions into a single class during compilation.
   - It is often used in large projects where multiple developers can work on different parts of a class without interfering with each other.
   - Example:

     ```csharp
     // File 1
     partial class Person
     {
         public string FirstName { get; set; }
     }

     // File 2
     partial class Person
     {
         public string LastName { get; set; }
     }
     ```

3. **Sealed Class:**
   - A sealed class is a class that cannot be inherited. It is marked with the `sealed` keyword.
   - Sealing a class prevents other classes from deriving from it. It is often used when you want to prevent further modification or extension of a class.
   - Example:

     ```csharp
     sealed class FinalClass
     {
         // Class members
     }
     ```

4. **Static Class:**
   - A static class is a class that cannot be instantiated, and it can only contain static members (methods, properties, fields).
   - Static classes are often used for utility classes or classes that provide a set of related functionalities that do not depend on instance state.
   - All members of a static class must be static, and you access them using the class name rather than creating an instance.
   - Example:

     ```csharp
     public static class MathUtility
     {
         public static double Add(double x, double y)
         {
             return x + y;
         }
     }
     ```