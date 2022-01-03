# Dependency Injection in .NET

**Created**: Wednesday, October 19, 2016 11:34:48 AM -04:00
**Modified**: Monday, January 03, 2022 10:30:21 AM -05:00

# Training Plan

1. https://app.pluralsight.com/library/courses/dependency-injection-on-ramp/table-of-contents
2. ~~http://rob.conery.io/2012/04/01/inversion-of-control-an-architects-version-of-global-variables/~~ (Article no longer exists)
3. [Inversion of Control (tutorialsteacher.com)](https://www.tutorialsteacher.com/ioc/inversion-of-control)

# Mark&#39;s Recommended Links

[12/7/16 11:01 AM] Mark Harris:

[The future of Unity - .NET Blog (microsoft.com)](https://devblogs.microsoft.com/dotnet/the-future-of-unity/)

https://weblogs.asp.net/cibrax/the-future-of-unity 

https://github.com/unitycontainer/unity 
1. From this website: Due to a complete lack of interest from the community to support this project, it has been archived and will no longer be maintained. There will be no more releases of this library.

given that, I'd probably pull the repo and build it myself

[12/7/16 11:03 AM] Mark Harris:

or better yet

find someone / ask if you can add it to https://dotnetfoundation.org/ 

i checked but didn't see it there yet

seems like a good place for it though

[12/7/16 11:04 AM] Mark Harris:

prism is there

maybe email the NuGet package owners and ask them? see if they'd consider adding it to the foundation?

# Medium Article

[Decouple Your Code With Dependency Injection](https://medium.com/better-programming/decouple-your-code-with-dependency-injection-d893ae9edcf8) (from Medium)

There are different ways how we can provide an instance with its necessary dependencies:

1. Constructor injection
2. Property injection
3. Method injection

## Constructor Injection

Constructor, or initializer-based dependency injection, means providing all required dependencies during the initialization of an instance, as constructor arguments.

```c#
public class DataProcessor {

    private final DbManager manager;
    private final Calculator calculator;

    public DataProcessor(DbManager manager, Calculator calculator) {
        this.manager = manager;
        this.calculator = calculator;
    }

    // ...
}
```

Thanks to this simple change, we can offset most of the initial disadvantages:

1. Easily replaceable: `DbManager` and `Calculator` are no longer bound to the concrete implementations, and are now mockable for unit-testing.
2. Already initialized and “ready-to-go”: We don’t need to worry about any sub-dependencies required by our dependencies (e.g., database filename, significant digits), or that they might crash during initialization.
3. Mandatory requirements: The caller knows exactly what’s needed to create a `DataProcessor`.
4. Immutability: Dependencies are still final.

Even though **constructor injection is the preferred way** of many DI frameworks, it has its obvious disadvantages, too.

1. <mark style="background: #FFF3A3A6;">The most significant one is that <strong>all dependencies must be provided at initialization</strong>.</mark>

Sometimes, we don’t initialize a component ourselves or we aren’t able to provide all dependencies at that point. Or we need to use another constructor.

1. <mark style="background: #FFF3A3A6;">And once the dependencies are set, they can’t be changed.</mark>

But we can mitigate these problems by using one of the other injection types.

## Property Injection

1. Sometimes we don’t have access to the actual initialization of type, and only have an already initialized instance.
2. Or the needed dependency is not explicitly known at initialization as it would be later on.

In these cases, instead of relying on a constructor, we can use *property injection*:

```c#
public class DataProcessor {

    public DbManager manager = null;
    public Calculator calculator = null;

    // ...

    public void processData() {
        // WARNING: Possible NPE (Null Pointer Exception)
        this.manager.processData();
    }

    public BigDecimal calc(BigDecimal input) {
        // WARNING: Possible NPE (Null Pointer Exception)
        return this.calculator.expensiveCalculation(input);
    }
}

```

No constructor is needed anymore, we can provide the dependencies at any time after initialization.

<mark style="background: #FFF3A3A6;">But this way of injection also comes with drawbacks: <strong>Mutability</strong>.</mark>

Our `DataProcessor` is **no longer guaranteed to be “ready-to-go” after initialization**. Being able to change the dependencies at will might give us more flexibility, but also **the disadvantage of more runtime-checks**.

We now have to deal with the possibility of a **`NullPointerException`** when accessing the dependencies.

## Method Injection

Even though we decoupled the dependencies with constructor injection and/or property injection, by doing so, **we still only have a single choice**. What if we need **another Calculator** in some situations?

**We don’t want to add additional properties or constructor arguments for a second `Calculator`**, because there might be a third one needed in the future. And changing the property every time before we call `calc(...)` isn't feasible either, and will most likely lead to bugs using the wrong one.

A better way is to parameterize the method call itself with its dependency:

```c#
public class DataProcessor {

    // ...

    public BigDecimal calc(Calculator calculator, BigDecimal input) {
        return calculator.expensiveCalculation(input);
    }
}
```


Now the caller of `calc(...)` is responsible for providing an appropriate `Calculator` instance, and `DataProcessor` is completely decoupled from it.

## Mixed Injection

Even more flexibility can be gained by **mixing different types of injection**, and providing a default Calculator:

```c#
public class DataProcessor {

    // ...

    private final Calculator defaultCalculator;

    public DataProcessor(Calculator calculator) {
        this.defaultCalculator = calculator;
    }
    
    // ...
    
    public BigDecimal calc(Calculator calculator, BigDecimal input) {
    
        return Optional.ofNullable(calculator)
                       .orElse(this.calculator)
                       .expensiveCalculation(input);
    }
}

```

The caller *could* provide a different kind of Calculator, but it doesn’t *have* to. We still have a decoupled, ready-to-go `DataProcessor`, with the ability to adapt to specific scenarios.
