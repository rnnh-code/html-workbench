# Example: Technical explainer

## User request

> Explain how our token-bucket rate limiter works to a new engineer joining the team. Include the request lifecycle, the Redis storage layout, and the failure modes.

## Why the skill should trigger

The reader is technical but unfamiliar. They need a *mental model first*, then code, then edge cases. HTML wins because it lets us put a labeled SVG lifecycle diagram next to annotated code, with a glossary the reader can expand on demand. Markdown linearizes all of this, making it harder to learn from.

## HTML capability categories

- **Code** — annotated snippets with inline notes.
- **Illustrations** — SVG lifecycle / state diagram.
- **Workflows** — request flow from arrival to allow/deny.
- **Tables** — Redis key layout, failure-mode reference.
- **Spatial layouts** — diagram beside its explanation.

## Recommended pattern

Technical explainer (`html_artifact_patterns.md` §3).

## Expected output structure

- Title + one-line answer ("Token bucket per user, refills at N/sec, burst capacity B, all in Redis.").
- Mental model section: the simplest accurate metaphor (bucket of tokens, leaks at a constant rate).
- Annotated lifecycle SVG: request arrives → key derived → tokens checked → decremented → response. Color-coded states.
- Step-by-step walk-through with code snippets and inline annotations.
- Redis storage layout: key pattern, value structure, TTL, atomicity guarantees.
- Edge cases and failure modes: clock skew, Redis unavailability, race on first-bucket creation.
- Glossary (collapsible).
- Where to find this in the codebase: file paths, function names, line ranges.

## Expected interactions

- Hover diagram node → highlight matching code snippet.
- Click annotation → highlight the code line.
- Expand glossary on demand.

## Expected export

- Copy the explanation as Markdown for pasting into onboarding docs.

## Common failure modes

- **Code-first ordering.** Showing implementation before the mental model loses readers.
- **Diagram with no labels.** Boxes and arrows that don't say what they are.
- **Skipping edge cases.** The most useful part of an explainer is "what happens when X breaks."
- **No pointer back to actual files.** New engineers can't find the code, can't read it, can't extend the explanation.
- **Over-explaining.** If the code is self-evident, don't annotate every line.
