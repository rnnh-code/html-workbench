# Example: PR / code review

## User request

> Review PR #1834. It refactors our rate-limiter to use Redis instead of in-process counters. Pay attention to the lock acquisition logic — that's where I'm worried.

## Why the skill should trigger

A PR review benefits from spatial layout (file list sidebar + diff body), severity tagging, side-by-side comparison, anchor linking from sidebar to inline comments, and an exportable summary. Markdown can show a diff and a comment list, but loses the *spatial* relationship between the file list, the diff, and the comments.

## HTML capability categories

- **Code** — annotated diff with inline comments.
- **Tables** — concerns table, file map.
- **Spatial layouts** — sticky sidebar with file list.
- **Interaction** — filter by severity, jump to file.
- **Workflows** — reviewer checklist.

Five categories.

## Recommended pattern

PR / code review (`html_artifact_patterns.md` §2).

## Expected output structure

- Header: PR number, title, author, branch, base.
- One-line summary of what the PR does.
- Recommended action (Approve / Request changes / Discuss) — visible above the fold.
- Top concerns list, severity-tagged (blocker / major / minor / nit / praise), each anchored to its inline comment.
- Sticky sidebar: file list with comment counts per file.
- Per-file annotated diff sections: filename header, hunks, inline comments next to specific lines.
- Reviewer checklist: correctness, tests, security, performance, docs, observability.

## Expected interactions

- Click file in sidebar → scroll to that file's diff.
- Filter inline comments by severity.
- Collapse resolved comments.
- Severity badge hover → tooltip with definition.

## Expected export

- Copy summary + top concerns as Markdown for pasting back as a PR comment.
- Copy each file's comments as a Markdown block.

## Common failure modes

- **Burying the recommended action.** Reviewers should see "Request changes" or "Approve" within 5 seconds of opening.
- **Mixing severities.** A nit and a security blocker in the same flat list. Use severity tags so the user can filter.
- **Inline comments without line numbers.** Severs the link to the actual code.
- **Pretending to render the full diff** when the source isn't provided. If the user didn't paste the diff, ask or use placeholders — don't fabricate code.
- **Empty checklist items** ("Tests: ✓" with no rationale). Either justify the check or remove it.
