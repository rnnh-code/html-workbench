# HTML Artifact Patterns

Twenty templates. Each template lists: best use case, required sections, useful visual elements, useful interactions, export mechanism (if relevant), common mistakes, minimum quality bar.

Use this file when you've decided HTML is appropriate (per `SKILL.md` §4) and you're picking the *shape* of the artifact.

---

## 1. Implementation plan

**Best use case.** A plan that involves multiple steps, dependencies, code touchpoints, risks, and a verification path. Think: "I need to build feature X across 3 services over 2 weeks."

**Required sections.**
- Title + one-line goal
- Context / motivation (why this work, what problem it solves)
- Architecture diagram (SVG showing components and data flow)
- Phased step list with dependencies and owners
- Risk register (what could go wrong, mitigation, severity badge)
- Verification plan (how we know it's done)
- Out-of-scope / explicit non-goals

**Useful visual elements.** SVG architecture diagram, milestone timeline, risk severity badges (info / warn / critical), code-touchpoint table with file paths.

**Useful interactions.** Collapsible phase sections (`<details>`), filterable risk list, copy-as-Markdown button.

**Export.** Copy plan as Markdown for pasting into a doc / ticket; copy checklist as plain text.

**Common mistakes.** Skipping the "why" section; treating it like a TODO list with no architecture; no verification plan; making it look like a Gantt chart without owners.

**Minimum quality bar.** Reader can tell in 30 seconds: what's being built, why, in what order, who owns what, and how we'll verify.

---

## 2. PR / code review

**Best use case.** A focused review of a pull request where you want diff context, severity tags, and a reviewer checklist on one page.

**Required sections.**
- PR metadata (number, author, branch, base)
- One-line summary
- Top concerns (severity-tagged, with anchor links to inline comments)
- Annotated diff (file → hunk → comment)
- Changed-files map (sidebar list)
- Reviewer checklist (correctness, tests, security, performance, docs)
- Recommended action (approve / changes requested / discuss)

**Useful visual elements.** Severity badges (blocker / major / minor / nit / praise), inline diff with `+`/`-` coloring, sticky sidebar with file list, line-number anchors.

**Useful interactions.** Click file in sidebar → scroll to first comment in that file. Filter by severity. Collapse resolved comments.

**Export.** Copy review summary as Markdown for posting back as a PR comment.

**Common mistakes.** Burying the recommended action; mixing nits with blockers in the same list; no severity tags; not linking comments to specific lines.

**Minimum quality bar.** A reviewer can read the recommended action in 5 seconds and find the blockers in 30.

---

## 3. Technical explainer

**Best use case.** "How does X work?" — a rate limiter, caching layer, auth flow, queue, scheduler. Reader is technical but unfamiliar with the specific implementation.

**Required sections.**
- Title + one-line answer ("This is a token-bucket limiter with per-user keys.")
- Mental model (the simplest accurate metaphor)
- Annotated lifecycle / data flow (SVG)
- Step-by-step walk-through with code snippets
- Edge cases and failure modes
- Glossary (collapsible)
- Where to find this in the codebase (file paths, function names)

**Useful visual elements.** Inline SVG state machine or lifecycle diagram, color-coded code annotations, side-by-side panels for "before / after" comparisons.

**Useful interactions.** Click annotation → highlight corresponding code line. Hover diagram node → show description.

**Export.** Copy as Markdown for pasting into onboarding docs.

**Common mistakes.** Showing code without a mental model first; diagram with no labels; no edge cases; no pointer back to actual files.

**Minimum quality bar.** A reader who's never seen this code can describe what it does in their own words after 5 minutes.

---

## 4. Architecture / module map

**Best use case.** Overview of an unfamiliar system — services, dependencies, data flow, external integrations.

**Required sections.**
- Title + one-line system purpose
- Top-level architecture diagram (SVG)
- Service / module table (name, responsibility, owner, source path, key dependencies)
- Request lifecycle for the most important user-facing operation
- External dependencies (APIs, databases, queues, third-party)
- Glossary

**Useful visual elements.** Layered SVG diagram with consistent shape language (rectangle = service, cylinder = datastore, parallelogram = queue, oval = external), color by team or layer, dependency arrows.

**Useful interactions.** Click module → scroll to its row in the table. Filter table by owner or layer.

**Export.** Copy module table as JSON.

**Common mistakes.** Boxes-and-arrows soup with no legend; inconsistent shape language; no path-to-source for any module; missing external dependencies.

**Minimum quality bar.** A new engineer can name every box, point to where it lives in the code, and explain how a request flows through the system.

---

## 5. Design exploration

**Best use case.** Multiple design directions for the same problem so the user can compare and pick.

**Required sections.**
- Brief (the design problem in one paragraph)
- Three to five rendered directions, each with: name, hero, distinguishing decision, tradeoffs
- Side-by-side comparison row (typography, color, density, tone)
- Recommendation with reasoning

**Useful visual elements.** Live HTML/CSS renders (not screenshots). Comparison matrix showing key axes. Annotated pros/cons.

**Useful interactions.** Toggle between dark/light. Resize each direction inline. Mark a favorite (with export).

**Export.** Export the chosen direction's design tokens as JSON.

**Common mistakes.** Three directions that are visually identical; no recommendation; no tradeoff articulation; using fake content that obscures the visual decisions.

**Minimum quality bar.** Each direction is genuinely different on at least three axes (color, density, typography, tone). Tradeoffs are explicit.

---

## 6. Design-system token sheet

**Best use case.** Documenting the tokens (colors, type scale, spacing, radii, shadows, motion) used across the design system.

**Required sections.**
- Color palette (semantic groups: brand, neutral, status)
- Typography scale (size, weight, line-height, use case)
- Spacing scale (with visual rulers)
- Radii, shadows, borders
- Motion tokens (durations, easings)
- Token table (CSS variable name, value, where used)

**Useful visual elements.** Color swatches with hex/RGB/contrast info. Type specimens at real sizes. Spacing visualized as horizontal bars.

**Useful interactions.** Click swatch → copy CSS variable. Switch between hex / RGB / HSL.

**Export.** Copy all tokens as CSS variables. Copy as JSON. Download `tokens.css`.

**Common mistakes.** No semantic naming (just "blue-500"); no contrast info; type scale shown as the same string ("Lorem ipsum") at every size with no use-case label.

**Minimum quality bar.** A developer can copy any token and use it in code without guesswork.

---

## 7. Component variant sheet

**Best use case.** All states and variants of a single component on one page (button: default/hover/focus/active/disabled, primary/secondary/destructive, sm/md/lg).

**Required sections.**
- Component name + one-line purpose
- Variant matrix (state × style × size)
- Anatomy diagram (labeled parts)
- Accessibility notes (keyboard, ARIA, contrast)
- Usage do's and don'ts
- Code snippet for each variant

**Useful visual elements.** Live rendered components (not screenshots) on a neutral grid. Annotated anatomy diagram. Contrast ratios on every color combo.

**Useful interactions.** Click variant → copy code snippet. Toggle dark mode.

**Export.** Copy variant code as HTML.

**Common mistakes.** Showing only one state (no hover, no focus, no disabled); no accessibility notes; live components that don't actually have working focus states.

**Minimum quality bar.** Every state visible on the page. Every state has a contrast number.

---

## 8. Animation sandbox

**Best use case.** Tuning timing, easing, distance, color, or staggering of a UI animation. The user wants to *feel* it, not read about it.

**Required sections.**
- Animation preview (large, central)
- Parameter controls (sliders for duration, delay; selects for easing; color pickers)
- Code preview (CSS / JS) that updates live
- Reset to default
- Reduced-motion mode toggle

**Useful visual elements.** Big preview area, restrained controls panel, syntax-highlighted code.

**Useful interactions.** Live update. Replay button. Copy current params.

**Export.** Copy CSS / JS for the current parameters. Copy as JSON tokens.

**Common mistakes.** Preview too small to feel the motion; controls without unit labels; no reset; no reduced-motion fallback.

**Minimum quality bar.** Every parameter change is visible immediately. Every parameter has a unit. The exported code uses the current values.

---

## 9. Clickable prototype

**Best use case.** A multi-screen flow the user can click through (e.g., onboarding, checkout, settings flow) without writing real code.

**Required sections.**
- Flow map (which screens link to which)
- Each screen rendered at realistic fidelity
- Hotspots (clickable areas) with destination overlays in a "show hotspots" mode
- Notes panel (per screen)

**Useful visual elements.** Realistic content (not lorem ipsum), navigation between screens via JS state, breadcrumb showing current step.

**Useful interactions.** Click → navigate. "Show hotspots" toggle reveals link destinations. Back button.

**Export.** Export flow as JSON (screens, links, notes).

**Common mistakes.** Dead clicks (hotspots that don't go anywhere); no flow map; placeholder content that hides the design decisions.

**Minimum quality bar.** Every screen reachable. Every interactive element does something or is clearly disabled.

---

## 10. Research explainer

**Best use case.** Distilling a paper, blog post, or technical write-up into a navigable explainer.

**Required sections.**
- Title + one-paragraph plain-language summary
- Why it matters / what changed
- Annotated key figures (if available, embedded as images or recreated as SVG)
- Methodology (collapsed by default for non-technical readers)
- Glossary
- Citations / source links

**Useful visual elements.** Pull quotes for key claims, color-coded sections, sticky TOC.

**Useful interactions.** Expand methodology. Hover citation → show source.

**Export.** Copy summary section as Markdown.

**Common mistakes.** Burying the plain-language summary; replacing the source's diagrams with worse ones; losing citations.

**Minimum quality bar.** A reader who hasn't seen the paper can explain the core claim and why it matters.

---

## 11. Incident report / postmortem

**Best use case.** What happened, when, why, and what we're changing. Audience is engineering and leadership.

**Required sections.**
- Headline (impact in one sentence)
- Impact panel (users affected, duration, region, severity)
- Timeline (UTC timestamps, who did what, evidence)
- Root cause chain (5 whys or causal graph)
- Detection / response analysis (what worked, what didn't)
- Action items (owner, due date, status)
- Appendix: logs, graphs, related links

**Useful visual elements.** Vertical timeline with severity badges, root-cause diagram (SVG), action-item table.

**Useful interactions.** Filter timeline by role. Click action item → show context.

**Export.** Copy timeline as Markdown. Copy action items as JSON for ticket import.

**Common mistakes.** Blame-oriented language; missing timestamps; root cause stops at the proximate cause; action items with no owner or date.

**Minimum quality bar.** Every action item has an owner and a date. Every timestamp is UTC.

---

## 12. Weekly / status report

**Best use case.** Recurring update to leadership or a cross-functional team. "Here's what shipped, slipped, and is blocked."

**Required sections.**
- Date range
- Executive summary (3-5 bullets)
- Shipped / Slipped / Blocked sections (with owners and links)
- Metrics that moved (with deltas)
- Asks (decisions or help needed)
- Next week's focus

**Useful visual elements.** Status badges, metric tiles with delta arrows, executive summary in a callout.

**Useful interactions.** Filter by team or owner. Toggle "since last report" view.

**Export.** Copy executive summary as Markdown.

**Common mistakes.** Burying asks at the bottom; no deltas on metrics; no clear definition of "shipped"; mixing this week with general status. Color-coding metric tiles by *direction* (up = green) instead of *favorability* — see `color_strategy.md` "Metric direction" for why latency, error rate, and churn break this default.

**Minimum quality bar.** Reader knows in 60 seconds: what shipped, what slipped, what's blocked, and what they're being asked to do. Every metric tile is unambiguously good-or-bad without the reader having to think.

---

## 13. Slide deck

**Best use case.** Presentation-style artifact for sharing in a meeting or async. Each section is one slide.

**Required sections.**
- Cover slide (title, subtitle, presenter, date)
- Agenda
- Body slides (one idea per slide, large text, minimal density)
- Closing / next steps slide

**Useful visual elements.** Large headline type, restrained color, big diagrams or single key visual per slide, slide numbers.

**Useful interactions.** Keyboard nav (← → space). Fullscreen mode. Speaker-notes overlay (`s` key).

**Export.** Copy as Markdown outline. Print-to-PDF stylesheet for slide-per-page output.

**Common mistakes.** Cramming a document onto slides; tiny type; no keyboard nav; backgrounds that fight the content.

**Minimum quality bar.** Readable from across the room. Keyboard navigable. One idea per slide.

---

## 14. Custom editor

**Best use case.** A one-off tool to edit, sort, tag, or curate structured data and export the result. Examples: triage queue, tag editor, dataset reviewer.

**Required sections.**
- Title + how-to-use
- Item list (cards, rows, or kanban columns)
- Edit controls per item
- Filter / search
- Export bar (always visible)

**Useful visual elements.** Drag handles, status badges, change indicators (modified vs. unchanged).

**Useful interactions.** Drag-drop reorder. Inline edit. Bulk select. Undo. Keyboard shortcuts.

**Export.** Copy as JSON. Download as JSON / CSV. Copy as a paste-able prompt for an agent.

**Common mistakes.** No undo; no export confirmation; no indication of unsaved changes; controls that don't keyboard-work.

**Minimum quality bar.** Every change is visible. Export always works. Closing the tab without exporting feels obviously bad.

---

## 15. Prompt tuner

**Best use case.** Iterating on a prompt with parameters (system prompt, examples, temperature, top-p, model choice) and copying the final version back to an agent.

**Required sections.**
- Prompt editor (textarea with size handles)
- Parameter panel (temperature, top-p, max tokens, model)
- Few-shot examples editor
- Copy-as-prompt button (always visible)
- Diff vs. last copy

**Useful visual elements.** Token count, character count, parameter sliders with units.

**Useful interactions.** Live token count. Reset to last copied. Diff view.

**Export.** Copy full prompt + params as a single block. Copy as JSON for API use.

**Common mistakes.** No token count; no diff with previous; export missing parameters.

**Minimum quality bar.** What you copy is what would actually run.

---

## 16. Ticket triage board

**Best use case.** Sorting a batch of issues / tickets / requests into priority and ownership.

**Required sections.**
- Inbox column (unsorted)
- Priority columns (P0 / P1 / P2 / Won't Do)
- Per-ticket card with key fields (title, severity, age, reporter)
- Filter / search bar
- Export bar

**Useful visual elements.** Column counts, age badges (red after N days), severity colors.

**Useful interactions.** Drag-drop between columns. Click card → expand details. Bulk assign.

**Export.** Copy decisions as JSON. Copy as Markdown table.

**Common mistakes.** No counts on columns; no way to filter; export loses the column membership; cards too dense to scan.

**Minimum quality bar.** Tickets visibly move between columns. Export reflects every move.

---

## 17. Feature-flag editor

**Best use case.** Reviewing and editing a list of feature flags before deploying.

**Required sections.**
- Flag list with current value and proposed value
- Per-flag: description, rollout %, environment, owner
- Dependency warnings (flag X requires flag Y)
- Diff summary
- Export

**Useful visual elements.** Toggles for boolean flags, sliders for rollout %, diff badges (changed / unchanged), dependency arrows.

**Useful interactions.** Edit inline. Validate on blur. Show conflicts.

**Export.** Copy as JSON / YAML. Copy diff vs. current.

**Common mistakes.** No diff view; no dependency check; export loses unchanged flags (sometimes you want them, sometimes you don't — make it a choice).

**Minimum quality bar.** What you'd deploy is exactly what you exported.

---

## 18. Dataset curation tool

**Best use case.** Reviewing rows in a dataset and accepting / rejecting / editing them.

**Required sections.**
- Row list (or one-row-at-a-time view)
- Per-row: original content, accept / reject / edit controls, notes
- Stats panel (total, accepted, rejected, pending)
- Filter / search
- Export

**Useful visual elements.** Status badges, side-by-side original vs. edited view, progress bar.

**Useful interactions.** Keyboard shortcuts (j/k for next/prev, a for accept, r for reject). Bulk accept. Undo.

**Export.** Download accepted rows as JSONL. Download rejected with reasons.

**Common mistakes.** No keyboard shortcuts (slow with thousands of rows); no undo; no progress indication; no per-row notes.

**Minimum quality bar.** Reviewing 100 rows takes minutes, not hours.

---

## 19. Decision matrix

**Best use case.** Comparing options against weighted criteria. "Should we use X, Y, or Z?"

**Required sections.**
- Decision question
- Options (rows or columns)
- Criteria with weights (sum to 1.0 or 100%)
- Score per option per criterion (with rationale)
- Weighted total
- Recommendation

**Useful visual elements.** Heat-mapped table cells, weight indicators, total bar chart.

**Useful interactions.** Edit weights → totals recompute. Click cell → show rationale. Sort by weighted total.

**Export.** Copy matrix as Markdown. Copy decision summary as a one-paragraph rationale.

**Common mistakes.** Weights that don't sum; scores without rationale; no sensitivity check (does the decision change if a weight shifts?).

**Minimum quality bar.** Reader can recompute the decision themselves and see why option X won.

---

## 20. SVG diagram sheet

**Best use case.** A page of diagrams the user wants to embed elsewhere. Each diagram is exportable as standalone SVG.

**Required sections.**
- Page title + diagram set purpose
- Each diagram with title, description, and SVG
- Per-diagram: copy SVG / download SVG / copy as PNG (rasterized)
- Legend (consistent across diagrams)

**Useful visual elements.** Consistent shape language across diagrams, named anchor points, restrained color.

**Useful interactions.** Per-diagram copy / download. Show source code.

**Export.** Per-diagram SVG. Per-diagram PNG. Export all as a zip-equivalent (concatenated).

**Common mistakes.** Inconsistent shape language between diagrams; no legend; SVGs that copy with broken styling because of external CSS.

**Minimum quality bar.** Each SVG is fully self-contained when copied.

---

## Cross-cutting reminders

- **Two-or-more rule.** Every pattern above uses at least two of the eight HTML capability categories.
- **Export *first*, polish second.** If the artifact captures a user decision (sort, edit, tune, select, annotate, score), wire up the export button and verify it round-trips before you polish styling. Patterns 8, 9, 11, 14, 15, 16, 17, 18, 19 all live or die by their export. A polished editor with a half-wired export wastes the user's afternoon.
- **Test exports by clicking, not reading code.** Click the button, paste the result somewhere, confirm the round-trip works. Static review misses lossy / stale / partial exports.
- **Mobile is real.** Even technical artifacts get opened on phones. Respect the viewport.
- **Self-contained.** One file. Inline everything. No remote scripts.
