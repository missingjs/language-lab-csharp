[← Back to projects](../README.md)

# Project 7: Async URL Checker

Build a CLI tool that checks many URLs concurrently.

## Example

```text
urlcheck urls.txt --concurrency 20 --timeout 2s
```

## Output

```text
OK      https://example.com      200   120ms
FAILED  https://bad.example.com  timeout
```

## Learning Modules

- `HttpClient`
- `async` / `await`
- `Task.WhenAll`
- `SemaphoreSlim`
- `CancellationToken`
- Timeouts
- Error modeling
- Controlled concurrency

## Completion Criteria

- Supports configurable concurrency
- Supports timeout and cancellation
- Does not create unbounded concurrent requests
- Distinguishes network, timeout, and HTTP status failures
- Has tests for core scheduling logic
