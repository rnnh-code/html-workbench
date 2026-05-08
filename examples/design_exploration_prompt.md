# Example: Design exploration

## User request

> Show me 4 different design directions for an empty state when a user has no projects yet. Help me pick one.

## Why the skill should trigger

The user wants to *see* and *compare* options. Markdown could describe four directions in prose, but the user's brain compares visuals far better than verbal descriptions of visuals. HTML lets us render four directions live, side by side, with explicit tradeoffs.

## HTML capability categories

- **Design** — typography, color, spacing, components.
- **Spatial layouts** — four directions visible at once.
- **Tables** — comparison matrix across axes (tone, density, contrast, illustration style).
- **Interaction** — toggle dark mode, "mark as favorite" on each direction.
- **Images** — illustration placeholders or reference imagery if provided.

## Recommended pattern

Design exploration (`html_artifact_patterns.md` §5).

## Expected output structure

- Brief: the design problem, one paragraph (audience, intent, constraints).
- Four labeled directions, each a real rendered card with: name, hero, the actual empty-state UI, and a short rationale.
- Side-by-side comparison row across axes: tone (warm / clinical), density (sparse / dense), illustration (none / icon / scene), CTA prominence.
- Recommendation: one direction picked, with reasoning grounded in the audience and intent.

## Expected interactions

- Toggle dark / light mode on the whole page.
- Resize each direction inline (mobile / tablet / desktop) to see how it adapts.
- "Pick this one" button on each direction. Clicking it fills the export with that direction's tokens.

## Expected export

- Export the chosen direction's design tokens (colors, type, spacing) as JSON or CSS variables.
- Copy the chosen direction's HTML / CSS as a snippet to drop into the codebase.

## Common failure modes

- **Identical-looking directions.** If the four directions don't differ on at least three axes (color, density, type, tone), they're not real exploration.
- **Lorem ipsum content.** Use realistic copy — empty-state copy is part of the design decision.
- **No recommendation.** "Up to you" is a cop-out. Pick one and defend it.
- **No tradeoffs.** Each direction should have an explicit "this is great for X, weak for Y."
- **Decorative-only differences** (e.g., four border-radius values). Real differences are in tone, density, hierarchy, and content.
