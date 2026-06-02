[← Back to projects](../README.md)

# Project 11: Background Job Queue

Build an in-memory background job system.

## Features

```text
enqueue job
multiple workers
retry on failure
max retry count
timeout
graceful shutdown
job status query
```

## Learning Modules

- `Channel<T>`
- `BackgroundService`
- `CancellationToken`
- `Task`
- Retry policy
- Worker lifecycle
- Thread safety
- Logging

## Completion Criteria

- Supports multiple workers
- Supports graceful shutdown
- Does not lose currently running jobs during shutdown
- Supports retry and max retry count
- Exposes job status
- Has tests for queue behavior
