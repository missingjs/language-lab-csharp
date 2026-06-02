[← Back to projects](../README.md)

# Project 2: Log Analyzer

Build a command-line log analysis tool.

## Example Input

```text
2026-01-01T10:00:00Z GET /users 200 23ms
2026-01-01T10:00:01Z POST /login 500 80ms
```

## Example Output

```text
Total requests: 12000
Status 200: 10300
Status 500: 87
Top paths:
  /users 3200
  /login 900
Slowest endpoints:
  ...
```

## Learning Modules

- File streaming
- `IEnumerable<T>`
- LINQ
- Records
- Pattern matching
- Regular expressions
- Aggregation
- Error handling
- Unit tests with sample files

## Completion Criteria

- Processes large files without loading everything into memory
- Parses log lines into typed records
- Uses LINQ for filtering, grouping, and aggregation
- Reports malformed lines clearly
- Has tests for parsing and aggregation
