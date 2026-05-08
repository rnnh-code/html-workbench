# Reusable HTML Primitives

Plain HTML / CSS / JS building blocks. No frameworks, no CDN, no npm. Each primitive lists *when to use*, *when not to use*, *accessibility notes*, and *common implementation mistakes*.

The goal is to give the agent a familiar component vocabulary (cards, badges, tabs, accordions, callouts, etc.) without requiring a design system.

---

## Card

**When.** Group related content. Lists of items. Comparable units.

**When not.** Single-item displays. When the visual frame distracts from content.

```html
<article class="card">
  <header class="card-head"><h3>Title</h3><span class="badge">v1.2</span></header>
  <div class="card-body">…</div>
  <footer class="card-foot">…</footer>
</article>
```

```css
.card { border: 1px solid var(--border); border-radius: 8px; background: var(--bg); }
.card-head, .card-foot { padding: 12px 16px; }
.card-head { border-bottom: 1px solid var(--border); display: flex; justify-content: space-between; align-items: baseline; }
.card-body { padding: 16px; }
.card-foot { border-top: 1px solid var(--border); }
```

**Accessibility.** `<article>` is appropriate when the card is independently meaningful; `<section>` if it's part of a labeled group; plain `<div>` if it's purely visual. Don't put a card-wide click handler that obscures keyboard targets — make the primary action a real `<button>` or `<a>`.

**Common mistakes.** Three-layer drop-shadow nesting. 20px radius "for warmth." Click-anywhere cards that aren't keyboard-accessible.

---

## Table

**When.** Dense comparison. Sorted / filterable lists. Anything with > 6 rows × > 3 cols.

**When not.** Layout. Fewer than ~5 rows of homogeneous data (a list reads better).

```html
<table class="data-table">
  <thead><tr><th>Field</th><th>Type</th><th>Default</th></tr></thead>
  <tbody>
    <tr><td>name</td><td>string</td><td>—</td></tr>
  </tbody>
</table>
```

```css
.data-table { border-collapse: collapse; width: 100%; font-variant-numeric: tabular-nums; }
.data-table th, .data-table td { text-align: left; padding: 8px 12px; border-bottom: 1px solid var(--border); }
.data-table th { background: var(--bg-subtle); font-weight: 600; position: sticky; top: 0; }
.data-table tbody tr:hover { background: var(--bg-subtle); }
```

**Accessibility.** Use `<th scope="col">` for headers. Add a `<caption>` if the table has a title.

**Common mistakes.** Right-aligned text columns. Left-aligned number columns. Headers that don't stick on tall tables.

---

## Badge

**When.** Status, severity, type, count, version. Small bits of metadata.

**When not.** Long labels. Things that should be sentences.

```html
<span class="badge badge--success">Done</span>
<span class="badge badge--warn">Pending</span>
<span class="badge badge--error">Failed</span>
```

```css
.badge { display: inline-block; padding: 2px 8px; border-radius: 999px; font-size: 12px; font-weight: 500; line-height: 1.4; }
.badge--success { background: var(--success-bg); color: var(--success); }
.badge--warn { background: var(--warning-bg); color: var(--warning); }
.badge--error { background: var(--error-bg); color: var(--error); }
```

**Accessibility.** Pair color with text — never color alone. If a badge has only an icon, give it `aria-label`.

**Common mistakes.** Using badges as primary actions. Stacking 5+ badges and losing scannability.

---

## Tabs

**When.** Switching between related views in the same context (e.g., overview / details / history of one entity).

**When not.** Hiding content the user needs to see at the same time.

```html
<div class="tabs" role="tablist">
  <button role="tab" aria-selected="true" aria-controls="p1" id="t1">Overview</button>
  <button role="tab" aria-selected="false" aria-controls="p2" id="t2">Details</button>
</div>
<section role="tabpanel" id="p1" aria-labelledby="t1">…</section>
<section role="tabpanel" id="p2" aria-labelledby="t2" hidden>…</section>
```

JS handles tab → panel toggle and arrow-key nav.

**Accessibility.** Use ARIA tab pattern. Arrow-key navigation between tabs. Activate on focus *or* on click — pick one and document.

**Common mistakes.** Hiding panels with `display: none` and forgetting to restore focus. Not handling Home/End to jump to first/last tab.

---

## Accordion / `<details>`

**When.** Progressive disclosure. Long Q&A. Optional sections.

**When not.** Critical content. The user shouldn't have to click to find what they came for.

