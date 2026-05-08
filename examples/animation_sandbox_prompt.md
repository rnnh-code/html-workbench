# Example: Animation sandbox

## User request

> I'm tuning the entrance animation on our hero card — duration, easing, and starting offset. Build me a sandbox where I can play with the values and copy the final CSS.

## Why the skill should trigger

Motion *cannot be described in Markdown*. The user has to feel it. They also need to iterate quickly — slide a value, see the result. HTML with sliders + live preview + live CSS output is the right surface.

## HTML capability categories

- **Interaction** — sliders, selects, buttons.
- **Code** — live CSS / JS preview that updates with parameters.
- **Design** — the actual animated element, rendered.
- **Workflows** — replay, reset, copy.

## Recommended pattern

Animation sandbox (`html_artifact_patterns.md` §8).

## Expected output structure

- Header: title + one-line purpose ("Tune entrance for `.hero-card`. Copy CSS when done.").
- Big preview area centered. Replay button.
- Controls panel: sliders (duration ms, delay ms, offset px), selects (easing), color pickers if relevant. Each labeled with units.
- Live code preview: CSS keyframes / transition that updates as parameters change.
- Reset to default.
- Reduced-motion mode toggle so the user sees the static fallback.

## Expected interactions

- Live update: changing any control reflects immediately in preview and code.
- Replay: re-trigger the animation.
- Reset: snap all controls back to provided defaults.
- Reduced-motion toggle: simulate `prefers-reduced-motion: reduce`.

## Expected export

- Copy current CSS (the keyframes / transition with the user's values inlined).
- Copy current parameters as JSON.

## Common failure modes

- **Preview too small.** The user can't feel the motion.
- **Parameters without units.** "Duration: 200" is ambiguous (ms? frames?).
- **No reset.** Users tune destructively; reset gives them confidence to explore.
- **No reduced-motion fallback.** Animation that breaks for ~10% of users.
- **Decorative animation in the *chrome* of the sandbox** — animated buttons, sliding panels — that fights with the animation under tuning.
- **Exporting outdated values.** What gets copied must match the current preview, not a snapshot from 3 changes ago.
