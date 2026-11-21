# Trip Planner Repository Setup & Branching Strategy

This document explains how to create and organize the Trip Planner GitHub repository, which branches to use, and how to keep product research, architecture, and implementation work organized.

## 1. Create the GitHub repository

Recommended repository name:

```text
trip-planner
```

Recommended initial settings:
- Visibility: **Private** while the product and research are evolving. Make it public later if you want to showcase the work.
- Initialize with a `README.md`.
- Add a `.gitignore` appropriate for the backend, frontend, and development environment as those technologies are selected.
- Add a licence only after deciding how you want others to use the project.
- Never commit passwords, API keys, access tokens, production data, or real `.env` files.

## 2. Recommended branch strategy

Start with a simple strategy. Do not create a permanent branch for every phase or every module.

### Permanent branches

| Branch | Purpose |
|---|---|
| `main` | Stable, reviewed work. Keep it in a state you could safely demonstrate or release. |
| `develop` | Optional integration branch. Add it only when you have a real need to combine several ongoing changes before promoting them to `main`. |

**Recommendation for a solo developer:** Begin with `main` only. Create short-lived task branches from `main`, merge them back after review, and delete them. Introduce `develop` later if your release workflow genuinely needs it.

### Short-lived working branches

Create a branch for a specific piece of work, not for an entire phase.

Use these naming patterns:

| Work type | Naming pattern | Example |
|---|---|---|
| Product research | `docs/research/<phase>-<topic>` | `docs/research/phase-02-invitations` |
| Architecture design | `docs/architecture/<phase>-<topic>` | `docs/architecture/phase-02-invitations` |
| Documentation maintenance | `docs/<topic>` | `docs/update-learning-roadmap` |
| Backend implementation | `feature/backend-<topic>` | `feature/backend-trip-creation` |
| Frontend implementation | `feature/frontend-<topic>` | `feature/frontend-trip-creation` |
| Bug fix | `fix/<topic>` | `fix/invitation-expiry-validation` |
| Tests | `test/<topic>` | `test/expense-equal-split` |
| Build or infrastructure | `chore/<topic>` | `chore/add-ci-workflow` |

Use lowercase kebab-case. Keep branch names short, descriptive, and tied to one reviewable task.

## 3. How to work through each subfeature

For every subfeature, keep the research, architecture, and implementation connected.

Example: Phase 2 → Email Invitations.

### Step A — Research the reference product

Create:

```bash
git switch main
git pull
git switch -c docs/research/phase-02-email-invitations
```

Work on:
- The real-world problem.
- Observable behaviour in the reference product.
- User workflows and business rules.
- Edge cases and failure scenarios.
- Engineering concepts to learn.
- Evidence, assumptions, and unanswered questions.

Save the completed Template 1 document under:

```text
docs/03-reverse-engineering/phase-02/invitations/
└── 01-reverse-engineering.md
```

Commit and merge the research branch when the document is ready for review.

### Step B — Design your product architecture

Create a new branch:

```bash
git switch main
git pull
git switch -c docs/architecture/phase-02-email-invitations
```

Use the approved research document and Template 2 to design:
- Requirements and workflows.
- Business rules and state transitions.
- Domain model and database design.
- API contracts.
- Permissions and security.
- Failure handling and consistency.
- Module boundaries and tests.

Save the completed Template 2 document under:

```text
docs/04-product-architecture/phase-02/invitations/
└── 02-architecture-design.md
```

Review and approve the architecture before implementation. Merge the documentation branch when ready.

### Step C — Implement the approved design

Create a separate implementation branch:

```bash
git switch main
git pull
git switch -c feature/backend-email-invitations
```

Implement a small vertical slice based on the approved design. Add tests and update documentation if implementation reveals a necessary design change.

Merge after review and successful checks.

**Important:** If you are using `develop`, create task branches from `develop` and merge them back into `develop`. Promote tested, integrated work from `develop` to `main` according to your release process.

## 4. Suggested repository structure

