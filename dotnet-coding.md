# Personal .NET Coding Instructions (C# 10+, .NET 7/8)
# Copilot: follow these rules strictly when generating C# code

## Core Values
- Prefer readable, boring, maintainable code over cleverness
- Optimize for correctness and clarity first
- Keep changes small, reviewable, and revertible
- Avoid unnecessary abstractions, frameworks, patterns
- Follow existing conventions unless improving deliberately

## Architecture Principles
- Separate concerns: API/hosting, application, domain, infrastructure
- Keep domain/business logic free of framework dependencies
- Constructor injection only; avoid service locators
- Prefer composition over inheritance
- Use explicit data-in/data-out services with minimal side effects
- Keep boundaries clear: validate at edges, enforce invariants
- Avoid CQRS/event sourcing/mediators unless complexity demands

## Project Structure & Dependencies
- Organize by feature or bounded area; avoid deep folder hierarchies
- Keep dependency direction one-way; avoid cyclic references
- Minimize public surface area; default to internal
- Do not expose EF/ORM entities beyond data access

## C# Coding Style
- Use nullable reference types correctly; avoid null-forgiving operators
- Keep methods small and focused; one responsibility per method
- Guard clauses preferred; keep nesting shallow
- Explicit names for types/methods; explicit types unless obvious
- Avoid magic numbers/strings; centralize constants
- Minimal, purposeful comments only

## Async & Concurrency
- Async for IO-bound work; propagate CancellationToken
- Avoid async for CPU-bound work; use synchronous or background processing
- Use Task.WhenAll for independent operations; avoid unbounded parallelism
- No Task.Run in server code except explicit background work
- Prevent deadlocks: avoid .Result/.Wait

## Error Handling
- Throw early; use typed exceptions; preserve stack traces
- Catch only to add context, translate to boundary, or recover safely
- Validate inputs at edges; enforce invariants in core logic

## Logging & Observability
- Use structured logging; stable event names/IDs; meaningful properties
- Avoid logging sensitive data (PII, secrets)
- Correlate logs with trace/activity IDs
- Log failures with context; avoid noisy success logs
- Emit metrics for latency, throughput, error rates

## Testing
- Fast, deterministic unit tests
- Test business rules and edge cases; minimal mocks
- Integration tests for boundaries (DB, HTTP, messaging)
- Prefer testing outcomes over implementation details
- Keep test data realistic and minimal

## Data Access
- Avoid “get all then filter in memory”
- Small transactional scopes; batch queries when reasonable
- Server-side filtering, paging, and projections
- Treat migrations/schema changes as contract; review carefully

## Performance
- Measure before optimizing; profile in production-like scenarios
- Avoid unnecessary allocations in hot paths
- Watch N+1 queries and over-fetching
- Use caching only with clear invalidation strategy
- Prefer streaming for large payloads; enforce limits at boundaries

## Security
- Validate and encode all input; assume hostile input
- Apply least privilege for identities, permissions, data access
- Never log secrets; use secure storage
- Use platform cryptography; never roll your own
- Handle authn/authz explicitly; deny by default

## Configuration & Environment
- Use strongly typed, validated configuration at startup
- Fail fast on missing or invalid config
- Environment-specific behavior via configuration, not code
- Keep time, culture, and timezone explicit; prefer UTC internally

## Maintainability & Change Management
- Prefer incremental refactors over rewrites
- Remove dead code; avoid “just in case” hooks or flags
- Keep dependencies updated pragmatically; avoid bleeding edge
- Document architectural and operational decisions briefly

## Self Code Review Checklist
- Intent obvious from names and structure?
- Boundaries respected; dependencies clean?
- Async, cancellation, and error paths correct?
- Logs useful, non-sensitive, and structured?
- Tests cover business-critical behavior and edge cases?
- Avoidable complexity removed?
