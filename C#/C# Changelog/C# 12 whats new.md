[What's new in C# 12 - C# Guide | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12)

# What's new in C# 12

-   Article
-   04/10/2023

## In this article

1.  [Primary constructors](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12#primary-constructors)
2.  [Default lambda parameters](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12#default-lambda-parameters)
3.  [Alias any type](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12#alias-any-type)
4.  [See also](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12#see-also)

Some C# 12 features have been introduced in previews. The You can try these features using the latest [Visual Studio preview](https://visualstudio.microsoft.com/vs/preview/) or the latest [.NET 8 preview SDK](https://dotnet.microsoft.com/download/dotnet).

-   [Primary constructors](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12#primary-constructors) - Introduced in Visual Studio 17.6 preview 2.
-   [Optional parameters in lambda expressions](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12#default-lambda-parameters) - Introduced in Visual Studio 17.5 preview 2.
-   [Alias any type](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12#alias-any-type) - Introduced in Visual Studio 17.6 preview 3.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12#primary-constructors)

## Primary constructors

You can now create primary constructors in any `class` and `struct`. Primary constructors are no longer restricted to `record` types. Primary constructor parameters are in scope for the entire body of the class. To ensure that all primary constructor parameters are definitely assigned, all explicitly declared constructors must call the primary constructor using `this()` syntax. Adding a primary constructor to a `class` prevents the compiler from declaring an implicit parameterless constructor. In a `struct`, The implicit parameterless constructor initializes all fields, including primary constructor parameters to the 0-bit pattern.

The compiler generates public properties for primary constructor parameters only in `record` types, either `record class` or `record struct` types. Non-record classes and structs may not always want this behavior for primary constructor parameters.

You can learn more about primary constructors in the article on [instance constructors](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/instance-constructors#primary-constructors).

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12#default-lambda-parameters)

## Default lambda parameters

You can now define default values for parameters on lambda expressions. The syntax and rules are the same as adding default values for arguments to any method or local function.

You can learn more about default parameters on lambda expressions in the article on [lambda expressions](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions#input-parameters-of-a-lambda-expression).

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-12#alias-any-type)

## Alias any type

You can use the `using` alias directive to alias any type, not just named types. That means you can create semantic aliases for tuple types, array types, pointer types, or other unsafe types. For more information, see the [feature specification](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/using-alias-types)