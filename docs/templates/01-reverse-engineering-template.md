# Template 01 — Product Reverse Engineering & Learning

> Use this template to investigate **one phase, module, sub-feature, or individual feature** in an existing product before designing our own solution.
>
> Copy this file once per topic. Replace every `[placeholder]`. Keep evidence, inference, and assumptions separate.

---

## 0. Investigation Metadata

| Field | Value |
|---|---|
| Product | [e.g. Wanderlog] |
| Area / phase | [e.g. Travel Planning] |
| Module | [e.g. Itinerary] |
| Sub-feature | [e.g. Reorder itinerary stops] |
| Feature under investigation | [Specific capability] |
| Research date | [YYYY-MM-DD] |
| Researcher | [Name] |
| Status | [Not started / In progress / Reviewed / Accepted] |
| Related PRD requirement | [Requirement ID or link] |
| Related investigations | [Links to related files] |

## 1. Learning Objective

**What am I trying to understand?**

[Write the specific product and engineering question. Avoid vague goals such as “understand itinerary”.]

**Why is this important to our product?**

[Explain which user problem or architectural decision depends on this investigation.]

**What should I be able to explain after this research?**

- [Learning outcome 1]
- [Learning outcome 2]
- [Learning outcome 3]

## 2. Real-World Problem

### 2.1 Core problem