```text
trip-planner/
│
├── README.md
├── AGENTS.md
├── .gitignore
├── .env.example
│
├── docs/
│   ├── 00-project-context/
│   │   └── 00-project-context.md
│   │
│   ├── 01-learning-roadmap/
│   │   └── trip-planner-learning-roadmap.csv
│   │
│   ├── 02-phase-contexts/
│   │   ├── phase-00-foundations.md
│   │   ├── phase-01-identity-trip.md
│   │   └── ...
│   │
│   ├── 03-reverse-engineering/
│   │   ├── phase-01/
│   │   │   ├── user-registration/
│   │   │   │   └── 01-reverse-engineering.md
│   │   │   └── trip-creation/
│   │   │       └── 01-reverse-engineering.md
│   │   └── ...
│   │
│   ├── 04-product-architecture/
│   │   ├── phase-01/
│   │   │   ├── user-registration/
│   │   │   │   └── 02-architecture-design.md
│   │   │   └── trip-creation/
│   │   │       └── 02-architecture-design.md
│   │   └── ...
│   │
│   └── 05-decisions/
│       ├── README.md
│       └── ADR-0001-modular-monolith.md
│
├── backend/
├── frontend/
├── database/
└── infrastructure/
```

Create implementation folders when you have selected the stack and are ready to build. Do not add empty folders just to make the tree look complete.

## 5. Initial setup commands

After creating an empty GitHub repository, clone it:

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd trip-planner
```

Add your initial documentation and folders, then:

```bash
git add .
git commit -m "chore: initialize trip planner repository structure"
git push -u origin main
```

Create a research branch for your first subfeature:

```bash
git switch -c docs/research/phase-01-user-registration
```

After completing the work:

```bash
git add docs/
git commit -m "docs: document user registration research"
git push -u origin docs/research/phase-01-user-registration
```

Open a Pull Request on GitHub, review the changes, and merge into `main`.

For the next task, return to the base branch and create a fresh branch:

```bash
git switch main
git pull
git switch -c docs/architecture/phase-01-user-registration
```

## 6. Pull Request checklist

Before merging a research or architecture change:
- [ ] The document is saved in the correct location.
- [ ] The phase, feature, and subfeature are clearly identified.
- [ ] Observations are separated from assumptions and hypotheses.
- [ ] Sources are recorded where applicable.
- [ ] Open questions and unresolved decisions are visible.
- [ ] No unrelated files or changes are included.

Before merging implementation:
- [ ] The implementation follows the approved architecture or documents why it differs.
- [ ] Authorization and validation are handled on the backend.
- [ ] Relevant tests are added and run.
- [ ] No secrets or private data are committed.
- [ ] API and architecture documentation are updated when needed.
- [ ] Known limitations are recorded.

## 7. Git commit message convention

Use a simple conventional style:

```text
docs: add invitation research
docs: design invitation architecture
feat: implement trip creation endpoint
fix: validate expired invitations
test: cover equal expense splitting
chore: configure backend build
```

Suggested prefixes:
- `docs:` documentation and research.
- `feat:` new product functionality.
- `fix:` bug fixes.
- `test:` tests.
- `refactor:` code restructuring without intended behaviour change.
- `chore:` tooling, configuration, and maintenance.

## 8. What not to do

- Do not create a permanent branch for every phase.
- Do not keep one long-lived branch for all research.
- Do not mix research, architecture, and implementation into one huge change when they can be reviewed separately.
- Do not merge unreviewed AI-generated architecture as an approved decision.
- Do not force-push or rewrite shared history casually.
- Do not commit `.env` files, secrets, database dumps, or real user information.
- Do not introduce `develop` unless it solves an actual integration or release need.

## 9. Recommended starting plan

1. Create the private GitHub repository `trip-planner`.
2. Add `README.md`, `AGENTS.md`, and `.gitignore`.
3. Add the `docs/` structure and copy in the project context, phase contexts, templates, roadmap, and CSV tracker.
4. Start with `main` only.
5. Create `docs/research/phase-00-foundations` for the initial foundation work.
6. Complete one subfeature's Template 1, then Template 2, in separate branches.
7. Begin implementation only after the relevant architecture is reviewed and approved.

The goal is a clean, understandable history showing how the product moved from research to architecture to implementation.
