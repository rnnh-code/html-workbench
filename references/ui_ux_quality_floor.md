# UI / UX Quality Floor

A practical checklist. Hit every applicable item before the artifact is "done."

This isn't aspirational design polish — it's the *floor*. Below this, the artifact is broken even if the content is good.

---

## Information architecture

- [ ] Title at the top, one-line purpose immediately below.
- [ ] Most important content above the fold (no decorative hero pushing it down).
- [ ] Logical reading order top-to-bottom; no zigzagging.
- [ ] Sections labeled with `<h2>` / `<h3>` so the user can scan.
- [ ] If the artifact is long (> 1 viewport-height of content), include a sticky TOC or section nav.
- [ ] Related controls grouped, separated from unrelated controls by whitespace or borders.
- [ ] Progressive disclosure for non-essential detail (`<details>`, tabs, accordions).

## Typography

- [ ] Body text ≥ 16px.
- [ ] Line-height ≥ 1.5 for body, ≥ 1.2 for headings.
- [ ] Max content width ≤ 75ch for prose; tables and dashboards can be wider.
- [ ] No more than two font families.
- [ ] Type hierarchy is obvious at a glance (size, weight, color).
- [ ] System font stack by default (`-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif`) unless brief calls for a specific font.
- [ ] Numerals are tabular when used in tables (`font-variant-numeric: tabular-nums`).

## Spacing

- [ ] Spacing scale is consistent (e.g., 4 / 8 / 12 / 16 / 24 / 32 / 48 / 64).
- [ ] No arbitrary one-off values like `padding: 13px`.
- [ ] Rhythm is even between sections.
- [ ] Cards / list items have breathable inner padding (≥ 12px).

## Visual hierarchy

- [ ] One obvious primary action per section.
- [ ] Visual weight (size / contrast / color) matches importance.
- [ ] Decorative elements never outweigh content.
- [ ] No more than three levels of headline hierarchy on a single screen.

## Contrast

- [ ] WCAG AA: 4.5:1 for body text, 3:1 for UI elements and large text.
- [ ] Test in both light and dark backgrounds if you support them.
- [ ] No gray text below `#666` on white.
- [ ] Link color distinguishable from body text without relying on hover.

## Responsiveness

- [ ] Renders cleanly at 360px wide.
- [ ] Renders cleanly at 1440px wide.
- [ ] No horizontal scroll on mobile (unless intentionally spatial: kanban, canvas).
- [ ] Text reflows; controls stack; tables scroll within their container, not the page.
- [ ] Use `meta name="viewport" content="width=device-width, initial-scale=1"`.

## Accessibility

- [ ] Every interactive element is reachable by keyboard.
- [ ] Visible focus state on every interactive element.
- [ ] Form inputs have `<label>` (not just placeholder).
- [ ] Buttons that aren't text have `aria-label`.
- [ ] Images have `alt` (decorative images have `alt=""`).
- [ ] Heading levels don't skip (no `<h1>` → `<h3>` jump).
- [ ] Color is never the only carrier of meaning.
- [ ] `prefers-reduced-motion` respected if you animate.

## Forms

- [ ] Labels above or beside inputs (not placeholder-only).
- [ ] Required fields marked clearly.
- [ ] Validation messages near the field they apply to.
- [ ] Error / success / warning states visually distinct.
- [ ] Help text where the format isn't obvious.
- [ ] Group related fields with `<fieldset>` / `<legend>`.

## Interaction states

- [ ] Default, hover, focus, active, disabled — all distinguishable.
- [ ] Loading state for any async action.
- [ ] Empty state for any list / table that can be empty.
- [ ] Confirmation for destructive actions.

## Focus states

- [ ] `:focus-visible` styled (not removed).
- [ ] Outline color contrasts with both the element and the background.
- [ ] Focus order matches visual order.

## Keyboard

- [ ] Tab moves through controls.
- [ ] Enter activates buttons / links.
- [ ] Space activates buttons.
- [ ] Esc closes modals / dropdowns.
- [ ] Arrow keys navigate lists where appropriate (slides, kanban).
- [ ] Document keyboard shortcuts in the UI when not obvious.

## Touch

- [ ] Tap targets ≥ 40px × 40px.
- [ ] Adequate spacing between targets.
- [ ] No hover-only interactions; use click/tap as the primary signal.

## Animation

- [ ] Durations 100-300ms for UI feedback.
- [ ] Easing matches purpose (`ease-out` for entrances, `ease-in` for exits, `ease-in-out` for state changes).
- [ ] Honors `prefers-reduced-motion: reduce` (provide static alternative).
- [ ] No animations longer than 500ms unless the user triggered them deliberately.

## Charts

- [ ] Axes labeled with units.
- [ ] Legend present when there are multiple series.
- [ ] Color choices accessible.
- [ ] Data source noted (date range, sample size).
- [ ] Empty / no-data state.

## Diagrams

- [ ] Title.
- [ ] Legend explaining shapes and colors.
- [ ] Consistent shape language (e.g., rectangle = service, cylinder = datastore).
- [ ] Arrows have direction.
- [ ] Labels readable at the size shown.
- [ ] Source noted if the diagram is derived from real code.

## Code display

- [ ] Monospace font.
- [ ] Background distinguishable from prose.
- [ ] Syntax highlighting if code is more than ~10 lines.
- [ ] Long lines wrap or scroll; never overflow the page.
- [ ] Line numbers when discussing specific lines.
- [ ] Copy button on code blocks longer than ~3 lines.

## Tables

- [ ] Header row visually distinct.
- [ ] Sticky header if the table is taller than the viewport.
- [ ] Numbers right-aligned.
- [ ] Text left-aligned.
- [ ] Zebra-striping or row borders for readability.
- [ ] Sortable when more than ~10 rows and sort makes sense.
- [ ] Filterable / searchable when more than ~25 rows.

## Mobile-specific

- [ ] No fixed-width containers larger than the viewport.
- [ ] Buttons full-width on small screens when they're primary actions.
- [ ] Modals don't crop content on small screens.
- [ ] Don't assume hover.

## Print / share

- [ ] `@media print` stylesheet hides nav and shows content cleanly.
- [ ] Page breaks land in sensible places (`page-break-inside: avoid` for cards / tables).
- [ ] Background colors and shadows print correctly or are dropped intentionally.

## Empty states

- [ ] Explain why the area is empty.
- [ ] Suggest what to do next.
- [ ] No "0 results" with no other text.

## Error states

- [ ] Error message says *what* went wrong and *how to fix it*.
- [ ] Don't blame the user.
- [ ] Recoverable: provide a retry / reset.

## Copy / export

- [ ] Button is visible (not hidden behind hover).
- [ ] Confirmation appears for at least 1.5s after click.
- [ ] What gets copied matches what's on screen.
- [ ] Format options (Markdown / JSON / plain) where useful.
- [ ] Failure is communicated (e.g., clipboard permission denied).

---

## Quick self-test

If you can answer "yes" to all of these, the artifact has cleared the floor:

1. Can a stranger tell what this is for in 5 seconds?
2. Can they read the body text without zooming?
3. Can they navigate without a mouse?
4. Does the most important content come before any decoration?
5. If they edit / sort / tune something, can they get it out?
6. Does it still work without JavaScript? (Graceful degradation, not parity.)
7. Does it look intentional, not generic?
