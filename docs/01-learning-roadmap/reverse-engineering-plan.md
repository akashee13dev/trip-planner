# Product Reverse Engineering & Solution Architecture Plan

**Project:** Trip Planner  
**Purpose:** Understand the problems, reverse-engineer existing product behaviour, design our solution, and establish the architecture and implementation order before building anything.

---

## 1. Objective

The PRD defines **what** the product should do. This plan defines how we will investigate **why each capability exists, what problems it solves, how existing products solve those problems, and how we should design our own solution**.

We will not jump directly from the PRD to database tables, APIs, or code.

For each major capability, we will investigate:

1. **Core problem** — What real-world problem are we solving?
2. **Sub-problems** — What smaller problems make up that problem?
3. **Existing solution** — How does Wanderlog solve each sub-problem?
4. **Limitations and gaps** — What is difficult, missing, confusing, or inefficient?
5. **Our proposed solution** — What should we build differently or improve?
6. **Functional requirements** — What exact user actions and system behaviours are needed?
7. **Engineering implications** — What domain concepts, data, workflows, APIs, and components are required?
8. **Dependencies and build order** — What must exist before this module can be implemented?
9. **Validation** — How will we know the solution actually works?

We will reverse-engineer observable product behaviour, not pretend to know Wanderlog's private source code or internal architecture.

---

## 2. Six Core Problem Domains

We should organize the product around six core problems rather than treating every PRD feature as an independent module.

### 2.1 Trip Coordination

**Core problem:** A group needs one shared place to organize a trip, invite people, assign permissions, and make decisions.

**Related capabilities:**
- Identity and user profiles
- Trips
- Membership
- Permissions
- Invitations
- Polls and group decisions
- Activity feed

### 2.2 Travel Planning

**Core problem:** People have places they want to visit but need to organize them into a practical schedule.

**Related capabilities:**
- Places
- Bucket list
- Itinerary
- Scheduling and ordering
- Maps
- Routing

### 2.3 Travel Execution

**Core problem:** The original plan may not match reality. Activities take longer, people arrive late, and plans change.

**Related capabilities:**
- Visit tracking
- Schedule recalculation
- Trip progress
- Location sharing
- Notifications

### 2.4 Financial Coordination

**Core problem:** Multiple people pay for shared activities, and the group needs to know who owes whom.

**Related capabilities:**
- Expenses
- Split calculations
- Payment allocations
- Balances
- Settlements
- Financial history

### 2.5 Travel Information Management

**Core problem:** Booking details and important travel information are scattered across emails, documents, and apps.

**Related capabilities:**
- Reservations
- Confirmation details
- Attachments
- Booking information

### 2.6 Journey Preservation

**Core problem:** After the trip, people want to remember what happened, where they went, and what they experienced.

**Related capabilities:**
- Journal
- Photos and memories
- Journey timeline
- Visited places
- Completed trip experience

These domains are connected. For example, itinerary planning depends on trip membership and place management. The map depends on places and itinerary ordering. Expense settlement depends on expense records, participants, and payment allocations.

Understanding these dependencies will help us choose the correct design and implementation order.

---

## 3. Existing Product Research: Wanderlog

We will investigate Wanderlog's publicly observable product behaviour and workflows.

Areas to examine:

| Area | Observable approach to investigate | Our opportunity to explore |
|---|---|---|
| Collaboration | Shared trips, editing, viewing permissions | More structured trip-level roles and decision workflows |
| Itinerary | Day-wise activities connected to a map | Preserve planned versus expected time and track execution |
| Maps | Map pins, routes, distances, route optimization | Group-aware map and last-shared member locations |
| Expenses | Budget tracking and group bill splitting | A clearly separated expense and settlement domain |
| Reservations | Centralized booking information and imports | Reliable manual reservation management for MVP |
| Offline | Offline trip access | Consider offline-first data design when mobile becomes relevant |

For each capability, capture:
- Entry point and navigation.
- User actions and workflow.
- Required inputs.
- System response.
- Resulting state.
- Permissions.
- Failure and edge cases.
- Related features.
- Pricing or plan restrictions, where relevant.

### Evidence rules

Clearly label findings as:

- **Verified observation:** Directly observed or supported by reliable evidence.
- **Documented claim:** Stated in official product documentation or public material.
- **Inference:** A reasonable interpretation of observed behaviour.
- **Hypothesis:** A possibility that needs validation.
- **Unknown:** Information we cannot currently establish.

Do not claim to know Wanderlog's private database schema, service boundaries, algorithms, infrastructure, or source code without evidence.

