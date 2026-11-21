# Trip Planner

A collaborative trip planning application focused on group travel: plan together, travel effortlessly, remember forever.

This repository records how the product moves from research to architecture to implementation. Every subfeature is first studied against a reference product (Wanderlog), then designed, and only then built.

## Status

Research and design. No implementation stack has been selected yet.

## Repository layout

| Path | Contents |
|---|---|
| `docs/00-project-context/` | Project context and the product requirements document (PRD) |
| `docs/01-learning-roadmap/` | Learning roadmap, research plan, playbook, and the phase/feature tracker CSV |
| `docs/02-phase-contexts/` | One context file per phase (00–11) |
| `docs/03-reverse-engineering/` | Completed Template 1 documents, by phase and subfeature |
| `docs/04-product-architecture/` | Completed Template 2 documents, by phase and subfeature |
| `docs/05-decisions/` | Architecture Decision Records (ADRs) |
| `docs/templates/` | Template 1 (reverse engineering) and Template 2 (architecture design) |
| `docs/prompts/` | Reusable AI prompts for each template |
| `docs/reference/wanderlog/` | Raw notes from studying the reference product |

`backend/`, `frontend/`, `database/`, and `infrastructure/` will be added once the stack is chosen.

## How to work

1. Read `docs/how-to-use-the-workbook.md`.
2. Follow `docs/repository-and-branching-guide.md` for branches, commits, and pull requests.
3. For each subfeature: research branch (Template 1) → architecture branch (Template 2) → implementation branch.