```html
<details>
  <summary>Why does this happen?</summary>
  <p>Because the cache invalidates on every write…</p>
</details>
```

`<details>` is native, accessible, keyboard-friendly, and works with no JS. Prefer it over a custom accordion.

**Common mistakes.** Hiding the *primary* content behind clicks. Custom accordions that don't work with keyboard.

---

## Callout / alert

**When.** Inline warnings, assumptions, risks, decisions, info notes. Things the reader must notice without leaving the flow.

```html
<aside class="callout callout--warn">
  <strong>Heads up.</strong> This migration touches production data.
</aside>
```

```css
.callout { padding: 12px 16px; border-left: 4px solid var(--info); background: var(--info-bg); border-radius: 6px; }
.callout--warn { border-color: var(--warning); background: var(--warning-bg); }
.callout--error { border-color: var(--error); background: var(--error-bg); }
.callout--success { border-color: var(--success); background: var(--success-bg); }
```

**Accessibility.** Use `<aside>` for tangential, `role="alert"` for things screen readers should announce immediately (rare). Pair color with a label like "Heads up." or an icon.

**Common mistakes.** Three callouts in a row, all the same severity. Critical info buried in a callout instead of in the main flow.

---

## Timeline

**When.** Incidents, plans, history, sequence-of-events.

**When not.** Items without inherent order.

```html
<ol class="timeline">
  <li><time>14:02 UTC</time><h4>First alert fired</h4><p>…</p></li>
  <li><time>14:05 UTC</time><h4>Oncall paged</h4><p>…</p></li>
</ol>
```

Style as a vertical line with markers (use a CSS pseudo-element). Use monospace `<time>` for timestamps.

**Accessibility.** Use `<ol>` for ordered events. `<time datetime="...">` for machine-readable timestamps.

**Common mistakes.** Inconsistent timezones (some UTC, some local). No event description, just timestamps.

---

## Stepper / progress indicator

**When.** Multi-step workflows where the user needs to know where they are.

```html
<ol class="stepper">
  <li class="is-done">Plan</li>
  <li class="is-current" aria-current="step">Build</li>
  <li>Verify</li>
  <li>Ship</li>
</ol>
```

**Accessibility.** `aria-current="step"` on the active step. Use `<ol>` for ordered.

**Common mistakes.** No "current" indicator. No way to jump to a different step (or a forced linear flow when navigation should be flexible).

---

## Sticky nav / TOC

**When.** Long documents (> 1 viewport-height). The user needs to jump.

```html
<nav class="toc" aria-label="Sections">
  <ul>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#architecture">Architecture</a></li>
    …
  </ul>
</nav>
```

```css
.toc { position: sticky; top: 16px; max-height: calc(100vh - 32px); overflow-y: auto; }
```

**Accessibility.** Use `<nav>` with `aria-label`. Highlight the current section as the user scrolls (IntersectionObserver).

**Common mistakes.** TOC that obscures content on small screens. No active-section highlight.

---

## Code block (with optional copy)

**When.** Any code snippet, command, or path.

```html
<pre class="code"><code>git rebase --onto main origin/main</code>
  <button class="code-copy" data-copy-target="this">Copy</button>
</pre>
```

```css
.code { position: relative; background: var(--bg-subtle); padding: 12px 16px; border-radius: 6px; overflow-x: auto; font-family: ui-monospace, SFMono-Regular, monospace; font-size: 14px; line-height: 1.6; }
.code-copy { position: absolute; top: 8px; right: 8px; }
```

**Accessibility.** Code is real text — don't put it in `<img>` or screenshot it.

**Common mistakes.** Removing line breaks. Tiny code (< 13px). No copy button on long blocks.

---

## Annotated code

**When.** Walking through code in a technical explainer or PR review.

```html
<div class="annotated">
  <pre class="code"><code>const x = 1;<span class="annot" data-id="a">  // mark</span></code></pre>
  <aside class="annot-note" data-for="a">This is the mark we discuss in §3.</aside>
</div>
```

JS links annotation hover ↔ note highlight.

**Common mistakes.** Annotations that don't link visually to the code they describe. Tiny annotation markers.

---

## SVG diagram

**When.** Architecture, data flow, state machine, pipeline. Anything spatial.

Inline `<svg>` directly in the HTML so it themes from CSS variables.

```html
<svg viewBox="0 0 400 200" role="img" aria-labelledby="diagram-title">
  <title id="diagram-title">Request lifecycle</title>
  <rect x="20" y="20" width="120" height="60" fill="var(--bg-subtle)" stroke="var(--border)" />
  <text x="80" y="55" text-anchor="middle">Client</text>
  <!-- … -->
</svg>
```

