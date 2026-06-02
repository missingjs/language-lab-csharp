[← Back to projects](../README.md)

# Project 1: CLI TODO Tool

Build a command-line TODO application.

## Example Features

```text
todo add "learn C#"
todo list
todo done 1
todo remove 1
todo search async
```

## Learning Modules

- Basic C# syntax
- Classes and properties
- Records or simple classes
- `List<T>`
- File IO
- JSON serialization
- Exceptions
- `dotnet new`, `dotnet run`, `dotnet test`
- Basic unit testing

## Suggested Structure

```text
TodoCli/
├── src/
│   └── TodoCli/
│       ├── Program.cs
│       ├── TodoItem.cs
│       ├── TodoStore.cs
│       └── TodoCommandHandler.cs
└── tests/
    └── TodoCli.Tests/
```

## Completion Criteria

- Can add, list, complete, remove, and search tasks
- Persists data to a local JSON file
- Separates CLI parsing from core business logic
- Has unit tests for the core logic
- Uses clear error messages