Competitor limitations are hypotheses until validated. Do not automatically turn every observed limitation into a product requirement.

---

## 4. Recommended Investigation Sequence

This sequence is ordered by engineering dependencies, not by the order in which features appear in the UI.

1. **Foundation and identity**
   - Users and authentication
   - Profiles
   - Trips and trip lifecycle
   - Membership
   - Permissions
   - Invitations

2. **Collaboration engine**
   - Shared data
   - Concurrent edits
   - Polls and comments
   - Activity history
   - Notifications

3. **Places and itinerary engine**
   - Place records
   - Bucket lists
   - Scheduling
   - Ordering
   - Date handling
   - Itinerary changes

4. **Geospatial and routing engine**
   - Coordinates
   - Map rendering
   - Route calculations
   - Distances
   - Travel durations
   - Day-wise routes

5. **Travel execution engine**
   - Visit states
   - Actual versus planned times
   - Delay propagation
   - Schedule recalculation
   - Member location sharing

6. **Expense engine**
   - Expense creation
   - Split algorithms
   - Payment allocations
   - Balances
   - Settlement simplification
   - Financial audit history

7. **Reservation engine**
   - Reservation types
   - Confirmation information
   - Attachments
   - Statuses
   - Itinerary integration

8. **Journal engine**
   - Day-wise memories
   - Photos
   - Member contributions
   - Visited-place relationships
   - Historical trip views

9. **Cross-module integration**
   - Security
   - Notifications
   - Reporting
   - Performance
   - Deployment
   - Monitoring
   - End-to-end workflows

This is an investigation sequence, not a rule that one entire module must be finished before another begins. We will identify smaller dependencies and build vertical slices where appropriate.

---

## 5. Standard Research Workflow for Every Module

Follow these steps for every core problem or module.

### Step 1 — Define the core problem

Document:
- Who experiences the problem?
- In what situation does it occur?
- What are they trying to achieve?
- What makes the current process difficult?
- What happens if the problem is not solved?
- How frequently does it occur?
- How important is it to the product's value?

Write a concise problem statement.

### Step 2 — Decompose into sub-problems

For each sub-problem, document:

| Field | Description |
|---|---|
| Sub-problem | The specific difficulty |
| User | Who experiences it |
| Trigger | When it occurs |
| Current workaround | How people solve it today |
| Consequence | What goes wrong |
| Desired outcome | What success looks like |
| Priority | Critical, high, medium, or low |

Decompose by user needs, business rules, and system responsibilities—not only by UI screens.

### Step 3 — Study the existing product

Capture:
- Entry point.
- User actions.
- Required inputs.
- System response.
- Resulting state.
- Permissions.
- Failure and edge cases.
- Related features.
- Pricing or plan restrictions, if relevant.

Use official documentation, product pages, help articles, app listings, demonstrations, and direct product exploration where available. Cite sources and record the research date when information may change.

### Step 4 — Evaluate the existing solution

Ask:
- What works well?
- What is intuitive?
- What is unnecessarily complicated?
- What is missing?
- What limitations affect users?
- What happens with large itineraries or groups?
- What happens with concurrent users?
- What happens when data is incorrect or incomplete?
- What happens when a workflow fails halfway?

Separate verified limitations from hypotheses that need testing.

### Step 5 — Explore alternative solutions

For each meaningful alternative, explain:
- How it works.
- User experience.
- Technical complexity.
- Data implications.
- Reliability.
- Scalability.
- Trade-offs.
- Operational cost.
- Best use case.

Compare alternatives and avoid producing many superficial variations.

### Step 6 — Recommend our solution

State:
1. Recommended approach.
2. Why it is appropriate.
3. What we should adopt from the existing product.
4. What we should improve.
5. What we should deliberately not build.
6. MVP scope.
7. Future scope.
8. Decisions that still need validation.

Mark proposed decisions as recommendations until approved.

### Step 7 — Define functional behaviour

For each capability, document:
- Actor.
- Preconditions.
- Trigger.
- Main workflow.
- Alternative workflows.
- Business rules.
- State changes.
- Permissions.
- Validation.
- Failure behaviour.
- Expected result.
- Acceptance criteria.

Include realistic examples.

### Step 8 — Identify domain concepts

For each important concept, investigate:
- Meaning.
- Identity.
- Attributes.
- Relationships.
- Lifecycle.
- State transitions.
- Invariants.
- Ownership.
- Permissions.
- Historical requirements.

Do not create database tables before understanding the domain model.

### Step 9 — Design the technical solution

