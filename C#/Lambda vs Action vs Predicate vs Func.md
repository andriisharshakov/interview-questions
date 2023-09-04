# Lambda vs Action vs Predicate vs Func

## Lambda Expression

Purpose: Used to create anonymous functions.
Signature: Can be of various forms.

```C#
Func<int, int> square = x => x * x;
int result = square(5); // result = 25
```

## Action

Purpose: Represents a method that takes parameters but doesn't return a value.
Signature: `Action<T>` where `T` is the input parameter type.

```C#
Action<string> printMessage = message => Console.WriteLine(message);
printMessage("Hello, World!");
```

## Predicate

Purpose: Represents a method that takes a parameter and returns a Boolean value, often used for filtering.
Signature: `Predicate<T>` where `T` is the input parameter type.

```C#
Predicate<int> isEven = number => number % 2 == 0;
bool result = isEven(6); // result = true
```

## Func

Purpose: Represents a method that takes parameters and returns a value of a specified type.
Signature: `Func<T, TResult>` where `T` is the input parameter type, and TResult is the return type.

```C#
Func<string, string, string> concatenate = (s1, s2) => s1 + s2;
string result = concatenate("Hello, ", "World!"); // result = "Hello, World!"
```
