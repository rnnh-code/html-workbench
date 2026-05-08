# Example: Custom editor (triage / curation / tuning)

## User request

> I have 32 bug reports from the last sprint. Help me triage them — sort each into P0, P1, P2, or Won't Do, with a one-line reason. I want to copy the result back into Linear when I'm done.

## Why the skill should trigger

The user is going to *do work* in the artifact (move 32 cards into 4 buckets) and then *export* the result into another system. This is the canonical case for HTML over Markdown: the artifact captures decisions and turns them into something pasteable.

## HTML capability categories

- **Interaction** — drag-drop, click-to-promote, keyboard nav.
- **Spatial layouts** — kanban-style columns.
- **Tables** — alternative dense view.
- **Workflows** — clear states (unsorted / sorted / decided).
- **Code** — exported JSON / Markdown matches what's on screen.

## Recommended pattern

Custom editor (`html_artifact_patterns.md` §14) — specifically a triage board (§16).

## Expected output structure

- Header: title, instructions ("Drag tickets between columns. Press 1-4 to assign the focused card. Click a card to add a reason.").
- Five columns: Inbox (32 unsorted) / P0 / P1 / P2 / Won't Do.
- Per-card: title, severity badge, age in days, reporter, expand-to-add-reason.
- Filter / search bar for finding a specific card.
- Stats: counts per column. "Unsorted: N remaining" prominent until 0.
- Always-visible export bar: "Copy as Markdown" / "Copy as JSON" / "Copy for Linear" with a confirmation pill.

## Expected interactions

- Drag-drop between columns.
- Keyboard: focus a card, press 1-4 to move it; arrow keys to navigate cards.
- Click a card → expand its reason input inline.
- Bulk select with shift-click; bulk assign.
- Undo (last move).
- Filter by reporter / age / severity.

## Expected export

- **Copy as Markdown** — table sorted by column, with reasons.
- **Copy as JSON** — `{ p0: [{id, title, reason}], p1: [...], ... }`.
- **Copy for Linear** — the format Linear's bulk-paste accepts.
- All three reflect the *current* state of the board, including any reasons added.

## Common failure modes

- **No undo.** A misplaced drag is permanent; users won't trust the tool.
- **No keyboard support.** Triaging 32 cards by mouse is slow.
- **Lossy export.** If the export drops the `reason` field or the column membership, the user redoes work.
- **No visible "unsorted remaining" count.** The user doesn't know when they're done.
- **Export bar that disappears on scroll.** Users panic that their work was lost.
- **Drag feedback missing.** No drop-target highlight, no original-position indicator → uncertainty about whether the move took.
- **Pretending to fetch from Linear.** This artifact stays offline. The user copies in / pastes out manually.
