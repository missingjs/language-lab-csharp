# C# Learning Roadmap: From Beginner to Advanced Practitioner

This document summarizes a structured learning path for someone who is new to C# and wants to grow into an advanced C#/.NET practitioner. The recommended approach is to combine conceptual learning with progressively more difficult small projects.

For the project sequence itself, see [projects/README.md](projects/README.md).

---

## 1. Core Philosophy

C# is not just a traditional object-oriented language. Modern C# combines several layers:

1. The C# language itself
2. Object-oriented design and composition
3. Modern language features such as records, pattern matching, and nullable reference types
4. LINQ and functional-style data transformation
5. Asynchronous and concurrent programming with `Task`, `async`, and `await`
6. The .NET runtime, standard library, CLI, NuGet, and project system
7. Application frameworks such as ASP.NET Core, EF Core, Worker Services, Unity, Blazor, and desktop UI frameworks
8. Engineering practices such as testing, logging, configuration, diagnostics, performance analysis, and deployment

The key transition from intermediate to advanced C# usage happens when you stop thinking only in terms of classes and inheritance, and start thinking in terms of clear type models, explicit nullability, async boundaries, resource ownership, composition, testability, and runtime behavior.

---

## 2. Stage One: Master the C# Language Basics

### 2.1 Basic Syntax and Expressions

You should become comfortable with:

- Variables and constants
- Expressions and statements
- `if`, `switch`, `for`, `foreach`, and `while`
- Methods
- Namespaces
- `using` directives
- String interpolation
- Top-level statements
- Basic project structure

Example:

```csharp
var name = "Alice";
var age = 30;

if (age >= 18)
{
    Console.WriteLine($"{name} is an adult.");
}
```

Remember that `var` is not dynamic typing. It is compile-time type inference.

### 2.2 Value Types and Reference Types

You should understand the difference between:

- Value types
- Reference types
- `struct`
- `class`
- Copy semantics
- Reference sharing
- Boxing and unboxing
- `null`

Example:

```csharp
int x = 1;
int y = x;
y = 2;
// x is still 1
```

But:

```csharp
var a = new User { Name = "Alice" };
var b = a;
b.Name = "Bob";
// a.Name is now "Bob"
```

This distinction affects API design, memory behavior, performance, and concurrency safety.

### 2.3 Nullable Reference Types

Modern C# code should usually enable nullable reference types:

```xml
<Nullable>enable</Nullable>
```

You should understand:

- Non-nullable reference types
- Nullable reference types
- `string` vs `string?`
- Nullability warnings
- Null-forgiving operator `!`
- `ArgumentNullException.ThrowIfNull`
- Designing APIs that make nullability explicit

Example:

```csharp
string name = "Alice";
string? maybeName = null;
```

The goal is to make possible absence visible in the type signature.

### 2.4 Collections

You should learn the common collection types and interfaces:

- `Array`
- `List<T>`
- `Dictionary<TKey, TValue>`
- `HashSet<T>`
- `Queue<T>`
- `Stack<T>`
- `IEnumerable<T>`
- `IReadOnlyList<T>`
- `IReadOnlyDictionary<TKey, TValue>`

You should also understand when to expose concrete collections and when to expose interfaces.

Example:

```csharp
IEnumerable<User> users = GetUsers();
List<User> list = users.ToList();
```

Advanced C# code often uses collection interfaces to express capability boundaries.

---

## 3. Stage Two: Object-Oriented Design and Modern Data Modeling

### 3.1 Classes, Properties, and Constructors

You should become comfortable with:

- `class`
- Fields
- Properties
- Methods
- Constructors
- Access modifiers
- `static`
- `readonly`
- `const`
- `sealed`

Example:

```csharp
public sealed class User
{
    public User(string email)
    {
        Email = email;
    }

    public string Email { get; }
}
```

Properties are a core C# feature and should not be treated as simple public fields.

### 3.2 Interfaces and Composition

Interfaces are central to C# design.

Important topics:

- Interface definition
- Interface implementation
- Dependency inversion
- Composition over inheritance
- Explicit interface implementation
- Default interface methods
- Constructor injection

Example:

```csharp
public interface IUserRepository
{
    Task<User?> FindByIdAsync(UserId id, CancellationToken cancellationToken);
}
```

