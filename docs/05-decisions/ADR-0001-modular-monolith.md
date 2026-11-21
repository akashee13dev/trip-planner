# ADR-0001: Modular Monolith for the Initial Product

**Status:** Accepted
**Source:** `docs/00-project-context/00-project-context.md`, section 4

## Context

The Trip Planner has several distinct business areas: identity, trips, membership, places, itinerary, maps, expenses, reservations, journal, and notifications. The MVP is built by a small team, and the domain boundaries are still being discovered through research.

## Decision

Build the initial product as a modular monolith:

- One deployable backend with clearly separated modules.
- Each module owns its data and business rules; other modules use its public interface, not its tables.
- An API-first backend with versioned endpoints under `/api/v1/`.
- Expense management is designed as an independent module but is not a separate service in the MVP.

## Alternatives considered

- **Microservices from the start:** independent deployment and scaling, but adds network failures, distributed transactions, and operational overhead before there is a concrete need.
- **Unstructured monolith:** fastest to start, but module boundaries erode and later extraction becomes hard.

## Consequences

- Cross-module operations can use local transactions, which keeps consistency simple.
- Module boundaries must be enforced by convention and review, since the runtime does not enforce them.
- A module can be extracted into a service later if a concrete scaling, ownership, or reliability requirement appears.
