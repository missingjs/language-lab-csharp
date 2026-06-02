[← Back to projects](../README.md)

# Project 5: Result and Validation Library

Build a small `Result<T>` and validation library.

## Example API

```csharp
Result<User> result = UserRegistration.Create(email, password);

if (result.IsSuccess)
{
    User user = result.Value;
}
else
{
    Console.WriteLine(result.Error);
}
```

## Learning Modules

- Generics
- Records
- Pattern matching
- Domain errors
- Expected failure vs exception
- Fluent API design
- Unit testing

## Suggested Features

```text
Result<T>
Result<T, TError>
Map
Bind / Then
Match
Validation errors
Combine multiple validation results
```

## Completion Criteria

- Represents expected business failures without throwing exceptions
- Supports generic success and error values
- Can compose multiple validation steps
- Has clear tests for success, failure, and composition
- Avoids hiding unexpected system failures
