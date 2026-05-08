# Purposeful Delight

Delight is *seasoning*, not the meal. Good micro-interactions reduce confusion and confirm action. Bad ones waste time and dilute trust.

The test for any animation or playful touch: **does removing it make the artifact harder to use?** If no, remove it.

---

## Where delight pulls its weight

- **Copy / export confirmations.** "Copied!" pill that fades after 1.5s. Tells the user the action worked.
- **Drag / drop feedback.** Drop target highlights as the dragged item enters. Original position fades.
- **Hover / focus states.** A subtle 80-150ms transition between resting and hovered helps the user feel where they are.
- **Empty states.** A small illustrated cue (SVG, monoline) helps an empty container feel intentional rather than broken.
- **Success states.** A check icon that scales in over 200ms after a save.
- **Selection feedback.** Ring or border that animates in when the user picks something.
- **Tiny transitions on state change.** Tab switching, accordion open/close, modal in/out. ≤ 200ms.
- **Preview updates.** When a slider moves, the preview updates instantly with no jank.
- **Onboarding hints.** A pulse on the export button the first time the user reaches a milestone.

---

## Where delight backfires

- **Loading shimmers** that last longer than the actual load.
- **Hero animations** that delay the actual content.
- **Confetti / celebrations** in serious tools (PR reviews, incident reports, financial dashboards).
- **Bounce / spring easing** on data updates — makes precise reading harder.
- **Animations longer than 300ms** for routine interactions.
- **Auto-playing animations** that the user didn't trigger.
- **Hover-only interactions** that mobile users can't reach.
- **Pulsing CTAs** that scream for attention in a calm artifact.
- **Sound effects.** Almost always wrong.

---

## Reduced motion

Always honor the user's system preference:

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

Provide static fallbacks for any motion that *carries information*. If a slide's content depends on an entrance animation to be readable, the static fallback should still be readable.

---

## Timing and easing

| Purpose | Duration | Easing |
|---|---|---|
| Hover / focus highlight | 80-150ms | `ease-out` |
| Button press feedback | 80-120ms | `ease-out` |
| Tab / accordion change | 150-250ms | `ease-in-out` |
| Modal in | 200-250ms | `ease-out` |
| Modal out | 150-200ms | `ease-in` |
| Confirmation pill | 1500ms total visible, fade in 150ms / hold 1.2s / fade out 150ms | linear |
| Reorder / drop animation | 200-250ms | `ease-out` |
| Page-level transition | 250-350ms | `ease-in-out` |
| Decorative entrance (rare) | ≤ 400ms | `ease-out` |

> 400ms feels slow. < 80ms feels invisible. Aim for the middle.

---

## Serious vs. playful tone

| Artifact | Tone | Delight budget |
|---|---|---|
| Implementation plan | Serious | Minimal — copy confirmations, hover states |
| PR review | Serious | Minimal — anchor scrolling, severity hover |
| Incident report | Serious | None decorative; only state-change transitions |
| Weekly report | Semi-serious | Metric tile reveal, copy confirmation |
| Slide deck | Performative | Slide transitions ≤ 200ms |
| Custom editor | Functional | Drag feedback, validation animations, success states |
| Prototype | Playful (controlled) | Whatever serves the prototype |
| Animation sandbox | Playful | The animation *is* the point |
| Design exploration | Confident | Hover reveal, selection feedback |

When in doubt, less.

---

## Common micro-interaction patterns

### Copy confirmation

```html
<button class="btn-copy" data-copy="hello world">
  Copy
  <span class="copied-pill" aria-live="polite">Copied!</span>
</button>

<style>
  .btn-copy { position: relative; }
  .copied-pill {
    position: absolute;
    top: -28px;
    left: 50%;
    transform: translateX(-50%) translateY(4px);
    padding: 4px 10px;
    background: var(--success);
    color: white;
    border-radius: 6px;
    font-size: 12px;
    opacity: 0;
    pointer-events: none;
    transition: opacity 150ms ease-out, transform 150ms ease-out;
  }
  .btn-copy.is-copied .copied-pill {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }
</style>
```

### Drop-target highlight

```css
.drop-zone { transition: background-color 100ms, border-color 100ms; }
.drop-zone.is-over {
  background-color: var(--accent-bg);
  border-color: var(--accent);
}
```

### Validation shake (use sparingly)

Only for clearly erroneous user input the user must fix.

```css
@keyframes shake {
  0%, 100% { transform: translateX(0); }
  25% { transform: translateX(-4px); }
  75% { transform: translateX(4px); }
}
.input.is-invalid { animation: shake 200ms ease-out; border-color: var(--error); }
@media (prefers-reduced-motion: reduce) {
  .input.is-invalid { animation: none; }
}
```

### Tab switch

```css
.tab-content { transition: opacity 150ms ease-out; }
.tab-content[hidden] { display: none; }
```

Don't slide tab content horizontally — it's distracting and rarely informative.

---

## When NOT to animate

- The user didn't trigger anything (no spontaneous animation).
- The motion would obscure data the user is reading (no animating chart values into existence on every render).
- The artifact is being printed, screenshotted, or read with a screen reader.
- The motion would compete for attention with another, more important animation.
- The user has `prefers-reduced-motion: reduce`.
- You're using motion to make a weak design feel "alive." Fix the design instead.

---

## Self-test for every animation

Before shipping any animated element, answer:

1. What does it communicate that wasn't already clear?
2. Could a static design carry the same information?
3. Will it still be tolerable on the 50th use?
4. Does it work with reduced motion?
5. Is it ≤ 300ms unless the user deliberately asked for something longer?
6. Does it serve the user's task, or did I add it because the artifact felt empty?

If any answer is "no" or "I don't know" — cut it.
