# Export Patterns

The export loop is one of the main reasons HTML beats Markdown for interactive artifacts. The user does work in the artifact, and that work needs to come back out — into a doc, a ticket, a prompt, a config file, or the next conversation.

This file ships ready-to-paste vanilla JS snippets. No dependencies, framework-neutral, safe to inline.

---

## Universal copy helper

Use this as the base for every "copy" button. It tries `navigator.clipboard.writeText` (modern, async, returns a promise) and falls back to a hidden textarea + `document.execCommand('copy')` for older browsers and insecure contexts.

```html
<script>
  function copyText(text) {
    if (navigator.clipboard && window.isSecureContext) {
      return navigator.clipboard.writeText(text);
    }
    return new Promise((resolve, reject) => {
      const ta = document.createElement('textarea');
      ta.value = text;
      ta.style.position = 'fixed';
      ta.style.opacity = '0';
      ta.style.pointerEvents = 'none';
      document.body.appendChild(ta);
      ta.focus();
      ta.select();
      try {
        document.execCommand('copy') ? resolve() : reject();
      } catch (err) {
        reject(err);
      } finally {
        document.body.removeChild(ta);
      }
    });
  }

  function flashCopied(button, label = 'Copied!', duration = 1500) {
    const original = button.textContent;
    button.textContent = label;
    button.classList.add('is-copied');
    setTimeout(() => {
      button.textContent = original;
      button.classList.remove('is-copied');
    }, duration);
  }

  document.addEventListener('click', (e) => {
    const btn = e.target.closest('[data-copy]');
    if (!btn) return;
    const target = btn.dataset.copyTarget
      ? document.querySelector(btn.dataset.copyTarget)
      : null;
    const text = target ? (target.value ?? target.textContent) : btn.dataset.copy;
    copyText(text).then(() => flashCopied(btn)).catch(() => flashCopied(btn, 'Copy failed', 2000));
  });
</script>
```

Then any button with `data-copy="..."` or `data-copy-target="#some-id"` works:

```html
<button data-copy="hello world">Copy hello</button>
<button data-copy-target="#prompt-textarea">Copy prompt</button>
```

---

## Download helper

For exporting JSON, CSV, or text as a file the user keeps locally:

```js
function downloadFile(filename, content, mime = 'application/json') {
  const blob = new Blob([content], { type: mime });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = filename;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  setTimeout(() => URL.revokeObjectURL(url), 1000);
}

// usage
downloadFile('decisions.json', JSON.stringify(state, null, 2));
downloadFile('triage.csv', toCsv(rows), 'text/csv');
```

---

## Pattern: Copy visible summary as Markdown

Hand-build a Markdown string from the *current state* of the artifact (not from the original input — the user's edits matter).

```js
function summaryAsMarkdown(state) {
  const lines = [];
  lines.push(`# ${state.title}`);
  lines.push('');
  lines.push(`_${state.subtitle}_`);
  lines.push('');
  if (state.notes) lines.push(state.notes, '');
  state.sections.forEach(s => {
    lines.push(`## ${s.heading}`);
    s.items.forEach(item => lines.push(`- ${item}`));
    lines.push('');
  });
  return lines.join('\n');
}
```

Wire it to a button:

```html
<button id="copy-md">Copy as Markdown</button>
<script>
  document.getElementById('copy-md').addEventListener('click', (e) => {
    copyText(summaryAsMarkdown(state)).then(() => flashCopied(e.currentTarget));
  });
</script>
```

---

## Pattern: Copy full state as JSON

Most useful for editors that capture decisions. The receiving system (an agent, a config loader, a teammate) parses it.

```js
function exportStateAsJson(state) {
  return JSON.stringify(state, null, 2);
}

document.getElementById('copy-json').addEventListener('click', (e) => {
  copyText(exportStateAsJson(state)).then(() => flashCopied(e.currentTarget, 'JSON copied'));
});
```

---

## Pattern: Copy diff vs. baseline

For editors where users modify a baseline (feature flags, prompt parameters, design tokens). Only export what *changed*.

```js
function diffAgainst(baseline, current) {
  const diff = {};
  for (const [key, value] of Object.entries(current)) {
    if (JSON.stringify(value) !== JSON.stringify(baseline[key])) {
      diff[key] = { from: baseline[key], to: value };
    }
  }
  return diff;
}