[Describe the user's real-world difficulty without proposing a feature yet.]

### 2.2 Actors and context

| Actor | Goal | Current difficulty | Relevant permissions / constraints |
|---|---|---|---|
| [Actor] | [Goal] | [Difficulty] | [Constraints] |

### 2.3 Sub-problems

Break the core problem into smaller problems. Each should be understandable and researchable independently.

| ID | Sub-problem | Why it matters | Frequency / impact | Dependencies |
|---|---|---|---|---|
| SP-01 | [Problem] | [Impact] | [Known / estimate / unknown] | [Other sub-problem] |

### 2.4 Current user workaround

[How do people solve this today without our product? Mention spreadsheets, chat apps, maps, notes, payment apps, manual coordination, etc. where relevant.]

## 3. Existing Product Reverse Engineering

> Investigate observable product behaviour. Do not claim knowledge of private source code, database schemas, algorithms, or infrastructure unless there is direct evidence.

### 3.1 Product workflow

**Entry point:** [Where does the user start?]

**Preconditions:** [What must already exist?]

**Main flow:**
1. [User action]
2. [Product response]
3. [Next user action]
4. [Final result]

**Alternative flows:**
- [Alternative / optional path]

**Failure and edge flows:**
- [Invalid input, permission denial, network failure, duplicate action, etc.]

### 3.2 Observed behaviour

| Step | User action | Visible system response | Data / state that appears to change | Evidence |
|---|---|---|---|---|
| 1 | [Action] | [Response] | [Observed change] | [URL, screenshot, docs, test notes] |

### 3.3 Market solution comparison

| Capability | Product behaviour | Evidence type | Strength | Limitation / question |
|---|---|---|---|---|
| [Capability] | [What was observed] | [Verified / official docs / inference] | [What works well] | [What to investigate] |

### 3.4 Evidence register

| Evidence ID | Claim supported | Source / URL / screenshot | Type | Confidence | Date checked |
|---|---|---|---|---|---|
| E-01 | [Claim] | [Source] | [Direct observation / official documentation / review / inference] | [High / medium / low] | [Date] |

**Important distinction**
- **Verified observation:** Directly tested or observed.
- **Officially documented:** Stated by the product's official documentation.
- **Inference:** A possible explanation, not confirmed.
- **Hypothesis:** Needs further validation.
- **Unknown:** No reliable evidence yet.

## 4. What We Learned

### 4.1 User expectations

[What does the user expect the product to do?]

### 4.2 Important domain rules

[List rules implied by the workflow. Example: moving an itinerary item must not delete its underlying place.]

### 4.3 UX principles worth preserving

[What makes the existing workflow understandable or efficient?]

### 4.4 Limitations and opportunities

| Limitation / friction | Evidence | User impact | Opportunity for our product |
|---|---|---|---|
| [Issue] | [Evidence ID or hypothesis] | [Impact] | [Possible improvement] |

Do not label something a market weakness unless evidence supports it. Mark unverified opportunities as hypotheses.

## 5. Concepts I Need to Learn

List concepts from product/domain knowledge and software engineering separately.

### 5.1 Product and domain concepts

| Concept | What it means | Why this feature needs it | My understanding / questions |
|---|---|---|---|
| [Concept] | [Definition] | [Reason] | [Notes] |

### 5.2 Technical concepts

| Concept | What it means | Where it applies | What I need to practise |
|---|---|---|---|
| [Concept] | [Definition] | [Application] | [Exercise] |

### 5.3 Algorithms, protocols, or standards

[Describe any relevant algorithm, protocol, data standard, or mathematical concept. If none, write “Not applicable”.]

### 5.4 Learning resources

| Resource | Topic | Why it is relevant | Status |
|---|---|---|---|
| [Official docs / article / book / course] | [Topic] | [Reason] | [Not started / completed] |

## 6. Alternatives and Trade-offs

Identify at least two reasonable ways to solve the problem. Do not jump to a preferred technology before understanding the trade-offs.

| Approach | How it works | Advantages | Disadvantages / risks | Complexity | Suitable when |
|---|---|---|---|---|---|
| A. [Approach] | [Description] | [Benefits] | [Costs] | [Low / medium / high] | [Conditions] |
| B. [Approach] | [Description] | [Benefits] | [Costs] | [Low / medium / high] | [Conditions] |
| C. [Optional] | [Description] | [Benefits] | [Costs] | [Level] | [Conditions] |

**Questions to challenge the design**
- Is this solving the underlying problem or just copying a competitor feature?
- Is there a simpler solution that meets the MVP need?
- What happens when the network is slow or unavailable?
- What happens when two users act at once?
- What data must be authoritative?
- What is the security/privacy impact?
- What will become difficult to change later?

## 7. Proposed Product Direction — Initial Hypothesis

This is a research conclusion, not yet the approved architecture.

**Problem we will solve:** [Specific problem]

**Proposed user outcome:** [What the user can accomplish]

**Proposed behaviour:** [High-level workflow]

**What we may adopt from the market:** [Behaviours]

**What we may improve:** [Evidence-based improvement or clearly labelled hypothesis]

**What we will not build now:** [Out of scope]

**Open questions:** [Questions that block a final decision]

## 8. Dependencies and Boundaries

| Dependency | Why it is needed | Existing / future module | Required before implementation? |
|---|---|---|---|
| [Dependency] | [Reason] | [Module] | [Yes / no / partial] |

**This topic owns:** [Responsibilities]

**This topic does not own:** [Responsibilities that belong elsewhere]

**Inputs it needs:** [Data / events / user actions]

**Outputs it provides:** [Data / events / results]

## 9. Validation Plan

### 9.1 Scenarios to test

| Scenario | Given | When | Expected result | Priority |
|---|---|---|---|---|
| Happy path | [Initial state] | [Action] | [Expected behaviour] | [P0/P1/P2] |
| Invalid input | [Initial state] | [Action] | [Expected behaviour] | [Priority] |
| Unauthorized user | [Initial state] | [Action] | [Expected behaviour] | [Priority] |
| Concurrent action | [Initial state] | [Two actions] | [Expected behaviour] | [Priority] |
| Failure / retry | [Initial state] | [Failure] | [Expected behaviour] | [Priority] |

### 9.2 How will we know the solution is better?

[Define observable measures or usability outcomes. Do not invent numeric targets without a basis.]

## 10. Research Conclusion

**What I now understand:**
- [Point]

**What remains unclear:**
- [Point]

**What we should carry into product design:**
- [Point]

**Recommendation:** [Proceed / research more / simplify / defer / reject]

**Confidence:** [High / medium / low] — [Explain why]

## 11. Review Checklist

- [ ] Core problem is stated without assuming a feature.
- [ ] Sub-problems are independently understandable.
- [ ] Existing product workflow was actually inspected.
- [ ] Claims are labelled by evidence type.
- [ ] Unknown internals are not presented as facts.
- [ ] Relevant domain and technical concepts are understood.
- [ ] At least two solution approaches were compared.
- [ ] MVP boundary is clear.
- [ ] Dependencies and ownership are identified.
- [ ] Edge cases and validation scenarios are documented.
- [ ] Open questions are visible.

---

## Reusable AI Prompt — Reverse Engineering Tutor

You are my product reverse-engineering researcher and engineering tutor.

I am investigating **[product / module / feature]** for a group travel-planning SaaS. Use this template as the structure of the investigation.

Your responsibilities:

1. Start with the real user problem. Do not assume the requested feature is the correct solution.
2. Break it into small, independently understandable sub-problems.
3. Research how the named market product currently behaves. Prefer official product documentation and direct observable workflows. Cite sources for current claims.
4. Clearly label verified observations, official documentation, inferences, hypotheses and unknowns.
5. Never invent the competitor's private architecture, database schema, algorithms or infrastructure.
6. Teach every required product and technical concept from first principles, with examples.
7. Compare at least two viable technical approaches and explain trade-offs.
8. Challenge unnecessary complexity and identify a simpler MVP solution.
9. Identify dependencies, data ownership, failure cases, security and concurrency concerns.
10. Do not write implementation code unless I explicitly ask for a small learning exercise.

Ask me focused questions one at a time when a decision depends on my product intent. Do not silently make important product decisions for me.

At the end, summarize what I understand, what I still need to learn, what evidence is missing and whether this topic is ready to move into product architecture design.
