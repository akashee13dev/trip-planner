# Trip Planner AI Workbook — How to Use It

## The correct workflow

**Do not complete Template 1 for every phase before starting Template 2.**

Work one subfeature at a time. For each subfeature, complete the learning/reverse-engineering stage, then immediately design your own product architecture.

Example:
1. Phase 1 → User Registration → Template 1.
2. Phase 1 → User Registration → Template 2.
3. Phase 1 → Authentication → Template 1.
4. Phase 1 → Authentication → Template 2.
5. Continue through the phase's subfeatures, then move to the next phase.

This creates a tight learning-to-design feedback loop. It also helps reveal dependencies and architecture decisions early.

## What to give the AI each time

For a Template 1 investigation:
1. `docs/00-project-context/00-project-context.md`
2. The relevant phase context from `docs/02-phase-contexts/`
3. `docs/templates/01-reverse-engineering-template.md`
4. `docs/prompts/01-reverse-engineering-prompt.md`
5. The reference product name and the exact subfeature being investigated.

For a Template 2 design:
1. `docs/00-project-context/00-project-context.md`
2. The relevant phase context
3. Your completed Template 1 document for that same subfeature
4. `docs/templates/02-product-architecture-template.md`
5. `docs/prompts/02-product-architecture-prompt.md`

## Example: Expense Management

Investigate and design each subfeature separately:
- Create expense
- Multiple payers
- Equal split
- Custom split
- Percentage split
- Individual balances
- Simplify settlements
- Record settlements
- Expense history

For each item, do Template 1 first and Template 2 second.

## Keep the documents organized

Completed documents live in two parallel trees, one per template, using the same phase and subfeature folder names (see `repository-and-branching-guide.md`):

```text
docs/
├── 03-reverse-engineering/
│   └── phase-01/
│       └── user-registration/
│           └── 01-reverse-engineering.md
└── 04-product-architecture/
    └── phase-01/
        └── user-registration/
            └── 02-architecture-design.md
```

Use lowercase kebab-case for folder names. Tick the subfeature's columns in `docs/01-learning-roadmap/phase-feature-tracker.csv` when each document is merged.

## Important distinction

- Template 1 answers: What problem exists, how does the market solve it, what can I observe, and what engineering concepts must I learn?
- Template 2 answers: Given what I learned and what my product needs, how should I design my solution?

Do not treat a competitor's visible behaviour as proof of its internal architecture. Record uncertainty explicitly.

## Recommended first exercise

Start with Phase 1 → User Registration, or Phase 0 foundations if you want to establish domain vocabulary first. Keep the first investigation small enough to complete and review thoroughly.
