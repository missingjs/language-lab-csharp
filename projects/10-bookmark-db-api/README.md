[← Back to projects](../README.md)

# Project 10: Database-backed Bookmark API

Extend the Minimal Web API with database persistence.

## Recommended Options

- SQLite for simplicity
- PostgreSQL for production-like practice

## Learning Modules

- EF Core
- `DbContext`
- Migrations
- LINQ-to-SQL translation
- Transactions
- Tracking vs no tracking
- Integration tests

## Completion Criteria

- Uses EF Core migrations
- Keeps persistence concerns out of the domain model where reasonable
- Uses async EF Core APIs
- Passes `CancellationToken`
- Has integration tests against a real test database
- Avoids obvious N+1 query patterns