After problem and behaviour are clear, investigate:
- Domain boundaries.
- Module responsibilities.
- Application services.
- Data ownership.
- Entity relationships.
- Database constraints.
- API contracts.
- Validation.
- Transactions.
- Concurrency.
- Idempotency.
- Security and authorization.
- Error handling.
- Audit history.
- Observability.
- Testing.

Explain why each design choice is needed.

### Step 10 — Define dependencies and implementation order

Identify:
- What this module depends on.
- What other modules depend on it.
- Which capabilities can be developed independently.
- Which interfaces must be agreed upon first.
- Which work can be delivered incrementally.

Provide a dependency graph and practical build sequence.

### Step 11 — Define validation and testing

Include:
- Happy-path scenarios.
- Negative scenarios.
- Boundary conditions.
- Permission tests.
- Concurrent update tests.
- Data integrity tests.
- Failure recovery tests.
- Performance considerations.
- Acceptance criteria.

---

## 6. Required Deliverables for Each Module

Create these documents progressively.

| Document | Purpose |
|---|---|
| 01. Problem Analysis | Understand the actual user problem |
| 02. Existing Product Analysis | Understand how Wanderlog handles it |
| 03. Solution Exploration | Compare approaches and improvements |
| 04. Functional Specification | Define exact system behaviour |
| 05. Domain Design | Identify entities, relationships, states and business rules |
| 06. Technical Design | APIs, database, algorithms, transactions and components |
| 07. Dependency Analysis | Identify what must exist first |
| 08. Implementation Plan | Break work into independently buildable tasks |
| 09. Testing Strategy | Define expected behaviour and edge cases |

Do not force all nine documents to be completed in one response. Work progressively and keep them consistent.

---

## 7. Master Architecture Document

Maintain one master architecture document that captures how all modules interact.

It should contain:

1. Product context and goals.
2. Core problem domains.
3. Module boundaries.
4. Module ownership.
5. Dependency graph.
6. Shared concepts.
7. API conventions.
8. Data ownership rules.
9. Cross-module workflows.
10. Security model.
11. Architectural decisions and rationale.
12. Known risks and unresolved questions.

Whenever a module design changes, check whether it affects another module. Do not allow separate AI sessions to independently invent incompatible models, API names, identifiers, or business rules.

### Architecture Decision Records (ADRs)

Maintain an ADR for important decisions:

- Decision title.
- Context.
- Options considered.
- Decision.
- Rationale.
- Consequences.
- Date and status.

---

## 8. Architectural Principles

### 8.1 Start with domain boundaries

Group functionality by business responsibility, not just screens or database tables.

For each module, define:
- What it owns.
- What it does not own.
- What data it controls.
- What operations it exposes.
- What other modules it depends on.
- What events or notifications it may publish.
- What invariants it must protect.

### 8.2 Prefer a modular monolith initially

Unless requirements prove otherwise, consider a modular monolith for the early product.

Use:
- Clear module boundaries.
- Explicit interfaces.
- Controlled data ownership.
- Independent domain logic.
- Consistent transaction handling.
- Automated tests around module boundaries.

Do not create microservices merely because a module might become independent in the future. Good boundaries should make future extraction possible without introducing premature infrastructure.

### 8.3 API-first design

For web and future mobile clients:
- Keep business logic on the backend.
- Use versioned APIs.
- Define consistent request and response contracts.
- Document APIs.
- Enforce authorization on every protected operation.
- Standardize errors and validation.
- Consider idempotency for operations that may be retried.
- Test API contracts.

### 8.4 Data design

Before finalizing a schema, understand:
- Entity identity.
- Relationships and cardinality.
- Ownership.
- Lifecycle.
- Constraints.
- Deletion behaviour.
- Historical records.
- Transaction boundaries.
- Concurrent modifications.
- Query patterns.

Avoid storing calculated values without a clear consistency strategy.

### 8.5 Security and privacy

For each operation, ask:
- Who can perform it?
- Who owns the resource?
- Can access be revoked?
- Is the data private?
- Is an audit trail required?
- Can one user access another user's data by changing an identifier?
- Does the operation expose sensitive information?

Authorization is a backend responsibility.

---

## 9. How We Will Work Together

