---
keyword: WORKFLOW
triggers: ["/write-a-prd", "/prd-to-plan", "/prd-to-issues", "/tdd", "/design-an-interface", "/grill-me", sub-issue, chunk, planning]
---

# Development Workflow Rules

Skill-driven loop to plan, track, and execute work.

## Phase Planning (one-time setup)

1. `/write-a-prd` — master PRD as GitHub issue
2. `/prd-to-plan` — phased plan saved to `./plans/`

## Per-Chunk Loop (repeat for each phase/feature)

1. Create a **chunk issue** from the relevant plan phase, referencing the master PRD
2. `/prd-to-issues` on the chunk issue — creates sub-issues (vertical slices)
3. For each sub-issue:
    - **New module?** → `/design-an-interface` first (3+ radically different designs, compare, pick one)
    - **Testable logic?** → `/tdd` is mandatory (red-green-refactor, vertical slices, one test at a time)
    - **Presentation-only?** → implement + manual verify (no TDD ceremony needed)
4. QA pass — create additional sub-issues as needed
5. Close chunk issue when all sub-issues resolved
6. Move to next chunk

## Issue Hierarchy

```
PRD Issue (master)
  └── Chunk Issue (one per plan phase)
        ├── Sub-issue (vertical slice)
        ├── Sub-issue (vertical slice)
        └── Sub-issue (QA finding)
```

## Closing Issues

When closing an issue:
1. **Update the body** — check off completed acceptance criteria, update any that changed from original spec. The body is the source of truth for "what shipped."
2. **Add a closing comment** — document what changed from the original spec and why. Preserves decision history. Body = what shipped, comment = what changed and why.

## Key Conventions

- One feature/chunk at a time — finish before moving on
- Sub-issues reference their parent chunk issue
- Chunk issues reference the master PRD
- `/design-an-interface` runs ONCE per new module, not per sub-issue
- TDD planning scales to complexity: brief for simple slices, thorough for complex ones
- Use `/grill-me` to stress-test design decisions before building
- `gh` CLI for all GitHub interactions
