# Project-Based Learning Path

This is a project-driven learning path for C#. The goal is to master the language itself first, then gradually move into .NET engineering, asynchronous programming, web APIs, data access, background services, and diagnostics.

The project sequence is designed to avoid jumping too early into large ASP.NET Core or Unity applications. Each project should focus on one to three core learning modules.

For the conceptual map behind these projects, see [../roadmap.md](../roadmap.md).

---

## The Fifteen Projects

1. [CLI TODO Tool](01-cli-todo/README.md) — Basic syntax, classes, JSON serialization, file IO, `dotnet` workflow.
2. [Log Analyzer](02-log-analyzer/README.md) — File streaming, LINQ, records, pattern matching, regex.
3. [LINQ Data Query Playground](03-linq-playground/README.md) — Method/query syntax, deferred execution, `IEnumerable<T>`.
4. [Strongly Typed Domain Model](04-domain-model/README.md) — Records, value objects, strongly typed IDs, immutable updates.
5. [Result and Validation Library](05-result-validation/README.md) — Generics, expected failure vs exception, fluent API.
6. [File Backup CLI](06-file-backup-cli/README.md) — File/directory APIs, streams, `IDisposable`, `using`.
7. [Async URL Checker](07-async-url-checker/README.md) — `HttpClient`, `Task.WhenAll`, `SemaphoreSlim`, `CancellationToken`.
8. [Typed Event Bus](08-event-bus/README.md) — Interfaces, generics, variance, async handlers.
9. [Minimal Web API](09-minimal-web-api/README.md) — ASP.NET Core, routing, DI, validation, integration tests.
10. [Database-backed Bookmark API](10-bookmark-db-api/README.md) — EF Core, migrations, transactions, async DB APIs.
11. [Background Job Queue](11-job-queue/README.md) — `Channel<T>`, `BackgroundService`, retry, graceful shutdown.
12. [Configuration and Options Demo](12-config-options/README.md) — `IConfiguration`, options pattern, validation.
13. [Worker Service](13-worker-service/README.md) — `IHostedService`, `BackgroundService`, hosting model.
14. [Diagnostics and Observability Lab](14-diagnostics-lab/README.md) — Structured logs, metrics, OpenTelemetry, `dotnet-trace`.
15. [Performance Optimization Lab](15-performance-lab/README.md) — BenchmarkDotNet, allocation analysis, profiling.

---

## Recommended Project Order

```text
1. CLI TODO Tool
2. Log Analyzer
3. LINQ Data Query Playground
4. Strongly Typed Domain Model
5. Result and Validation Library
6. File Backup CLI
7. Async URL Checker
8. Typed Event Bus
9. Minimal Web API
10. Database-backed Bookmark API
11. Background Job Queue
12. Configuration and Options Demo
13. Worker Service
14. Diagnostics and Observability Lab
15. Performance Optimization Lab
```

Learning progression:

```text
C# syntax and objects
→ Collections and LINQ
→ Records, pattern matching, and domain modeling
→ Error handling and Result pattern
→ Resource management and file IO
→ async/await and cancellation
→ Web APIs and dependency injection
→ EF Core and data access
→ Background services and channels
→ Logging, metrics, diagnostics, and performance
```

---

## Recommended Minimal Set

If time is limited, prioritize these projects:

```text
1. Log Analyzer
2. Strongly Typed Domain Model
3. Result and Validation Library
4. Async URL Checker
5. Minimal Web API
6. Database-backed Bookmark API
7. Background Job Queue
8. Performance Optimization Lab
```

These cover the most important C#/.NET skills:

```text
LINQ
records
pattern matching
nullable reference types
error modeling
async/await
CancellationToken
ASP.NET Core
EF Core
Channel<T>
testing
performance measurement
```

---

## Three-Pass Approach for Each Project

### Version 1: Make It Work

Focus on:

- Correct behavior
- Simple structure
- Clear names
- Basic tests

Do not over-engineer abstractions too early.

### Version 2: Make It Idiomatic C#

Refactor toward:

- Nullable reference types
- Records where appropriate
- Pattern matching
- LINQ
- Clear interfaces
- Proper exception or Result usage
- `CancellationToken` in async APIs

### Version 3: Make It Production-Aware

Add:

- Logging
- Configuration
- Dependency injection
- Testing improvements
- Graceful shutdown
- Metrics or diagnostics
- Performance measurements

---

## Questions to Ask During Projects

For every project, ask:

```text
Are nullability annotations accurate?
Should this be a class, record, record struct, or enum?
Is this expected failure or an exceptional failure?
Should this API accept a CancellationToken?
Is this LINQ query deferred or already materialized?
Will this collection be enumerated multiple times?
Is this resource disposed correctly?
Is shared state protected?
Is this interface useful, or just unnecessary abstraction?
Can the core logic be tested without the framework?
Can I diagnose this if it fails in production?
```

---

## Advanced C# Practitioner Goals

After completing this project sequence, you should be able to write C# code that is:

```text
clear in its type modeling
explicit about nullability
well-structured around interfaces and composition
comfortable with LINQ and data transformation
reliable with async/await and cancellation
careful with resource management
testable
ready for ASP.NET Core and EF Core
observable and diagnosable
measured before being optimized
```

The goal is not merely to know C# syntax, but to become comfortable building maintainable .NET systems.
