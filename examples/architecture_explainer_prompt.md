# Example: Architecture / module map

## User request

> I just inherited a codebase I don't know. Walk me through the architecture — services, data stores, how a checkout flows through, who owns what.

## Why the skill should trigger

Architecture lives in space — services on a canvas, data flowing along arrows, modules grouped by ownership. Markdown can list services, but loses the *shape* of the system. HTML lets the user see all the pieces at once and read details on demand.

## HTML capability categories

- **Illustrations** — system diagram in SVG.
- **Spatial layouts** — diagram + module table side by side.
- **Tables** — services / modules with owner / path / dependencies.
- **Workflows** — request lifecycle for the most important user-facing operation.

## Recommended pattern

Architecture / module map (`html_artifact_patterns.md` §4).

## Expected output structure

- Title + one-line system purpose ("Marketplace — buyers and sellers; payments via Stripe.").
- Top-level system diagram in SVG. Consistent shape language: rectangle = service, cylinder = datastore, parallelogram = queue, oval = external. Color by team.
- Service / module table: name, responsibility, owner team, source path, key dependencies.
- Request lifecycle for one critical operation (e.g., "place order"): step-by-step with the relevant services highlighted in the diagram.
- External dependencies section: third-party APIs, datastores, queues.
- Glossary of internal terms.

## Expected interactions

- Click a box in the diagram → scroll to its row in the table and highlight.
- Filter the table by owner team.
- Toggle which lifecycle is shown in the diagram.
- Hover an arrow → show the protocol / payload type.

## Expected export

- Copy module table as JSON.
- Copy the SVG of the diagram.
- Copy a Markdown summary.

## Common failure modes

- **Boxes-and-arrows soup.** A diagram with no shape language and no legend conveys little.
- **Missing the legend.** If you use shape and color to encode meaning, you must explain it.
- **No path-to-source.** "Service A" is useless without `src/services/a/` or equivalent.
- **Inconsistent shape language between artifact and downstream docs.** If you invent shapes that the team doesn't already use, document them prominently.
- **Pretending to know the system.** If the user didn't tell you what exists, ask or use placeholders. Don't fabricate services.
