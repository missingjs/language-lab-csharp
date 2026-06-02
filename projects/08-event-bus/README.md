[← Back to projects](../README.md)

# Project 8: Typed Event Bus

Build a small in-process event bus.

## Example API

```csharp
await eventBus.PublishAsync(new UserCreated(userId), cancellationToken);
```

## Learning Modules

- Interfaces
- Generics
- Variance
- Delegates
- Async handlers
- Dependency inversion
- Error handling

## Suggested Model

```csharp
public interface IEventHandler<in TEvent>
{
    Task HandleAsync(TEvent eventMessage, CancellationToken cancellationToken);
}
```

## Completion Criteria

- Supports registering and invoking handlers
- Supports async handlers
- Passes `CancellationToken`
- Handles handler failures explicitly
- Demonstrates generic event dispatch