1. Investigate one core problem or module at a time.
2. Do not dump the entire architecture in one response.
3. Ask one focused question when an important product decision is missing.
4. Do not ask again for decisions already captured in the PRD or approved notes.
5. Challenge assumptions respectfully.
6. Explain why a design is appropriate, not just what to choose.
7. Use examples and diagrams where useful.
8. Use tables for comparisons and structured requirements.
9. Identify dependencies before recommending implementation order.
10. Keep MVP and future enhancements separate.
11. Do not start coding unless explicitly requested.
12. Do not choose a technology stack prematurely.
13. Do not claim a competitor uses a particular internal architecture without evidence.
14. Maintain approved decisions, assumptions, open questions, and risks.
15. End each investigation with what is understood and what remains unresolved.

### Teaching style

Explain concepts in this order:

1. Real-world example.
2. Product behaviour.
3. Domain concept.
4. Engineering problem.
5. Possible technical approaches.
6. Trade-offs.
7. Recommended design.

Explain technical terms briefly before relying on them.

---

## 10. Readiness Checklist Before Coding

A module is ready for implementation when these foundational points are sufficiently clear:

- [ ] Core user problem is understood.
- [ ] Sub-problems are identified.
- [ ] Existing product behaviour has been investigated.
- [ ] Evidence and assumptions are separated.
- [ ] Proposed solution is approved.
- [ ] MVP scope is defined.
- [ ] Functional workflows are documented.
- [ ] Business rules are explicit.
- [ ] States and transitions are defined.
- [ ] Permissions are defined.
- [ ] Domain concepts and relationships are understood.
- [ ] API responsibilities are agreed.
- [ ] Data ownership and transaction boundaries are clear.
- [ ] Dependencies are identified.
- [ ] Error and edge cases are considered.
- [ ] Acceptance criteria are testable.
- [ ] Module fits the master architecture.

If critical items are missing, identify them before implementation. Not every future detail must be solved, but foundational decisions must not be guessed.

---

## 11. Project-Specific Starting Point: Trip Planner

The six core problem domains are:

1. **Trip Coordination:** Identity, trips, membership, permissions, invitations, group decisions, activity.
2. **Travel Planning:** Places, bucket lists, itinerary, scheduling, maps, routing.
3. **Travel Execution:** Visit tracking, actual versus planned time, schedule recalculation, location sharing.
4. **Financial Coordination:** Expenses, split calculations, balances, settlements, financial history.
5. **Travel Information Management:** Reservations, confirmation details, attachments.
6. **Journey Preservation:** Journal, photos, memories, timeline, completed trips.

### Recommended investigation order

1. Identity and Trip Foundation.
2. Membership, Invitations and Permissions.
3. Collaboration and Shared Data.
4. Places and Bucket Lists.
5. Itinerary and Scheduling.
6. Maps and Routing.
7. Travel Execution and Progress.
8. Expense Management and Settlement.
9. Reservation Management.
10. Journal and Completed Trips.
11. Cross-module Integration and Production Readiness.

This is the starting sequence, not an irreversible implementation plan. Revise it when dependency research reveals a better order.

### First investigation: Trip Coordination

Start by understanding how a trip becomes a shared, permission-controlled workspace for multiple users.

Investigate in this order:

**Trip Coordination → Identity → Trip Lifecycle → Membership → Invitations → Permissions → Shared Data → Collaboration**

This foundation supports the rest of the product.

---

## 12. Reusable Prompt for a New AI Investigation

Use this prompt in a new AI conversation and attach the PRD and this plan.

> I want to reverse-engineer the product or module described in the attached requirements before implementing it.
>
> Act as my Product Researcher, Senior Software Architect, and Engineering Mentor.
>
> Do not generate code yet.
>
> First identify the core problem this product capability solves. Decompose it into smaller user and system problems. Research how the selected existing product handles those problems using publicly verifiable product behaviour and documentation. Distinguish verified facts, inferences, hypotheses, and unknowns.
>
> Evaluate the existing approach, identify genuine limitations, explore alternatives, and recommend a simpler or better solution for our product.
>
> Then progressively define the functional workflows, business rules, domain concepts, states, permissions, data relationships, APIs, transaction boundaries, module dependencies, implementation sequence, and testing strategy.
>
> Explain the engineering reasoning behind decisions. Do not assume access to the competitor's private source code or internal architecture. Do not invent details. Do not silently turn assumptions into requirements.
>
> Work one problem at a time. Ask one focused question only when a missing decision materially affects the design. Maintain consistency with the attached PRD and previously approved architecture decisions.
>
> The final output should be a module-level design specification that another coding AI can implement without having to invent missing business rules or architecture.
>
> Start with problem analysis, not implementation.

---

## Guiding Principle

**Understand the problem. Reverse-engineer the behaviour. Design the domain. Validate the architecture. Then build.**
