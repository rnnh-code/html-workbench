# Color Strategy

Color is a system, not a decoration. Use it to encode meaning, signal hierarchy, and aid wayfinding — never to "make it pop."

---

## Use CSS variables for tokens

Always. Inline `style="color: #3a7bd5"` is a smell.

```css
:root {
  /* Neutrals — used for text, surfaces, borders */
  --bg:           #ffffff;
  --bg-subtle:    #f6f7f9;
  --bg-muted:     #ecedef;
  --border:       #d8dade;
  --text:         #1a1d23;
  --text-muted:   #5a6068;
  --text-subtle:  #7d8390;

  /* Brand / accent */
  --accent:       #2563eb;
  --accent-hover: #1e4fc4;
  --accent-bg:    #eff5ff;

  /* Status — semantic */
  --success:      #16804f;
  --success-bg:   #e8f5ee;
  --warning:      #b45309;
  --warning-bg:   #fdf2dc;
  --error:        #b42318;
  --error-bg:     #fdecea;
  --info:         #1d4ed8;
  --info-bg:      #eff5ff;
}
```

Use them everywhere. Refactor to add a token rather than hard-coding a one-off.

---

## Semantic colors

Reserve specific hues for specific meanings, and *use them consistently*:

| Meaning | Color family | Pair with |
|---|---|---|
| Success | green | check icon, "Success" / "Done" text |
| Warning | amber / orange | exclamation icon, "Warning" / "Heads up" text |
| Error | red | x icon, "Error" / "Failed" text |
| Info | blue | info icon, "Note" text |
| Selected | accent | check icon or filled state |
| Disabled | muted neutral | reduced opacity, no icon needed |
| Changed | distinct accent | "modified" badge, dot indicator |
| Risky | red-orange | warning icon, severity label |

If green means success on page 1 and "team A" on page 2, you've broken the system.

---

## Neutral palette

The dominant color in any artifact should be neutral.

A working neutral ramp:

```
#ffffff  → background
#f6f7f9  → subtle surface (cards, sidebar)
#ecedef  → muted surface (hover, secondary cards)
#d8dade  → border
#a6abb4  → divider, disabled foreground
#7d8390  → subtle text
#5a6068  → muted text
#1a1d23  → primary text
```

Pick *one* neutral ramp and stick with it. Mixing warm grays and cool grays in the same artifact looks careless.

---

## Accent colors

- **2-4 accents max** beyond neutrals.
- One **brand accent** for primary actions and identity.
- Up to four **status accents** (success / warning / error / info).
- Optional **categorical accents** if the data is genuinely categorical (charts, multi-team boards). Use a colorblind-safe palette like Okabe-Ito.

Don't add accents because something feels visually empty. Add whitespace instead.

---

## 60 / 30 / 10 balance

- **60%** dominant (usually neutral background and text).
- **30%** supporting (cards, secondary surfaces, secondary text, structural color).
- **10%** accent (CTAs, selected states, status, charts).

This isn't a literal pixel ratio — it's the *visual weight* the eye perceives. If the accent fills more than ~10% of the visible canvas, it stops being an accent.

---

## Contrast

WCAG AA minimum:

- **4.5:1** for body text (any text under 18pt regular or 14pt bold).
- **3:1** for large text and meaningful UI elements.
- **3:1** for non-text content like icons and chart elements.

Validate critical pairs:

| Foreground | Background | Required |
|---|---|---|
| Body text | Page background | 4.5:1 |
| Body text | Card background | 4.5:1 |
| Muted text | Card background | 4.5:1 if it's still readable text |
| Button text | Button fill | 4.5:1 |
| Focus outline | Background | 3:1 |
| Link | Body background | 4.5:1, distinguishable from body text |

Test in a contrast checker, not by eye. Designers' eyes have biases.

---

## Metric direction: color by *favorability*, not direction

The default mental model is *up = green = good*. That's wrong for half the metrics in a real dashboard or weekly report.