function diffAsMarkdown(diff) {
  if (Object.keys(diff).length === 0) return '_No changes._';
  const lines = ['| Field | From | To |', '|---|---|---|'];
  for (const [k, v] of Object.entries(diff)) {
    lines.push(`| \`${k}\` | \`${JSON.stringify(v.from)}\` | \`${JSON.stringify(v.to)}\` |`);
  }
  return lines.join('\n');
}
```

---

## Pattern: Copy as prompt

For prompt tuners, prompt builders, or any artifact whose output is meant to be pasted back into an agent. Build the prompt as a single string with clear delimiters.

```js
function buildPromptOutput(state) {
  return [
    state.systemPrompt && `# System\n${state.systemPrompt}`,
    state.examples?.length && `# Examples\n${state.examples.map(e => `User: ${e.user}\nAssistant: ${e.assistant}`).join('\n\n')}`,
    `# Parameters\nmodel: ${state.model}\ntemperature: ${state.temperature}\nmax_tokens: ${state.maxTokens}`,
    state.task && `# Task\n${state.task}`,
  ].filter(Boolean).join('\n\n');
}
```

---

## Pattern: Export reordered cards

For triage boards, kanban-style editors, or anything with drag-drop reorder. Capture both column membership *and* order within each column.

```js
function exportBoard(columns) {
  const out = {};
  for (const col of columns) {
    out[col.id] = Array.from(col.cards).map(c => ({ id: c.id, title: c.title }));
  }
  return out;
}
```

---

## Pattern: Export annotations

For PR reviews, postmortems, dataset curation. Each annotation has location, severity, comment, and resolved state.

```js
function exportAnnotations(annotations) {
  return annotations.map(a => ({
    target: a.target,        // e.g., "src/foo.ts:42" or "row:1234"
    severity: a.severity,
    comment: a.comment,
    resolved: !!a.resolved,
    timestamp: a.timestamp,
  }));
}
```

---

## Pattern: Export tuned parameters as CSS

For animation sandboxes and design-token editors that produce CSS.

```js
function tokensAsCss(tokens) {
  return `:root {\n${
    Object.entries(tokens).map(([k, v]) => `  --${k}: ${v};`).join('\n')
  }\n}`;
}
```

---

## Pattern: Export accepted / rejected dataset rows

For dataset curation. Two files: accepted and rejected with reasons.

```js
function exportCuration(rows) {
  const accepted = rows.filter(r => r.status === 'accepted')
    .map(r => JSON.stringify({ id: r.id, content: r.content }));
  const rejected = rows.filter(r => r.status === 'rejected')
    .map(r => JSON.stringify({ id: r.id, content: r.content, reason: r.reason }));
  return {
    acceptedJsonl: accepted.join('\n'),
    rejectedJsonl: rejected.join('\n'),
    accepted_count: accepted.length,
    rejected_count: rejected.length,
  };
}
```

---

## Pattern: Export final decision matrix

For decision matrices. Include weights, scores, totals, and the recommended option.

```js
function exportDecision(matrix) {
  const totals = matrix.options.map(opt => ({
    name: opt.name,
    total: matrix.criteria.reduce((sum, c) => sum + (opt.scores[c.id] * c.weight), 0),
  }));
  totals.sort((a, b) => b.total - a.total);
  return {
    question: matrix.question,
    criteria: matrix.criteria,
    options: matrix.options,
    totals,
    recommended: totals[0].name,
  };
}
```

---

## Pattern: Export implementation checklist

For implementation plans. Flatten phases / sections into a single ordered checklist.

```js
function exportChecklist(plan) {
  const items = [];
  for (const phase of plan.phases) {
    items.push(`## ${phase.name}`);
    for (const step of phase.steps) {
      const box = step.done ? '[x]' : '[ ]';
      items.push(`- ${box} ${step.description}${step.owner ? ` _(${step.owner})_` : ''}`);
    }
  }
  return items.join('\n');
}
```

---

## Confirmation UX

Every export should provide visible confirmation. Without it, the user re-clicks (or worse, assumes it failed and abandons the artifact).

- Inline pill or button label change for ~1.5s.
- `aria-live="polite"` on the confirmation element so screen readers announce it.
- For downloads, the browser's native download UI is sufficient — but include a fallback message ("If your download didn't start, click here").

```html
<button id="export" data-copy-target="#state">
  Export as JSON
</button>
<span id="export-status" aria-live="polite" class="sr-only"></span>
```

---

## Safety reminders

- **Escape user input before embedding it in HTML** (use `textContent`, not `innerHTML`).
- **Don't include secrets** in exports — credentials, tokens, environment variables — even if they're in the source data.
- **Don't auto-submit forms to external endpoints** as part of an "export." Stay local.
- **Don't fetch remote resources** to enrich exports. Keep it offline-friendly.

---

## What gets exported = what's on screen

The cardinal rule: the export should match what the user *sees right now*. If they reordered cards, the export reflects that. If they edited tokens, the export uses the edited values. If they added notes, the notes are in the export.

Don't export the original input. Don't merge in defaults the user removed. Don't add metadata they didn't authorize.

The user's mental model: "I see it on screen, I copy it, I paste it." Anything that violates this loses their trust.
