---
name: html-workbench
description: Create self-contained HTML artifacts for complex plans, specs, PR/code reviews, explainers, architecture diagrams, design explorations, component sheets, prototypes, reports, slide decks, and one-off editing interfaces. Use this skill whenever tables, visual design, SVG illustrations, annotated code, interaction, workflows, spatial layouts, images, or exportable UI would make the answer easier to understand, compare, share, or act on, even if the user does not explicitly ask for HTML. Skip this skill for short answers, plain prose, simple lists, small Markdown tables, or code-only responses where Markdown is clearer.
---

# html-workbench

> Diffs, call-graphs, comparisons, timelines, and tunable parameters are *spatial* information. Markdown flattens them. HTML lets the user see, compare, and act.

> The eight-category taxonomy and the export-loop discipline below are adapted from Thariq's [*HTML Effectiveness*](https://thariqs.github.io/html-effectiveness/) essay. This skill operationalizes that framework with explicit triggers, anti-triggers, pattern templates, and a UI/UX quality floor.

## 1. What this skill does

`html-workbench` helps an agent decide **when** an HTML artifact will materially improve a response, then build a **self-contained** `.html` file that earns its weight.

The artifact is a working surface for the user — a thinking surface, review surface, explanation surface, comparison surface, prototype surface, report surface, presentation surface, or editing surface. It is **not** a decorative webpage and not a portfolio piece. It exists to help a busy person understand, decide, review, tune, compare, or act faster than Markdown would let them.

Treat the file the way you'd treat a well-structured document: clear purpose, tight information architecture, restrained visual design, real interactions only where they pay for themselves.

## 2. When to use this skill

Reach for HTML when the answer is one of:

- Implementation plans, technical specs, RFCs
- Architecture explainers, system diagrams, data-flow diagrams, module maps
- PR / code reviews, annotated diffs, codebase tours
- Design explorations, design-system token sheets, component variant sheets
- Animation sandboxes, clickable prototypes, SVG figure sheets
- Research explainers, technical learning pages
- Weekly / status reports, incident timelines, postmortems
- Slide-like presentations
- One-off custom editors, prompt tuners, ticket triage boards, feature-flag editors, dataset curation tools, configuration editors
- Decision matrices, tradeoff comparisons

Trigger even if the user did not say "HTML" — these tasks almost always benefit from spatial layout, comparison, interactivity, or export.

## 3. When NOT to use this skill

Markdown wins for:

- Short answers, definitions, quick yes/no questions
- Plain prose, single paragraphs, summaries under ~200 words
- Simple lists or small Markdown tables (≤ ~6 rows × 3 columns)
- Code-only responses where the file *is* the answer
- Quick calculations, single command invocations
- Tasks where HTML would be *decorative* rather than load-bearing
- Cases where the user explicitly asked for Markdown / plain text / a code block

Be willing to say plainly: *"Markdown is the better output here."* HTML that adds friction without adding clarity is worse than no artifact at all.

## 4. HTML capability taxonomy

These eight categories form the trigger checklist. **If the task benefits from at least two, prefer an HTML artifact. If only one applies weakly, prefer Markdown.**

| # | Category | What it means | Why HTML beats Markdown | Artifacts that need it |
|---|---|---|---|---|
| 1 | **Tables** | Real `<table>` rows/columns, sortable, sticky headers | Dense comparison without ASCII alignment, scrollable, sortable | Decision matrix, status reports, token sheets |
| 2 | **Design** | Color, typography, spacing, tokens, hierarchy, states | Real CSS rather than imagined formatting | Design sheets, component states, leadership reports |
| 3 | **Illustrations** | Inline SVG diagrams, visual metaphors, figure sheets | Vector, scalable, labelable, themeable | Architecture, data flow, state machines |
| 4 | **Code** | Highlighted snippets, annotated diffs, callouts, file tours | Side-by-side panels, inline annotations, syntax color | PR reviews, code explainers, lifecycle traces |
| 5 | **Interaction** | Sliders, toggles, tabs, accordions, filters, buttons | The user can *try* it, not just read about it | Prototypes, tuners, sandboxes, editors |
| 6 | **Workflows** | Boxes, arrows, flows, timelines, state machines, pipelines | Spatial flow, not linear text | Plans, runbooks, incident timelines |
| 7 | **Spatial layouts** | Canvases, grids, side-by-side panels, module maps | Cognitive parallelism — see options at once | Design exploration, comparison, diagram sheets |
| 8 | **Images** | Embedded figures, screenshots, mockups, thumbnails | Inline visual evidence with captions | Reports, postmortems, design references |

