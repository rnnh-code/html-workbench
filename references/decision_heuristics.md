# Decision Heuristics: Markdown vs. Which HTML Artifact

When the request is ambiguous, this file resolves it.

The eight HTML capability categories from `SKILL.md` §4 are the trigger checklist:

1. Tables · 2. Design · 3. Illustrations · 4. Code · 5. Interaction · 6. Workflows · 7. Spatial layouts · 8. Images

**Two-or-more rule:** if the response would meaningfully use ≥ 2 categories, prefer HTML. If only 1 applies weakly, prefer Markdown.

---

## Output type decision tree

Walk this top to bottom; first match wins.

1. **User asked for Markdown / plain text / a code block?** → Markdown.
2. **Answer is < 200 words and prose-only?** → Markdown.
3. **Answer is a single command, code snippet, or simple list?** → Markdown.
4. **Answer is a small comparison (≤ 6 rows × 3 cols)?** → Markdown table.
5. **Answer involves sorting, editing, tuning, triaging, or selecting things the user will export?** → HTML editor / dashboard / tuner.
6. **Answer is a deck-style presentation (titles, slides, advance with keys)?** → HTML slide deck.
7. **Answer is a multi-direction design exploration?** → HTML design sheet.
8. **Answer involves SVG diagrams the user will want to copy out?** → HTML diagram sheet.
9. **Answer is a long technical document with code, diagrams, and tables (plan, spec, explainer, postmortem, report)?** → HTML document.
10. **Default if HTML is on the table and none of the above:** HTML document with the appropriate pattern from `html_artifact_patterns.md`.

---

## Markdown answer vs. HTML document

| Signal | Lean Markdown | Lean HTML document |
|---|---|---|
| Length | < 200 words | > 300 words |
| Comparison required | Small (≤ 6 rows) | Dense or weighted |
| Diagrams | None or one tiny ASCII | Two or more, or any SVG |
| Code | Single snippet or pure code answer | Multiple snippets with annotation |
| User decides something | No | Yes |
| Will be reread later | No | Yes |
| Will be shared | Maybe (paste) | Yes (open in browser) |

---

## HTML document vs. HTML report

| Document | Report |
|---|---|
| Standalone reference (plan, spec, explainer) | Periodic / scheduled (weekly, monthly, post-incident) |
| Reader pulls (looks it up when needed) | Reader gets pushed (sent / shared) |
| Dense reference content | Executive summary up top, deltas highlighted |
| No metric tiles | Often has metric tiles |

---

## HTML report vs. HTML dashboard

| Report | Dashboard |
|---|---|
| Frozen-in-time snapshot | Implied to update (even if static, *feels* live) |
| Linear top-to-bottom | Grid of tiles, parallel reading |
| Narrative-driven | Filter / drill / pivot |
| Decisions discussed | Decisions implied by the data |

If the user asks for a *one-time write-up*, build a report. If they ask for an *ongoing view*, build a dashboard — or push back and explain that a static HTML file can't auto-update.

---

## HTML prototype vs. HTML editor

| Prototype | Editor |
|---|---|
| Demonstrates an experience | Captures decisions |
| Click-through with fake data | Real data the user provides or edits |
| Export rare (maybe screenshots) | Export is the *point* |
| Polish is the value | Function is the value |

If the user wants to *show* something, build a prototype. If they want to *do* something, build an editor.

---

## HTML explainer vs. HTML slide deck

| Explainer | Slide deck |
|---|---|
| Read alone, scrolling | Presented to others, advancing |
| Dense per page | Sparse per slide |
| Linear flow | Sectioned, sometimes nonlinear |
| Often has TOC | Often has agenda |
| Stays open in a tab | Goes fullscreen |

If the user says "explain X to me," build an explainer. If they say "I'm presenting X to leadership," build a slide deck.

---

## HTML diagram sheet vs. HTML design sheet

| Diagram sheet | Design sheet |
|---|---|
| The diagrams are the deliverable | Components / tokens / states are the deliverable |
| Each diagram exports as standalone SVG | Each token / component exports as code |
| Reader will copy into other docs | Reader will copy into other code |
| Cares about shape language consistency | Cares about token consistency |

---

## When to *refuse* HTML and write Markdown

Be willing to push back. Build Markdown when:

- The user asked a yes/no question.
- The user asked for a single function or snippet.
- The user is in a chat context and wants a quick answer.
- The artifact would be entirely plain prose with no structure.
- The artifact would be a 5-row table.
- The user is iterating fast and an HTML artifact would slow them down.
- You'd be making something *decorative* rather than *load-bearing*.

Say so plainly: "Markdown is the better output here." Don't apologize for it.

---

## Worked examples

| Request | Right output | Why |
|---|---|---|
| "What does `git rebase --onto` do?" | Markdown answer | Definition, < 200 words, no comparison |
| "Compare `git rebase` vs `git merge` for our team" | HTML document or Markdown table | If 4-row table is enough → Markdown. If you want to add a flow diagram or pros/cons → HTML |
| "Plan the migration of our auth service to JWT" | HTML implementation plan | Multiple capabilities (workflows + code + tables + illustrations) |
| "Review this PR" | HTML PR review | Code + tables + spatial + interaction |
| "How does our rate limiter work?" | HTML technical explainer | Code + illustrations + workflows |
| "Show me 4 design directions for the empty state" | HTML design exploration | Design + spatial + images |
| "Tune the easing on this hero animation" | HTML animation sandbox | Interaction + design + code |
| "Triage these 40 bug reports" | HTML triage board | Interaction + spatial + tables |
| "Write the postmortem for last night's outage" | HTML incident report | Workflows + code + tables + images |
| "Give me a one-paragraph status on the auth project" | Markdown | Prose, < 200 words |
| "Format this CSV as a table" | Markdown | Single small comparison |
| "Write a Python function to parse this string" | Markdown code block | Code-only answer |
| "Send the team the quarterly results" | HTML weekly/quarterly report | Tables + design + workflows |
| "Render this state machine" | HTML diagram sheet (single diagram) or inline SVG in Markdown | If reusable / shareable → HTML; if quick illustration → Markdown w/ SVG |

---

## Failure modes (don't do these)

- **HTML for a 100-word answer.** It looks performative and slows the user down.
- **HTML report when the user is in a fast-moving chat.** They'll keep working in chat; the artifact gets lost.
- **HTML editor with no export.** Defeats the entire reason to use HTML over Markdown for this case.
- **Markdown table when there are 30 rows and 8 columns.** Use HTML so the user can sort / filter.
- **Slide deck when the content is reference material.** Slides are for presenting; references are for looking up. Don't conflate them.
- **Prototype when the user wanted an editor.** Prototypes show, editors *do*. If the user is going to act on the output, build an editor.
