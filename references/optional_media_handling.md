# Optional Media Handling

Some artifacts benefit from screenshots, image grids, frame sheets, or visual references. This file covers when to include them, how, and where to stop.

This skill **does not** generate, search for, or transform images. Media here is *evidence and illustration* — not the purpose of the artifact.

---

## When to include media

- **Postmortems** — graphs, alerts, screenshots from monitoring dashboards.
- **PR reviews** — before/after UI screenshots when the PR is visual.
- **Design explorations** — reference images that inspired a direction.
- **Reports** — embedded charts or diagrams the user already has.
- **Technical explainers** — diagrams from the source material the explainer is based on.
- **Slide decks** — hero images, key visuals.

If the artifact is essentially text + structure, media probably doesn't belong.

---

## How to include media

**Prefer local files.** If the user provides image paths, embed them with relative paths:

```html
<img src="./screenshots/dashboard-error.png" alt="Dashboard showing 500 error rate spike from 0.1% to 12%">
```

**Inline base64** for self-contained portability when files might move:

```html
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhE…" alt="…">
```

Trade-off: base64 inflates file size by ~33% and is hard to edit. Use it for small, critical visuals (icons, key screenshots) but not for large image grids.

**Use SVG when possible.** Inline `<svg>` themes with the artifact's CSS variables, scales without quality loss, and never breaks when files move.

---

## Image quality

- Always include `alt` text. Decorative images can use `alt=""`.
- Constrain max width with CSS so large images don't break layout.
- Use `loading="lazy"` for images far below the fold.
- Compress before embedding. PNG-quant for screenshots, mozjpeg for photos.
- Consider `srcset` for high-DPI when the image is critical and you have multiple resolutions.

```html
<figure>
  <img src="./alert-graph.png" alt="Error rate graph showing spike at 14:02 UTC" loading="lazy">
  <figcaption>Error rate, 13:50-14:30 UTC</figcaption>
</figure>
```

```css
figure { margin: 24px 0; }
figure img { max-width: 100%; height: auto; border: 1px solid var(--border); border-radius: 6px; }
figcaption { margin-top: 8px; font-size: 14px; color: var(--text-muted); }
```

---

## Why media should not dominate

Three reasons:

1. **Cognitive load.** A page of screenshots is harder to scan than a page of text + select images.
2. **File size.** Big artifacts open slowly and ship awkwardly.
3. **Truth-in-labeling.** If the artifact is mostly images, it's an image grid, not a thinking surface.

Use media to *support* a section, not to *be* the section. Every image should be discussed in the surrounding text.

---

## Why GIF / sticker generation is outside this skill

Several skills exist that specialize in animated media — searching, generating, captioning, sticker-making. **This skill stays out of that lane** for three reasons:

- **Scope discipline.** Adding GIF generation pulls in external APIs, network dependencies, and content moderation considerations that don't belong in a "self-contained HTML artifact" skill.
- **Different success criteria.** A GIF artifact is judged by visual punch and humor; a thinking surface is judged by clarity and decision support. Mixing them produces neither.
- **Self-containment.** The default output is one offline-capable HTML file. GIF search and generation require network calls.

If the user genuinely wants a GIF / sticker artifact, route them to a media-specialized skill or tool. If they want screenshots embedded into a structured document, that's this skill's job.

---

## When images are unavailable

If the artifact would benefit from media but none is provided:

### Option 1: SVG diagrams instead

Build the visual yourself in inline SVG. Architecture diagrams, data flow, state machines, charts — all render well as SVG.

### Option 2: Placeholders with explicit labels

Don't fake a screenshot. Use a labeled placeholder so it's obvious something is missing:

```html
<figure class="placeholder">
  <div class="placeholder-box" role="img" aria-label="Placeholder for dashboard screenshot">
    <span>Dashboard screenshot — not provided</span>
    <span class="hint">If available: paste at this location, alt: "Dashboard at incident peak"</span>
  </div>
</figure>
```

```css
.placeholder-box {
  aspect-ratio: 16 / 9;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 4px;
  background: var(--bg-subtle);
  border: 1px dashed var(--border);
  border-radius: 6px;
  color: var(--text-muted);
  text-align: center;
  padding: 16px;
}
```

This makes the gap visible and acknowledged, rather than secretly absent.

### Option 3: Describe in text

Write a one-sentence description where the image would go: *"Pre-incident graph: error rate flat at ~0.1%. Spike to 12% at 14:02 UTC. Recovery by 14:18."* This is a fine substitute when the image is auxiliary.

---

## Screenshot etiquette

When including screenshots from real systems:

- **Redact sensitive data** — PII, internal user IDs, customer names, tokens, real money figures the user didn't authorize.
- **Crop to the relevant area.** A whole-screen screenshot wastes attention.
- **Annotate** with arrows / circles / callouts when the relevant detail isn't immediately obvious.
- **Caption with date / source.** A graph from "yesterday" becomes meaningless in a week.

---

## Frame sheets

For animation explainers or motion design references, a frame sheet shows key frames side by side.

```html
<figure class="frames">
  <div class="frame"><img src="frame-1.png" alt="Start state"><figcaption>0ms — start</figcaption></div>
  <div class="frame"><img src="frame-2.png" alt="Mid state"><figcaption>120ms — peak</figcaption></div>
  <div class="frame"><img src="frame-3.png" alt="End state"><figcaption>240ms — settled</figcaption></div>
</figure>
```

```css
.frames { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 12px; }
```

If the user gave you a video clip, prefer extracting frames over embedding video — keeps the artifact self-contained and printable.

---

## Image grids

For design references, mood boards, or visual research:

```html
<div class="image-grid">
  <figure><img src="./ref-1.jpg" alt="Editorial layout reference"><figcaption>Source: …</figcaption></figure>
  <figure><img src="./ref-2.jpg" alt="Density reference"><figcaption>Source: …</figcaption></figure>
</div>
```

Always include source attribution where the user has it.

---

## Self-test

- Does each image earn its place by clarifying something the surrounding text can't?
- Does every image have meaningful `alt` text?
- Did you redact anything sensitive?
- Did you avoid faking screenshots that don't exist?
- Is the artifact still useful if a few images fail to load?

If you can't answer "yes" to all five, reconsider the media — or omit it.
