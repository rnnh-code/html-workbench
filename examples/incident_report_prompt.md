# Example: Incident report / postmortem

## User request

> Write up last night's outage. Started 14:02 UTC, recovered 14:31 UTC. Caused by a deploy that exhausted DB connections. Need a timeline, root-cause chain, and action items.

## Why the skill should trigger

Postmortems have a vertical spine (the timeline) with multiple parallel lanes (severity, role, evidence). They also have a root-cause chain that's easier to follow visually than as nested bullets. And the action items are exportable into a tracker. Markdown can do timelines but can't show severity colors, can't anchor evidence to specific timestamps, and forces the reader through linear text.

## HTML capability categories

- **Workflows** — vertical timeline with severity badges.
- **Code** — log excerpts, alert payloads, the offending diff.
- **Tables** — action items with owner / due date / status; impact panel.
- **Illustrations** — root-cause causal diagram (SVG).
- **Images** — graphs from monitoring (if provided).

## Recommended pattern

Incident report / postmortem (`html_artifact_patterns.md` §11).

## Expected output structure

- Headline: impact in one sentence ("29 minutes of elevated 500 errors on the API, peaking at 12% error rate.").
- Impact panel: users affected (with method of estimate), duration, region, severity.
- Timeline: UTC timestamps in a vertical column, each event with role tag (Detection / Response / Diagnosis / Mitigation / Recovery), evidence link, and a one-line description.
- Root-cause chain: SVG showing proximate cause → contributing factors → underlying conditions, or a 5-whys list.
- Detection / response analysis: what worked (alert fired, oncall paged), what didn't (no graph for connection pool, runbook out of date).
- Action items: table with owner, due date, status badge, link to ticket.
- Appendix: relevant logs, graphs, related links.

## Expected interactions

- Filter timeline by role.
- Click an evidence reference → expand the log excerpt.
- Sort action items by due date or owner.
- Severity badge legend toggle.

## Expected export

- Copy the timeline as Markdown for posting to the incident channel.
- Copy action items as JSON for ticket import.
- Copy the executive summary as a paragraph for leadership.

## Common failure modes

- **Blame-oriented language.** Postmortems describe systems, not people. "X failed to do Y" should be "the on-call rotation didn't catch Y because Z."
- **Mixed timezones.** UTC for everything, no exceptions. Show local in parentheses if useful.
- **Root cause stops too early.** "Deploy exhausted connections" is the proximate cause. Why was the connection limit so low? Why didn't the deploy preview catch it?
- **Action items without owner or date.** Worth nothing.
- **No follow-through marker.** Action items need a status field ("open / in-progress / done") so the doc stays useful as the team executes on it.