**Accessibility.** Provide `<title>` (and `<desc>` for complex diagrams). Use `role="img"` with `aria-labelledby`.

**Common mistakes.** Hardcoded colors that break theming. No legend. Inconsistent shape language.

---

## Form

```html
<form>
  <div class="field">
    <label for="email">Email</label>
    <input id="email" name="email" type="email" required>
    <p class="hint">We'll send a verification link.</p>
  </div>
</form>
```

**Accessibility.** Real `<label>` with matching `for`/`id`. Inline error messages near the field. `aria-invalid` on errored inputs.

**Common mistakes.** Placeholder-only labels. Validation messages far from the field. No required-field indicator.

---

## Slider

```html
<label for="duration">Duration <output for="duration">200</output>ms</label>
<input id="duration" type="range" min="50" max="800" step="10" value="200" oninput="this.previousElementSibling.querySelector('output').value = this.value">
```

**Accessibility.** Always show the current value (with units). Allow keyboard arrows. Label with units.

**Common mistakes.** No visible value. No units. Step too small / too large for the use case.

---

## Toggle

```html
<label class="toggle">
  <input type="checkbox" role="switch">
  <span>Enable feature flag</span>
</label>
```

**Accessibility.** Real `<input type="checkbox">` underneath. Don't reinvent.

**Common mistakes.** Custom toggle with no underlying input — breaks form serialization, screen readers, keyboard.

---

## Search / filter input

```html
<label for="filter" class="sr-only">Filter</label>
<input id="filter" type="search" placeholder="Filter by title…">
```

JS filters list items as the user types. Debounce if list is large.

**Common mistakes.** Filtering only by exact match (no substring). No "X of Y matched" indicator.

---

## Drag-drop board

Use the HTML5 drag-and-drop API. Support keyboard reorder for accessibility.

```html
<ol class="board-col" data-col="p0">
  <li class="card" draggable="true" tabindex="0">Card A</li>
  <li class="card" draggable="true" tabindex="0">Card B</li>
</ol>
```

**Accessibility.** Drag-drop is hard to make accessible. Provide a fallback: keyboard "move up / move down" buttons or a `<select>` to change column.

**Common mistakes.** Mouse-only interaction. No drop indicator. State not preserved for export.

---

## Copy / download buttons

See `export_patterns.md` for the full universal copy + download helpers. Wire every export-bearing artifact to them.

```html
<button data-copy-target="#prompt">Copy prompt</button>
<button id="download-json">Download JSON</button>
```

**Accessibility.** Visible label (not just an icon). `aria-live="polite"` on confirmation.

---

## Legend

**When.** Any chart or diagram with multiple series / shape types.

```html
<ul class="legend" aria-label="Legend">
  <li><span class="swatch" style="background: var(--success)"></span> Healthy</li>
  <li><span class="swatch" style="background: var(--warning)"></span> Degraded</li>
</ul>
```

**Common mistakes.** Legend far from the chart. Legend that doesn't match the actual colors used.

---

## Comparison matrix

A `<table>` with rows = options, columns = criteria, cells = scores or checkmarks. Highlight the best score per row or column.

**Common mistakes.** No clear winner indicator. Equal weight given to all criteria.

---

## Checklist

```html
<ul class="checklist">
  <li><input type="checkbox" id="c1"><label for="c1">Migrate database</label></li>
  <li><input type="checkbox" id="c2"><label for="c2">Update DNS</label></li>
</ul>
```

Wire to localStorage if persistence is useful.

**Common mistakes.** Checkbox without `<label>` so click area is tiny. State lost on refresh when persistence would help.

---

## Sticky header / footer

Use `position: sticky` (not fixed) so the header scrolls with the natural document flow until pinned.

```css
.app-header { position: sticky; top: 0; background: var(--bg); border-bottom: 1px solid var(--border); z-index: 10; }
```

**Common mistakes.** `position: fixed` with no spacer above the content (covers the first paragraph). z-index issues with dropdowns.

---

## What this file is *not*

This is a vocabulary, not a design system. There's no shared CSS reset, no component library, no JS framework. Every artifact is self-contained and inlines exactly what it needs.

If you find yourself writing the same 200 lines of CSS across many artifacts, that's a sign you might want a project-specific stylesheet — but for one-off artifacts, redundancy is fine.
