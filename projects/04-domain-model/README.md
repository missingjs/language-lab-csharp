[← Back to projects](../README.md)

# Project 4: Strongly Typed Domain Model

Build a pure domain model without a database or web framework.

## Recommended Domains

- Payment workflow
- Subscription billing
- Inventory reservation
- Ticket booking
- Order checkout

## Learning Modules

- Records
- Record structs
- Value objects
- Strongly typed IDs
- Enums
- Pattern matching
- Immutable updates
- Domain events

## Example

```csharp
public readonly record struct OrderId(Guid Value);
public readonly record struct Email(string Value);

public enum PaymentStatus
{
    Pending,
    Authorized,
    Captured,
    Failed
}
```

## Completion Criteria

- Avoids primitive obsession for important domain concepts
- Uses records or record structs for value objects
- Models states explicitly
- Uses pattern matching for state transitions
- Keeps core domain logic independent of UI, database, and web frameworks
