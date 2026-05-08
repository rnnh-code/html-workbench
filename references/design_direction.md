# Design Direction

Pick the direction *before* you start writing CSS. The artifact's job dictates its voice.

Each direction below has: *what it's for*, *typography cues*, *color cues*, *density cues*, *motion cues*, and *what to avoid*.

---

## Technical spec / RFC style

- **For:** implementation plans, RFCs, ADRs, architecture decision records.
- **Tone:** dense but calm. Reads like an engineering doc.
- **Type:** monospace headlines OK; serif body acceptable; 16-17px body; tight but legible line-height (1.5-1.6).
- **Color:** restrained. One accent for status (e.g., severity badges). Mostly neutral.
- **Density:** high. Multiple sections per viewport. Sticky TOC.
- **Motion:** essentially none. Maybe a subtle reveal on `<details>` open.
- **Avoid:** hero images, marketing-style headlines, gradients, decorative icons.

---

## Leadership / executive report style

- **For:** weekly / monthly reports, quarterly summaries, status updates to leadership.
- **Tone:** editorial. Reads like a thoughtful brief.
- **Type:** larger headlines (32-40px), generous line-height (1.6-1.7), serif or humanist sans.
- **Color:** one strong accent for emphasis. Status colors used sparingly.
- **Density:** medium. Executive summary in a callout. Sections clearly labeled. Metric tiles allowed but understated.
- **Motion:** none or one tiny reveal on metric tiles.
- **Avoid:** hype language, overdesigned dashboards, fake metrics, jargon walls.

---

## PR / code review style

- **For:** PR reviews, annotated diffs, codebase tours.
- **Tone:** technical, direct. Severity-aware.
- **Type:** monospace dominant; sans for prose; 14-15px monospace, 16px prose.
- **Color:** diff-aware (added = green tint, removed = red tint), severity badges (blocker / major / minor / nit).
- **Density:** high. Sticky sidebar with file list. Inline comments adjacent to lines.
- **Motion:** minimal. Maybe smooth scroll to anchored line.
- **Avoid:** marketing styling, big hero, unrelated decoration.

---

## Research / explainer style

- **For:** technical explainers, research breakdowns, learning pages.
- **Tone:** patient and instructive. Not condescending.
- **Type:** longer measure (60-75ch), serif body OK for long-form, generous line-height (1.65).
- **Color:** one accent for emphasis. Pull-quote color allowed.
- **Density:** medium. Diagrams interleaved. Glossary accessible.
- **Motion:** none, or a tiny highlight when an annotation is hovered.
- **Avoid:** dashboard styling, kpi tiles, sales energy.

---

## Architecture / diagram style

- **For:** system diagrams, module maps, data-flow drawings.
- **Tone:** technical, visual. Diagram-first.
- **Type:** small clean labels (12-14px), monospace for path/function names.
- **Color:** consistent shape language: rectangle = service, cylinder = datastore, parallelogram = queue. Color by team or layer.
- **Density:** the diagram is the focus; surrounding text supports it.
- **Motion:** none in the diagram itself. Maybe a hover tooltip.
- **Avoid:** rainbow palettes, decorative shadows, inconsistent iconography.

---

## Design exploration style

- **For:** multiple design directions for a single problem.
- **Tone:** confident, comparative.
- **Type:** lets each direction speak for itself; minimal framing chrome.
- **Color:** the directions wear different colors; the framing chrome is neutral.
- **Density:** medium. Each direction gets enough room to feel real.
- **Motion:** subtle hover state to highlight selection.
- **Avoid:** identical-looking directions; placeholder content that hides the real decisions.

---

## Prototype style

- **For:** clickable flows, animation sandboxes, interactive demos.
- **Tone:** playful but controlled. The thing being prototyped should feel real.
- **Type:** matches the prototype's fictional product.
- **Color:** matches the prototype's fictional product.
- **Density:** medium. Controls and content separated by clear scaffolding (panels, side-rail).
- **Motion:** the *point*. But still purposeful.
- **Avoid:** fake content that obscures the design; controls that don't work.

---

## Incident report style

- **For:** postmortems, incident timelines.
- **Tone:** factual, non-blame, severity-aware.
- **Type:** clear hierarchy; UTC timestamps in monospace.
- **Color:** severity colors throughout (info / warn / critical). Otherwise neutral.
- **Density:** medium-high. Timeline is the spine.
- **Motion:** none.
- **Avoid:** dramatic framing, blame language, marketing-style "what we learned" filler.

---

## Slide deck style

- **For:** presentation artifacts, async decks.
- **Tone:** big, sparse, one-idea-per-slide.
- **Type:** display-scale headlines (60-100px), generous tracking, body 24-32px.
- **Color:** high contrast. One or two accents max. Strong dark/light theme.
- **Density:** very low. White space is the design.
- **Motion:** slide transitions allowed, kept fast (≤ 200ms).
- **Avoid:** dense bullets, tiny labels, document-onto-slides.

---

## Custom editor style

- **For:** triage boards, prompt tuners, dataset curation, feature-flag editors.
- **Tone:** functional, calm. Built to be used, not admired.
- **Type:** UI-scale (14-15px) for controls, 16px for content; monospace for code/data.
- **Color:** restrained. State colors clearly distinct (selected, modified, error).
- **Density:** high in the working area, low in the chrome.
- **Motion:** purposeful (drag feedback, copy confirmation, validation). Fast.
- **Avoid:** marketing energy, decorative dashboard styling, controls that look pretty but don't keyboard-work.

---

## Bad default AI design habits to avoid

These show up uninvited. Catch yourself before shipping any of them:

- **Random purple-blue gradients** on hero sections.
- **Glassmorphism / frosted cards** that wash out content.
- **Card-grid SaaS dashboard** styling for things that aren't dashboards.
- **Big hero with the actual content far below.**
- **Lorem ipsum / fake metrics / placeholder logos** that obscure the real decisions.
- **Tiny gray text** for "secondary" information that's actually critical.
- **Emoji used as primary icons** (🚀 ⚡ 💎 next to every section).
- **Decorative-only motion** — animations that don't communicate state.
- **"Insight" cards with no insight** — empty containers labeled "Key takeaway."
- **Excessive rounding and shadows.** 16px radius and three-layer shadow on everything.
- **Generic dark-mode purple** that's neither dark nor purple.
- **Blurry abstract backgrounds.**
- **CTA buttons on artifacts that aren't selling anything.**
- **Accordion-of-everything** that hides the actual content behind clicks.

The artifact should look like an engineer or designer with taste made it for a specific purpose — not like a landing-page builder threw a template at it.
