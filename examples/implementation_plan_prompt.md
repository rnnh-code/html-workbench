# Example: Implementation plan

## User request

> We need to migrate our auth service from session cookies to JWT-based authentication. It's used by web, mobile, and three internal services. Plan the migration — phased rollout, code touchpoints, risks, verification.

## Why the skill should trigger

This is a multi-step technical plan with code touchpoints, dependencies, sequencing, and risks. A Markdown response would either be a wall of bullet points (hard to scan) or a thin outline (missing the architecture and risks). HTML lets the user *see* the architecture, *jump* to phases, and *export* the checklist into their tracker.

## HTML capability categories

- **Workflows** — phased rollout with dependencies.
- **Illustrations** — SVG showing current vs. target architecture.
- **Tables** — code touchpoints, risks, verification matrix.
- **Code** — example tokens / claims structure.
- **Spatial layouts** — phases beside their owners and risks.

Five categories — comfortably above the two-or-more threshold.

## Recommended pattern

Implementation plan (`html_artifact_patterns.md` §1).

## Expected output structure

- Title + one-line goal ("Migrate auth from session cookies to JWT, zero-downtime, Q3.")
- Context (why now, what problem it solves, blast radius).
- Side-by-side architecture diagrams: *before* (cookie-based) and *after* (JWT-based), as inline SVG.
- Phased plan: Phase 0 (prep) → Phase 1 (dual-write) → Phase 2 (cutover) → Phase 3 (cleanup). Each phase has goals, owners, code touchpoints (with file paths), and an exit criterion.
- Risk register table: risk, severity badge, likelihood, mitigation.
- Verification plan: how we know each phase is done.
- Out-of-scope section: what we are explicitly *not* changing.

## Expected interactions

- Sticky TOC for jumping between phases.
- `<details>` collapsing each phase's code touchpoints.
- Filter the risk register by severity.
- Click a phase milestone → smooth scroll to its section.

## Expected export

- Copy the phased plan as Markdown for pasting into a doc.
- Copy the action items as a checklist (`- [ ]` Markdown).
- Copy the risk register as a Markdown table.

## Common failure modes

- **Skipping the "why".** Plans without context get rejected by reviewers who weren't in the original conversation.
- **Treating it like a TODO list.** Without architecture and risks, the plan is just a sequence and doesn't help anyone catch issues early.
- **Fake metrics.** Don't invent timelines, headcount, or SLOs. Use placeholders the user can fill in.
- **No verification plan.** "We'll know when it's done" doesn't survive a real migration.
- **Pretending it's a Gantt chart.** Without owners and dates, a Gantt is decorative. Use a phase list with owners instead.