Mature C# code usually favors composition and small interfaces over deep inheritance trees.

### 3.3 Records and Immutable Data

Records are useful for modeling data with value-based equality.

Topics to study:

- `record class`
- `record struct`
- Positional records
- `init` properties
- `with` expressions
- Value-based equality
- DTOs, commands, events, and value objects

Example:

```csharp
public sealed record UserDto(string Id, string Email);
```

And:

```csharp
var updated = user with { Email = "new@example.com" };
```

Records are especially useful for data transfer objects, domain events, commands, query results, and immutable value objects.

### 3.4 Pattern Matching

Modern C# has powerful pattern matching features.

You should learn:

- `is` patterns
- `switch` expressions
- Type patterns
- Property patterns
- Relational patterns
- Logical patterns
- List patterns
- Null patterns
- Discard patterns

Example:

```csharp
return payment switch
{
    { Status: PaymentStatus.Pending } => "Waiting",
    { Status: PaymentStatus.Paid } => "Completed",
    { Status: PaymentStatus.Failed, Error: var error } => $"Failed: {error}",
    _ => "Unknown"
};
```

Pattern matching helps C# move beyond traditional object-oriented branching into clearer data-driven control flow.

---

## 4. Stage Three: LINQ and Functional-Style Programming

### 4.1 Delegates, Lambdas, and Closures

Important concepts:

- `delegate`
- `Func<T>`
- `Action<T>`
- `Predicate<T>`
- Lambda expressions
- Method groups
- Closures

Example:

```csharp
Func<int, int> square = x => x * x;
```

Delegates and lambdas are used throughout LINQ, event handling, asynchronous code, tests, and framework APIs.

### 4.2 LINQ

LINQ is one of the most important parts of idiomatic C#.

You should master:

- `Where`
- `Select`
- `SelectMany`
- `OrderBy`
- `GroupBy`
- `Any`
- `All`
- `FirstOrDefault`
- `SingleOrDefault`
- `Aggregate`
- `ToList`
- `ToDictionary`

Example:

```csharp
var emails = users
    .Where(user => user.IsActive)
    .Select(user => user.Email)
    .ToList();
```

More important than memorizing methods is understanding:

- Deferred execution
- Repeated enumeration
- Projection
- Filtering
- Aggregation
- Query syntax vs method syntax
- `IEnumerable<T>` vs `IQueryable<T>`

### 4.3 Immutability and Data Transformation

C# is not a purely functional language, but modern C# increasingly benefits from immutable data design.

Topics to study:

- `readonly`
- `init`
- Records
- `with` expressions
- `IReadOnlyList<T>`
- `System.Collections.Immutable`
- Pure functions where appropriate

The goal is not to eliminate mutation everywhere, but to use immutability where it improves correctness, testability, and concurrency safety.

---

## 5. Stage Four: Errors, Results, and Resource Management

### 5.1 Exceptions

C# primarily uses exceptions for error handling.

You should understand:

- `try`
- `catch`
- `finally`
- `throw`
- Custom exception types
- Exception filters
- Inner exceptions
- Stack traces

Example:

```csharp
try
{
    await service.DoWorkAsync();
}
catch (TimeoutException ex)
{
    logger.LogWarning(ex, "Operation timed out.");
}
```

Advanced code distinguishes between truly exceptional failures, expected domain failures, validation failures, and infrastructure boundary failures.

### 5.2 Result Pattern

Although C# commonly uses exceptions, Result-style modeling is useful for expected business failures.

Example:

```csharp
public abstract record Result<T>;

public sealed record Success<T>(T Value) : Result<T>;

public sealed record Failure<T>(string Error) : Result<T>;
```

Useful cases include:

- Validation
- Domain errors
- Workflow steps
- Expected failures
- Application service boundaries

The goal is not to replace all exceptions, but to avoid using exceptions for normal business control flow.

### 5.3 Resource Management

Resource management is essential in C#.

You should learn:

- `IDisposable`
- `using` statement
- `using` declaration
- `IAsyncDisposable`
- `await using`
- File, database, network, stream, timer, and lock resources

Example:

```csharp
using var stream = File.OpenRead(path);
```

Async resource example:

```csharp
await using var connection = await OpenConnectionAsync();
```

Correct resource management is a major marker of mature .NET code.