| Metric family | Up means | Color signal |
|---|---|---|
| Revenue, signups, retention, conversion | Better | Green up-arrow |
| Latency, error rate, p95, time-to-X | **Worse** | Red up-arrow (or green down-arrow) |
| Churn, unsubscribes, refunds, cost | **Worse** | Red up-arrow |
| Inventory, queue depth, backlog | Context-dependent | Don't use direction-based color alone |

Code your delta tiles by *improved / regressed / flat*, not *up / down*. The arrow tells the user *which way the number moved*; the *color* tells them *whether that's good*. If you encode both with the arrow color, a leadership reader who scans for green will misread a latency improvement as a regression.

Implementation: pass each metric tile a `favorability` flag, not a direction:

```js
function metricColor(delta, lowerIsBetter) {
  if (delta === 0) return 'var(--text-muted)';
  const improved = lowerIsBetter ? delta < 0 : delta > 0;
  return improved ? 'var(--success)' : 'var(--error)';
}
```

Always pair the color with a label ("improved" / "regressed") and the absolute delta. Color alone is the wrong primary signal for non-glanceable metrics.

## Color-blind safety

~8% of men have a form of color-vision deficiency. Always pair color with a redundant cue:

- **Status badges:** color + label + icon.
- **Chart series:** color + shape (markers) + position.
- **Diff:** color + `+`/`-` prefix.
- **Required field:** color + asterisk + "(required)".

If you removed all the color and the artifact still worked, you're doing it right.

For categorical data, prefer Okabe-Ito or similar colorblind-safe palettes. Avoid pure red/green pairs as the only signal.

---

## Avoiding color chaos

Common failure modes:

- **Rainbow charts** with 7+ series. Group, summarize, or break into multiple charts instead.
- **One-off colors** introduced for a single element. Add a token or reuse an existing one.
- **Inconsistent meaning** — green is success on one page, "team B" on another.
- **Two reds, two greens** (e.g., `#dc2626` and `#ef4444`) in the same artifact. Pick one of each.
- **Color used for decoration** (random colored borders to "warm it up"). Use whitespace and typography instead.

---

## Avoiding generic gradients

Plain AI-generated UI ships with:

- The default purple-blue gradient (`#667eea → #764ba2`).
- Glassmorphism cards on a blurry abstract background.
- Conic-gradient hero blobs.

Don't use these unless the brief explicitly calls for them. They're a tell that the design has no point of view.

If you must use a gradient, make it serve a specific purpose:
- A hero section where the brand is gradient-based.
- A chart fill from low to high.
- A subtle surface differentiation (very low contrast).

Otherwise: solid colors.

---

## Editorial vs. functional palettes

**Editorial** (reports, explainers, decks): warmer neutrals (slight ochre or beige tint), a single saturated accent, generous whitespace, larger type. Feels like a magazine.

**Functional** (editors, dashboards, sandboxes): cool neutrals, neutral accent, dense layout, smaller type. Feels like a tool.

Pick one early. Mixing them produces a "design-y dashboard" that's hard to use and unconvincing as editorial.

---

## Dark mode

If you support dark mode:

- Don't just invert. Adjust each token by hand.
- Reduce saturation on accents in dark mode (saturated colors look harsher on dark).
- Lift the lowest-level surface above pure black (`#0e1014` is friendlier than `#000`).
- Test contrast separately — pairs that pass in light mode often fail in dark.

```css
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #0e1014;
    --bg-subtle: #15181d;
    --bg-muted: #1d2128;
    --border: #2a2f38;
    --text: #ebecef;
    --text-muted: #a6abb4;
    --text-subtle: #7d8390;
    --accent: #5a8eff;
    /* ... */
  }
}
```

---

## Quick self-check

- Are all colors coming from tokens?
- Are status colors used consistently across the artifact?
- Could a colorblind reader still understand every state?
- Does the accent take up no more than ~10% of the visible canvas?
- Is there exactly one neutral ramp?
- Did you accidentally ship the default purple-blue gradient?
