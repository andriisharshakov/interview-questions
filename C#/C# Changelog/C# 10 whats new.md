[What's new in C# 10 - C# Guide | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10)

# What's new in C# 10

-   Article
-   02/21/2023

## In this article

1.  [Record structs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#record-structs)
2.  [Improvements of structure types](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#improvements-of-structure-types)
3.  [Interpolated string handler](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#interpolated-string-handler)
4.  [Global using directives](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#global-using-directives)
5.  [File-scoped namespace declaration](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#file-scoped-namespace-declaration)
6.  [Extended property patterns](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#extended-property-patterns)
7.  [Lambda expression improvements](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#lambda-expression-improvements)
8.  [Constant interpolated strings](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#constant-interpolated-strings)
9.  [Record types can seal ToString](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#record-types-can-seal-tostring)
10.  [Assignment and declaration in same deconstruction](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#assignment-and-declaration-in-same-deconstruction)
11.  [Improved definite assignment](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#improved-definite-assignment)
12.  [Allow AsyncMethodBuilder attribute on methods](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#allow-asyncmethodbuilder-attribute-on-methods)
13.  [CallerArgumentExpression attribute diagnostics](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#callerargumentexpression-attribute-diagnostics)
14.  [Enhanced #line pragma](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#enhanced-line-pragma)

C# 10 adds the following features and enhancements to the C# language:

-   [Record structs](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#record-structs)
-   [Improvements of structure types](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#improvements-of-structure-types)
-   [Interpolated string handlers](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#interpolated-string-handler)
-   [`global using` directives](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#global-using-directives)
-   [File-scoped namespace declaration](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#file-scoped-namespace-declaration)
-   [Extended property patterns](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#extended-property-patterns)
-   [Improvements on lambda expressions](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#lambda-expression-improvements)
-   [Allow `const` interpolated strings](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#constant-interpolated-strings)
-   [Record types can seal `ToString()`](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#record-types-can-seal-tostring)
-   [Improved definite assignment](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#improved-definite-assignment)
-   [Allow both assignment and declaration in the same deconstruction](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#assignment-and-declaration-in-same-deconstruction)
-   [Allow `AsyncMethodBuilder` attribute on methods](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#allow-asyncmethodbuilder-attribute-on-methods)
-   [CallerArgumentExpression attribute](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#callerargumentexpression-attribute-diagnostics)
-   [Enhanced `#line` pragma](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#enhanced-line-pragma)
-   [Warning wave 6](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/compiler-messages/warning-waves#cs8826---partial-method-declarations-have-signature-differences)

C# 10 is supported on **.NET 6**. For more information, see [C# language versioning](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/configure-language-version).

You can download the latest .NET 6 SDK from the [.NET downloads page](https://dotnet.microsoft.com/download). You can also download [Visual Studio 2022](https://visualstudio.microsoft.com/vs/), which includes the .NET 6 SDK.

Note

We're interested in your feedback on these features. If you find issues with any of these new features, create a [new issue](https://github.com/dotnet/roslyn/issues/new/choose) in the [dotnet/roslyn](https://github.com/dotnet/roslyn) repository.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#record-structs)

## Record structs

You can declare value type records using the [`record struct` or `readonly record struct` declarations](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record). You can now clarify that a `record` is a reference type with the `record class` declaration.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#improvements-of-structure-types)

## Improvements of structure types

C# 10 introduces the following improvements related to structure types:

-   You can declare an instance parameterless constructor in a structure type and initialize an instance field or property at its declaration. For more information, see the [Struct initialization and default values](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct#struct-initialization-and-default-values) section of the [Structure types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct) article.
-   A left-hand operand of the [`with` expression](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/with-expression) can be of any structure type or an anonymous (reference) type.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#interpolated-string-handler)

## Interpolated string handler

You can create a type that builds the resulting string from an [interpolated string expression](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated#compilation-of-interpolated-strings). The .NET libraries use this feature in many APIs. You can build one by [following this tutorial](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/tutorials/interpolated-string-handler).

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#global-using-directives)

## Global using directives

You can add the `global` modifier to any [using directive](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-directive) to instruct the compiler that the directive applies to all source files in the compilation. This is typically all source files in a project.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#file-scoped-namespace-declaration)

## File-scoped namespace declaration

You can use a new form of the [`namespace` declaration](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/namespace) to declare that all declarations that follow are members of the declared namespace:

C#

    namespace MyNamespace;
    

This new syntax saves both horizontal and vertical space for `namespace` declarations.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#extended-property-patterns)

## Extended property patterns

Beginning with C# 10, you can reference nested properties or fields within a property pattern. For example, a pattern of the form

C#

    { Prop1.Prop2: pattern }
    

is valid in C# 10 and later and equivalent to

C#

    { Prop1: { Prop2: pattern } }
    

valid in C# 8.0 and later.

For more information, see the [Extended property patterns](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-10.0/extended-property-patterns) feature proposal note. For more information about a property pattern, see the [Property pattern](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/patterns#property-pattern) section of the [Patterns](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/patterns) article.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#lambda-expression-improvements)

## Lambda expression improvements

C# 10 includes many improvements to how lambda expressions are handled:

-   Lambda expressions may have a [natural type](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions#natural-type-of-a-lambda-expression), where the compiler can infer a delegate type from the lambda expression or method group.
-   Lambda expressions may declare a [return type](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions#explicit-return-type) when the compiler can't infer it.
-   [Attributes](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions#attributes) can be applied to lambda expressions.

These features make lambda expressions more similar to methods and local functions. They make it easier to use lambda expressions without declaring a variable of a delegate type, and they work more seamlessly with the new ASP.NET Core Minimal APIs.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#constant-interpolated-strings)

## Constant interpolated strings

In C# 10, `const` strings may be initialized using [string interpolation](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated) if all the placeholders are themselves constant strings. String interpolation can create more readable constant strings as you build constant strings used in your application. The placeholder expressions can't be numeric constants because those constants are converted to strings at run time. The current culture may affect their string representation. Learn more in the language reference on [`const` expressions](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/const).

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#record-types-can-seal-tostring)

## Record types can seal ToString

In C# 10, you can add the `sealed` modifier when you override `ToString` in a record type. Sealing the `ToString` method prevents the compiler from synthesizing a `ToString` method for any derived record types. A `sealed` `ToString` ensures all derived record types use the `ToString` method defined in a common base record type. You can learn more about this feature in the article on [records](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/record).

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#assignment-and-declaration-in-same-deconstruction)

## Assignment and declaration in same deconstruction

This change removes a restriction from earlier versions of C#. Previously, a deconstruction could assign all values to existing variables, or initialize newly declared variables:

C#

    // Initialization:
    (int x, int y) = point;
    
    // assignment:
    int x1 = 0;
    int y1 = 0;
    (x1, y1) = point;
    

C# 10 removes this restriction:

C#

    int x = 0;
    (x, int y) = point;
    

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#improved-definite-assignment)

## Improved definite assignment

Prior to C# 10, there were many scenarios where definite assignment and null-state analysis produced warnings that were false positives. These generally involved comparisons to boolean constants, accessing a variable only in the `true` or `false` statements in an `if` statement, and null coalescing expressions. These examples generated warnings in previous versions of C#, but don't in C# 10:

C#

    string representation = "N/A";
    if ((c != null && c.GetDependentValue(out object obj)) == true)
    {
       representation = obj.ToString(); // undesired error
    }
    
    // Or, using ?.
    if (c?.GetDependentValue(out object obj) == true)
    {
       representation = obj.ToString(); // undesired error
    }
    
    // Or, using ??
    if (c?.GetDependentValue(out object obj) ?? false)
    {
       representation = obj.ToString(); // undesired error
    }
    

The main impact of this improvement is that the warnings for definite assignment and null-state analysis are more accurate.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#allow-asyncmethodbuilder-attribute-on-methods)

## Allow AsyncMethodBuilder attribute on methods

In C# 10 and later, you can specify a different async method builder for a single method, in addition to specifying the method builder type for all methods that return a given task-like type. A custom async method builder enables advanced performance tuning scenarios where a given method may benefit from a custom builder.

To learn more, see the section on [`AsyncMethodBuilder`](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/attributes/general#asyncmethodbuilder-attribute) in the article on attributes read by the compiler.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#callerargumentexpression-attribute-diagnostics)

## CallerArgumentExpression attribute diagnostics

You can use the [System.Runtime.CompilerServices.CallerArgumentExpressionAttribute](https://learn.microsoft.com/en-us/dotnet/api/system.runtime.compilerservices.callerargumentexpressionattribute) to specify a parameter that the compiler replaces with the text representation of another argument. This feature enables libraries to create more specific diagnostics. The following code tests a condition. If the condition is false, the exception message contains the text representation of the argument passed to `condition`:

C#

    public static void Validate(bool condition, [CallerArgumentExpression("condition")] string? message=null)
    {
        if (!condition)
        {
            throw new InvalidOperationException($"Argument failed validation: <{message}>");
        }
    }
    

You can learn more about this feature in the article on [Caller information attributes](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/attributes/caller-information#argument-expressions) in the language reference section.

[](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-10#enhanced-line-pragma)

## Enhanced #line pragma

C# 10 supports a new format for the `#line` pragma. You likely won't use the new format, but you'll see its effects. The enhancements enable more fine-grained output in domain-specific languages (DSLs) like Razor. The Razor engine uses these enhancements to improve the debugging experience. You'll find debuggers can highlight your Razor source more accurately. To learn more about the new syntax, see the article on [Preprocessor directives](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/preprocessor-directives#error-and-warning-information) in the language reference. You can also read the [feature specification](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-10.0/enhanced-line-directives#examples) for Razor based examples.