[← Back to projects](../README.md)

# Project 6: File Backup CLI

Build a command-line tool that copies files from one directory to another.

## Features

```text
backup --source ./documents --target ./backup
backup --source ./documents --target ./backup --dry-run
backup --source ./documents --target ./backup --include "*.md"
```

## Learning Modules

- File and directory APIs
- `Path`
- Streams
- `IDisposable`
- `using`
- Error handling
- Configuration
- Logging basics

## Completion Criteria

- Supports recursive directory traversal
- Supports dry run mode
- Handles file IO errors cleanly
- Uses `using` or `await using` where appropriate
- Logs what was copied, skipped, or failed
