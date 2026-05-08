# html-workbench

> An AI-agent skill that teaches when and how to produce self-contained HTML artifacts instead of plain Markdown — for plans, specs, code reviews, explainers, design explorations, prototypes, reports, slide decks, and one-off editing interfaces.

## Origin and credit

This skill is a direct descendant of **[Thariq's "HTML Effectiveness"](https://thariqs.github.io/html-effectiveness/)** essay (X: [@trq212](https://x.com/trq212)). The eight-category capability taxonomy, the "spatial information that Markdown flattens" framing, the always-end-with-an-export-button discipline, and the use-case clustering (specs, code review, design, reports, custom editors) all come from his work. If you haven't read his essay, **read it first** — it's the load-bearing source.

> *"Markdown has become the dominant file format used by agents to communicate with us... but as agents have become more and more powerful, I have felt that markdown has become a restricting format. I find it difficult to read a markdown file of more than a hundred lines."* — Thariq, *HTML Effectiveness*

Thariq is also mildly skeptical of skill-ification — he writes: *"I'm a little bit afraid that people will read this article and turn it into a /html skill or something. While there might be some value in that, I want to emphasize that you don't need to do much to get Claude to do this."* He's right that you don't *need* a skill to ask an agent for an HTML file. This skill exists for three specific reasons:

1. **Trigger calibration.** Agents tend to under-trigger HTML output unless prompted to. Equally importantly, they tend to *over-trigger* once exposed to the idea — wrapping definitional questions and code-only answers in styled pages. The skill encodes both positive triggers and explicit anti-triggers (short answers, simple lists, code-only responses, explicit Markdown requests) so the same agent makes the right call across many sessions and many users.
2. **Pattern templates.** Thariq's essay names the use cases. This skill ships twenty detailed templates — required sections, useful interactions, export mechanisms, and common mistakes per pattern — so an agent doesn't re-derive the structure of an incident report or a design exploration from scratch each time.
3. **Quality floor.** Accessibility, contrast, semantic HTML, framework neutrality, color discipline, and the export-loop discipline benefit from a written reminder. The skill bundles a UI/UX checklist and ready-to-paste vanilla JavaScript export snippets.

The skill is not an alternative to reading Thariq's essay. It's a thicker, opinionated layer on top, intended for agents that benefit from explicit structure.

## The thesis (Thariq's, summarized)

Diffs, call-graphs, side-by-side comparisons, timelines, and tunable parameters are *spatial* information. Markdown flattens them. HTML lets the user **see**, **compare**, **interact with**, and **export** the artifact — turning a one-shot text answer into a reviewable, shareable, editable surface.

For complex cognitive work, an HTML artifact opened in a browser is often the difference between "I read it and I think I understand" and "I see it and I can decide." Thariq's essay opens with examples of this and then makes the case across information density, ease of reading, ease of sharing, two-way interaction, data ingestion, and feeling more in the loop with the agent. All of that grounds this skill.

## What it produces

`html-workbench` covers twenty artifact patterns, including:

- **Documents** — implementation plans, specs, RFCs
- **Reviews** — PR / code reviews with annotated diffs and severity tags
- **Explainers** — architecture maps, request lifecycles, technical walkthroughs
- **Reports** — weekly status reports, incident postmortems
- **Design surfaces** — token sheets, component variant matrices, design explorations
- **Prototypes** — clickable flows, animation sandboxes, slide decks
- **Editors** — triage boards, prompt tuners, feature-flag editors, dataset curation tools

Every artifact is a **single self-contained `.html` file** — no React, no Tailwind, no shadcn/ui, no CDN scripts, no npm. Just plain HTML, CSS, and a small amount of vanilla JavaScript. Open it in any browser, share it, fork it, edit it.

## When to use

Reach for HTML when the response would meaningfully use **two or more** of these eight capability categories (a direct adaptation of Thariq's information-density list):

| | | |
|---|---|---|
| 1. Tables | 2. Design | 3. Illustrations |
| 4. Code | 5. Interaction | 6. Workflows |
| 7. Spatial layouts | 8. Images | |

If only one applies weakly — a five-line code answer, a three-row comparison, a quick definition — Markdown is the right format. The skill explicitly declines to trigger for those. In a bundled benchmark of 18 prompts (14 that should produce HTML, 4 that should produce Markdown), the skill correctly triggered or declined on all 18.

## Install

### Claude Code

```bash
git clone https://github.com/rnnh-code/html-workbench ~/.claude/skills/html-workbench
```

The skill is auto-discovered. Restart Claude Code if it's running, then ask for any of the artifact types above.

### Other agents

The skill is **agent-agnostic by design**. The whole package is plain Markdown plus one JSON file:

```
html-workbench/
├── SKILL.md                      # entry point with metadata frontmatter
├── references/                   # 9 detailed guides (load on demand)
├── examples/                     # 8 worked example prompts
└── evals/evals.json              # 18 evals (14 positive + 4 negative)
```

If your agent platform supports skills with YAML frontmatter, drop the directory in. If not, point your agent at `SKILL.md` directly — it's a structured prompt that any sufficiently capable model can follow.

## How it's organized

- **`SKILL.md`** — 16 sections covering the decision rule (when HTML, when Markdown), the eight-category capability taxonomy, the pattern selection heuristic, output principles, the UI/UX quality floor, design direction, color strategy, purposeful delight, reusable HTML primitives, the export loop, and safety rules.
- **`references/html_artifact_patterns.md`** — twenty detailed templates with required sections, useful interactions, export mechanisms, and common mistakes per pattern.
- **`references/ui_ux_quality_floor.md`** — accessibility, contrast, typography, spacing, and responsive checklist.
- **`references/decision_heuristics.md`** — disambiguates documents vs. reports vs. dashboards vs. prototypes vs. editors vs. slide decks vs. diagram sheets vs. design sheets.
- **`references/export_patterns.md`** — vanilla JavaScript snippets for clipboard, download, diff, and JSON export. The export loop is treated as a first-class reason to use HTML over Markdown — directly inheriting Thariq's "always end with an export button" rule.
- **`references/reusable_html_primitives.md`** — cards, badges, tabs, accordions, callouts, timelines, code blocks, SVG diagrams, drag-drop boards, and copy buttons — all as plain HTML/CSS/JS, no framework dependencies.
- **`references/color_strategy.md`** — semantic colors, neutral palettes, contrast, color-blind safety, the 60/30/10 balance, metric direction (latency-down-is-good).
- **`references/design_direction.md`** — picking an aesthetic appropriate to the artifact's job, and the bad-default AI design habits to avoid.
- **`references/purposeful_delight.md`** — when to animate, when not to, and how to keep micro-interactions fast and accessible.
- **`references/optional_media_handling.md`** — embedding screenshots, frame sheets, and SVG placeholders. Explicitly does *not* generate GIFs or stickers (out of scope).

## What it's *not*

- **Not a generic frontend-design skill.** Its purpose is better agent communication through HTML artifacts. Design polish matters but is subordinate to cognition.
- **Not a framework adapter.** No assumptions about React, Vue, Svelte, Tailwind, shadcn/ui, Radix, Framer Motion, GSAP, or any specific design system.
- **Not a media generator.** No GIF search, no sticker generation, no image synthesis. Other skills exist for that.
- **Not a "wrap everything in HTML" skill.** It actively pushes back against using HTML for short answers, code-only responses, and small Markdown tables. Thariq's instinct that you don't always need this is preserved as the skill's anti-trigger logic.

## Eval results

The bundled eval set (`evals/evals.json`) has 18 prompts: 14 positive and 4 negative. In the initial benchmark run with Claude Sonnet, the skill:

- Triggered correctly on all 14 positives (produced self-contained HTML matching the right pattern).
- Declined correctly on all 4 negatives (produced Markdown).
- Passed all structural assertions (semantic HTML, AA contrast, no remote scripts, expected pattern markers, working export buttons).

See `evals/evals.json` for the full prompt set and `references/decision_heuristics.md` for the trigger logic.

## Further reading

- **[Thariq, *HTML Effectiveness*](https://thariqs.github.io/html-effectiveness/)** — the source essay.
- **[Anthropic skill-creator](https://github.com/anthropics/skills/tree/main/skills/skill-creator)** — the progressive-disclosure skill structure this package follows.
- The component vocabulary borrows naming from modern UI systems (shadcn/ui, Radix), but the implementations in `references/reusable_html_primitives.md` are plain HTML/CSS/JS — no framework dependency.

## Contributing

Issues, pull requests, and forks are welcome. The skill is meant to evolve — if you spot a missing pattern, an over-trigger or under-trigger case, a clearer phrasing for the trigger description, or a better worked example, open a PR.

## License

MIT — see [LICENSE](./LICENSE).