If you find yourself using only one category and weakly (e.g. a small comparison with three rows), Markdown is probably better. Use the table above as a sanity check, not a permission slip.

## 5. Pattern selection heuristic

| User need | Pattern | Capability mix |
|---|---|---|
| Compare options | Card grid, comparison table, tradeoff matrix, side-by-side panels | Tables + Spatial |
| Explain code | Annotated snippets, call graph, request lifecycle, data-flow diagram | Code + Illustrations |
| Review a PR | Annotated diff, severity tags, reviewer checklist, changed-files map | Code + Tables + Spatial |
| Plan implementation | Timeline, milestones, architecture diagram, risks, code touchpoints | Workflows + Illustrations |
| Understand a system | Module map, request lifecycle, glossary, key invariants, dependency diagram | Illustrations + Spatial |
| Tune behavior | Sandbox with sliders / toggles / copyable parameters | Interaction + Code |
| Triage / reorder | Drag-drop board with export | Interaction + Spatial |
| Present to others | Slide-like sections with keyboard nav | Spatial + Design |
| Report status | Executive summary, timeline, shipped/slipped/blocked, follow-ups | Tables + Workflows + Design |
| Explain an incident | Timeline, impact panel, root-cause chain, logs, follow-ups | Workflows + Code + Tables |
| Show design | Component contact sheet, token table, state matrix, responsive mockups | Design + Spatial |
| Edit structured data | Form-based editor, validation, dependency warnings, copy/export output | Interaction + Code |
| Brainstorm visually | Multiple rendered directions with labeled tradeoffs | Design + Spatial |

For full templates per pattern, read `references/html_artifact_patterns.md`.

## 6. Output principles

By default, the agent should:

- Produce **one self-contained `.html` file**.
- Inline all CSS and JavaScript unless the user explicitly allows external assets.
- Avoid network dependencies (no remote scripts, no remote fonts, no analytics).
- Make the file open directly in any modern browser by double-clicking.
- Use semantic HTML (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<table>`, `<details>`).
- Use a responsive layout that works at desktop and mobile widths.
- Use accessible contrast and visible focus states.
- Use SVG for diagrams (inline, themeable, labelable).
- Use `<table>` for dense comparisons. Use `<details>` / tabs / accordions for long material.
- Include copy / export buttons for any artifact that captures user decisions.
- Include a short "How to use this artifact" line when interactions are non-obvious.
- Keep the document understandable if JavaScript fails (graceful degradation).
- Prefer clarity over cleverness.

## 7. UI/UX quality floor

Every artifact must meet this baseline:

- Clear title and one-line purpose at the top.
- Executive summary or TL;DR when the artifact is long or decision-oriented.
- Strong visual hierarchy (one obvious place to start reading).
- Readable typography: 16px minimum body text, line-height ≥ 1.5, max content width ≤ 75ch for prose.
- Adequate contrast (WCAG AA: 4.5:1 for body text, 3:1 for large text and UI).
- Responsive layout, no horizontal scrolling on mobile (unless the artifact is intentionally spatial like a board).
- Visible keyboard focus states on every interactive element.
- Touch-friendly hit targets (≥ 40px) on interactive controls.
- Semantic labels on every form input.
- Clear error / warning / success / disabled states (color *and* icon *and* text).
- Charts and diagrams labeled with legends, axes, and units.
- Color used for meaning, never alone (always pair with text, icon, shape, or position).
- Motion only when it improves understanding, with `prefers-reduced-motion` honored.
- No tiny gray text. No fake controls. No hidden essential information. No emoji-only icons.

Full checklist in `references/ui_ux_quality_floor.md`.

## 8. Design direction

Pick an intentional aesthetic before you start. The artifact's *job* dictates its *voice*:

- **Editorial / report-like** — research, leadership summaries, weekly reports.
- **Dense but calm** — implementation plans, specs, RFCs.
- **Technical / diagrammatic** — architecture explainers, system diagrams.
- **Review-focused** — PR / code reviews, with diff-aware color and severity tags.
- **Playful but controlled** — prototypes, animation sandboxes, custom editors.
- **Slide-like, high-contrast** — presentation artifacts.
- **Minimal and functional** — config editors, prompt tuners.
- **Visual and comparative** — design explorations, decision matrices.

Avoid generic AI defaults: random purple gradients, glassmorphism, bland SaaS dashboard cards, fake metrics, oversized hero sections that delay the content, decorative-only motion, meaningless icons, empty "insight" cards.

See `references/design_direction.md` for per-style guidance.

## 9. Color strategy

- **Use color for meaning**, not decoration. Reserve specific hues for success, warning, error, info, selected, disabled, changed, and risky states.
- **Keep the palette small.** Two to four accent colors beyond neutrals.
- **Aim for a 60/30/10 balance** of dominant / supporting / accent.
- **Always pair color with a redundant cue** — text, icon, shape, position — for color-blind users.
- **Use CSS variables** for tokens so colors are consistent and editable.
- **Use consistent meanings** — green is success everywhere, red is error everywhere.
- **Avoid rainbow palettes** unless the data is genuinely categorical.
- **Avoid washed-out gray text** below ~#666 on white.
- **Avoid the default purple-blue gradient** unless the brief calls for it.

Full guidance and example token sets in `references/color_strategy.md`.

## 10. Purposeful delight

Delight is seasoning, not the meal. Use it only when it improves comprehension, confidence, or usability.

Good places: copy/export confirmations, drag/drop feedback, hover/focus, empty states, success states, tiny transitions that clarify state changes, selection feedback, preview updates.

Rules:

- Keep micro-interactions fast and non-blocking (≤ 200ms).
- Honor `prefers-reduced-motion` and provide a static fallback.
- Never delay the user's task for animation.
- Never make a serious report or technical review feel unserious.
- Never use delight to paper over weak information architecture.
- Every animation needs a *reason*.

Examples in `references/purposeful_delight.md`.

## 11. Reusable HTML primitives

Borrow component vocabulary from modern UI systems, but stay framework-neutral. The default output is plain HTML / CSS / JS — **no React, Tailwind, shadcn/ui, Radix, Framer Motion, GSAP, npm, or external CDN scripts**, unless the user explicitly opts in.

Useful primitives:

- **Cards** for grouped ideas
- **Tables** for dense comparisons
- **Badges** for status / severity / type
- **Tabs** for switching related views
- **Accordions / `<details>`** for progressive disclosure
- **Alerts / callouts** for warnings, assumptions, risks
- **Timelines** for incidents, plans, history
- **Steppers / progress** for workflows
- **Sticky sidebars / TOC** for long documents
- **Code blocks with annotations** for technical artifacts
- **SVG diagrams** for architecture, data flow, pipelines, state machines
- **Forms / sliders / toggles / drag-drop boards** for editors
- **Copy / export buttons** for anything that captures decisions
- **Search / filter controls** for large sets
- **Legends** for diagrams and charts
- **Comparison matrices** for option selection
- **Checklists** for verification

Implementation snippets in `references/reusable_html_primitives.md`.

## 12. Export loop

The export loop is **the reason** an interactive HTML artifact exists, not a polish item bolted on at the end. If the user can edit, sort, tune, select, annotate, or decide something, and the artifact doesn't get those decisions back out, you've built Markdown with extra steps.

**Wire the export before you finish the styling.** A working export button on a rough artifact is more useful than a polished artifact with a missing or partial export. Test the export by actually clicking it and pasting the result somewhere — not by inspecting the code.

Things to watch for:

- **Editor without export.** A triage board that doesn't dump the columns is a waste of the user's afternoon.
- **Lossy export.** The export drops a field the user touched (reasons, notes, annotations, reorder).
- **Stale export.** What gets copied was captured at page-load, not at click time.
- **One format only when two are obviously needed.** A token sheet should export both as CSS variables and as JSON.
- **Hidden export.** The button is below the fold or behind hover; the user worries their work was lost.

Common exports:

- Copy as Markdown (paste-back into the agent)
- Copy as JSON (committable to a repo)
- Copy as prompt (next-turn input)
- Copy diff (changed fields only)
- Download JSON file
- Export reordered cards
- Export annotations
- Export accepted / rejected dataset rows
- Export tuned parameters
- Export final decision matrix
- Export implementation checklist

Show the user where the export button is. Include a "Copied!" confirmation. Snippets and patterns in `references/export_patterns.md`.

## 13. Optional media handling

If the artifact benefits from screenshots, GIF stills, image grids, frame sheets, or visual references, embed them inline (base64 or local path) **when available**.

But:

- Do not require external GIF search.
- Do not require media-generation APIs.
- Do not turn this into a sticker or GIF-making skill.
- Use SVG, diagrams, or labeled placeholders when no image is available.
- Media is evidence and illustration, never the purpose.

See `references/optional_media_handling.md`.

## 14. Recommended implementation process

1. Infer the user's real job-to-be-done.
2. Decide whether HTML adds real value over Markdown using §4's two-categories rule.
3. Identify which capability categories apply.
4. Choose an artifact pattern from §5 (or `references/html_artifact_patterns.md`).
5. Pick a design direction (§8).
6. Gather or infer the necessary inputs from the conversation.
7. Write a single self-contained HTML file with semantic structure, purposeful CSS, and minimal JavaScript.
8. Add a copy / export mechanism if the artifact captures user decisions.
9. Validate: rendering, interactive controls, copy/export, mobile readability, basic accessibility.
10. Tell the user the file path and what to inspect first.

## 15. Safety and robustness

- **Escape user-provided text** before embedding into HTML (`<`, `>`, `&`, `"`, `'`).
- **Never execute user-provided strings as JavaScript.** Treat user content as data, not code.
- **Do not include secrets** — credentials, API keys, tokens, environment variables — even if they appear in the source material.
- **Do not load remote scripts** unless explicitly permitted.
- **Preserve source references** — filenames, commit hashes, timestamps, links — when summarizing source material.
- **Prefer simple vanilla HTML/CSS/JS** unless the user opts into a framework.
- **Keep generated JavaScript small and auditable.** No minified blobs.
- **No hidden tracking, analytics, or remote calls.**
- **No forms that submit externally** unless the user asked.
- **Make the artifact useful offline.**

## 16. Visual restraint

Don't ship the AI-default look. Avoid:

- Generic SaaS-dashboard styling unless that's literally what was requested
- Fake metrics, lorem-ipsum content, placeholder logos
- Random gradients, glassmorphism, gratuitous animation
- Tiny gray text, low-contrast cards
- Emoji as primary icons
- Decorative-only UI, controls that don't do anything
- Overbuilt layouts, empty hero sections, excessive shadows / rounded cards
- Remote-asset dependence, framework assumptions
- Unlabeled charts, unexplained diagrams
- Pretty but useless dashboards

The artifact should look polished and intentional, but **not generic**. The best artifact is one the user actually reads, understands, and acts on.

---

## File map

```
html-workbench/
├── SKILL.md                                  ← you are here
├── references/
│   ├── html_artifact_patterns.md             ← 20 detailed templates (read when picking a pattern)
│   ├── ui_ux_quality_floor.md                ← practical checklist (read before final write)
│   ├── decision_heuristics.md                ← Markdown-vs-HTML decisions (read when ambiguous)
│   ├── design_direction.md                   ← per-style aesthetic guidance
│   ├── color_strategy.md                     ← tokens, palettes, contrast
│   ├── purposeful_delight.md                 ← when to animate, when not to
│   ├── export_patterns.md                    ← clipboard / download JS snippets
│   ├── reusable_html_primitives.md           ← cards, tabs, badges, etc., as plain HTML
│   └── optional_media_handling.md            ← embedding images / SVG / placeholders
├── examples/
│   ├── implementation_plan_prompt.md
│   ├── pr_review_prompt.md
│   ├── technical_explainer_prompt.md
│   ├── architecture_explainer_prompt.md
│   ├── design_exploration_prompt.md
│   ├── animation_sandbox_prompt.md
│   ├── incident_report_prompt.md
│   └── custom_editor_prompt.md
└── evals/
    └── evals.json                            ← 18 test prompts (positive + negative)
```