---

## 6. Stage Five: Generics and Type Design

### 6.1 Generics

Generics are central to C# library and application design.

Topics to learn:

- Generic methods
- Generic classes
- Generic interfaces
- Generic constraints
- `where T : class`
- `where T : struct`
- `where T : notnull`
- `where T : new()`

Example:

```csharp
public interface IRepository<T>
{
    Task<T?> FindAsync(Guid id, CancellationToken cancellationToken);
}
```

### 6.2 Variance

You should understand:

- Covariance with `out T`
- Contravariance with `in T`
- Invariance

Example:

```csharp
public interface IProducer<out T>
{
    T Produce();
}

public interface IConsumer<in T>
{
    void Consume(T value);
}
```

Variance matters when designing interfaces, event systems, abstractions, and reusable libraries.

### 6.3 Domain Modeling

C# can be very effective for domain modeling.

Important topics:

- Value objects
- Entities
- Aggregates
- Domain events
- Commands
- Queries
- DTOs
- Strongly typed IDs

Example:

```csharp
public readonly record struct UserId(Guid Value);
public readonly record struct Email(string Value);
```

This helps avoid primitive obsession, where too many unrelated domain concepts are represented as raw `string`, `int`, or `Guid` values.

---

## 7. Stage Six: Asynchronous and Concurrent Programming

### 7.1 Task and async/await

C# asynchronous programming is built around `Task`, `Task<T>`, `async`, and `await`.

Example:

```csharp
public async Task<User?> FindUserAsync(UserId id, CancellationToken cancellationToken)
{
    return await repository.FindByIdAsync(id, cancellationToken);
}
```

Topics to study:

- `Task`
- `Task<T>`
- `async`
- `await`
- `ConfigureAwait`
- `Task.WhenAll`
- `Task.WhenAny`
- `ValueTask`
- Async streams

You should understand that `async` does not necessarily create a new thread, and `await` does not block the current thread in the usual synchronous sense.

### 7.2 CancellationToken

Mature C# code passes cancellation through layers.

Topics:

- `CancellationToken`
- `CancellationTokenSource`
- Timeouts
- Cooperative cancellation
- Propagating cancellation through APIs

Example:

```csharp
public Task<User?> FindAsync(UserId id, CancellationToken cancellationToken)
```

Ignoring cancellation is one of the most common mistakes in service code.

### 7.3 Concurrency and Parallelism

Important tools and concepts:

- `Thread`
- ThreadPool
- `Task.Run`
- `Parallel.ForEach`
- `ConcurrentDictionary`
- `Channel<T>`
- `lock`
- `Monitor`
- `SemaphoreSlim`
- `ReaderWriterLockSlim`

A useful rule of thumb:

```text
IO-bound work: async/await
CPU-bound work: Task.Run, Parallel, ThreadPool
Producer-consumer workflows: Channel<T>
Shared mutable state: lock or concurrent collections
```

---

## 8. Stage Seven: .NET Engineering Practices

### 8.1 .NET SDK and CLI

You should become comfortable with:

```bash
dotnet new
dotnet build
dotnet run
dotnet test
dotnet add package
dotnet publish
```

You should also be able to read and edit `.csproj` files.

### 8.2 NuGet and Project Structure

Topics to understand:

- NuGet packages
- `PackageReference`
- Versioning
- Transitive dependencies
- Lock files
- Private packages
- Central package management
- Solution files
- Project references

### 8.3 Configuration, Logging, and Dependency Injection

Modern .NET applications commonly use the `Microsoft.Extensions.*` ecosystem.

Study:

- `Microsoft.Extensions.Configuration`
- `appsettings.json`
- Environment variables
- Options pattern
- `Microsoft.Extensions.Logging`
- Structured logging
- Serilog
- Dependency injection
- Service lifetimes: singleton, scoped, transient
- `IServiceCollection`
- `IServiceProvider`

Dependency injection is not magic. It is a disciplined way to manage object creation and dependencies.

### 8.4 Testing

Common testing frameworks include:

- xUnit
- NUnit
- MSTest

Useful supporting tools:

- FluentAssertions
- Moq
- NSubstitute
- FakeItEasy
- Testcontainers

Topics to practice:

- Unit tests
- Integration tests
- Parameterized tests
- Fakes, stubs, and mocks
- Test data builders
- Testing async code
- Testing cancellation and timeouts

---

## 9. Stage Eight: Application Ecosystem

### 9.1 ASP.NET Core

ASP.NET Core is the main web framework for modern C# applications.

Key topics:

- Routing
- Middleware
- Controllers
- Minimal APIs
- Model binding
- Validation
- Authentication
- Authorization
- Filters
- Dependency injection
- Configuration
- Logging
- OpenAPI

The goal is not just to build CRUD endpoints, but to understand the request pipeline and application architecture.

### 9.2 Entity Framework Core and Data Access

EF Core is widely used for database access.

Study:

- `DbContext`
- `DbSet`
- Migrations
- Change tracking
- No-tracking queries
- Relationships
- LINQ-to-SQL translation
- Transactions
- N+1 queries
- Raw SQL
- Connection resilience

EF Core is powerful, but it does not remove the need to understand SQL, indexes, transactions, and database performance.

### 9.3 Worker Services and Background Jobs

Useful topics:

- `IHostedService`
- `BackgroundService`
- `Channel<T>`
- Timers
- Graceful shutdown
- Retries
- Resilience
- Queue consumers

Worker services are an important part of production .NET systems.

### 9.4 Other Directions

After the core language and .NET foundations are solid, choose directions according to your goals:

- WPF, WinForms, or Avalonia for desktop applications
- Unity for games
- MAUI for cross-platform applications
- Blazor for web UI
- Azure SDKs for cloud services
- Orleans for virtual actor systems

Do not try to learn all C# ecosystems at once.

---

## 10. Stage Nine: Runtime, Diagnostics, and Performance

### 10.1 CLR and Garbage Collection

Important topics:

- CLR
- JIT compilation
- Managed memory
- Garbage collection
- Generations
- Large Object Heap
- Allocation
- Boxing
- `Span<T>`
- `Memory<T>`

You do not need to start here, but advanced C# developers should understand runtime costs.

### 10.2 Profiling and Diagnostics

Useful tools and topics:

- BenchmarkDotNet
- `dotnet-counters`
- `dotnet-trace`
- `dotnet-dump`
- Visual Studio Profiler
- PerfView
- OpenTelemetry
- Structured logs and metrics

You should learn how to diagnose slow code, excessive allocations, thread pool starvation, memory leaks, and production failures.

### 10.3 High-Performance C#

Advanced topics:

- `Span<T>`
- `ReadOnlySpan<T>`
- `Memory<T>`
- `ArrayPool<T>`
- `ValueTask`
- `ref struct`
- `readonly struct`
- Source generators
- Native AOT

These are powerful tools, but they should be learned after the fundamentals are solid.

---

## 11. Recommended Conceptual Learning Order

A good conceptual sequence is:

```text
1. Basic syntax and type system
2. Value types vs reference types
3. Nullable reference types
4. Classes, properties, and constructors
5. Interfaces and composition
6. Collections and IEnumerable<T>
7. Delegates and lambdas
8. LINQ and deferred execution
9. Records and immutable data modeling
10. Pattern matching and switch expressions
11. Exceptions and resource management
12. Generics and variance
13. Domain modeling with value objects
14. async/await and Task
15. CancellationToken
16. Concurrency primitives and Channel<T>
17. .NET CLI, NuGet, and csproj
18. Testing with xUnit, NUnit, or MSTest
19. Configuration, logging, and dependency injection
20. ASP.NET Core or another application direction
21. EF Core or data access
22. Worker services and background tasks
23. CLR, GC, profiling, and BenchmarkDotNet
24. High-performance C# features
```

---

## Final Advice

Do not learn C# only as old-style object-oriented programming, and do not start by trying to learn every .NET framework at once. A better path is:

```text
Small language projects
→ Collection and LINQ projects
→ Domain modeling projects
→ Async and cancellation projects
→ .NET engineering projects
→ ASP.NET Core and EF Core
→ Background services
→ Diagnostics and performance
```

The turning point comes when you can design clear type boundaries, handle nullability deliberately, write reliable async code with cancellation, manage resources correctly, and diagnose runtime behavior. Once you combine modern C# language features with solid .NET engineering practices, you are moving from ordinary C# usage into advanced C#/.NET system design.
