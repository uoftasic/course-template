# Contributing to docs

Conventions for pages under `docs/` in UofT ASIC Docsify course repos.

## Where content goes

| Content | Path |
|---------|------|
| Conceptual guides | `docs/guide/` |
| Formulas, APIs, cheatsheets | `docs/reference/` |
| Lab writeups (markdown only) | `docs/labs/` |
| Images used in docs | `docs/assets/img/` |
| Runnable lab code / data | `labs/<id>/` (not Pages) |
| CLIs and automation | `scripts/` (not Pages) |

## Adding a page

1. Add a kebab-case `.md` file under the right folder.
2. Add a sidebar entry in `_sidebar.md`.
3. Optionally add a top-nav link in `_navbar.md`.
4. Keep the first heading as `# Title`.

## Markdown conventions

- **Math:** `$inline$`, `$$display$$`
- **Images:** `![](assets/img/name.png)` relative to `docs/`
- **Code:** fenced blocks with a language tag (`systemverilog`, `python`, `bash`, …)
- **Cross-links:** Docsify routes for other doc pages; `https://github.com/uoftasic/...` for `labs/` and `scripts/`

## What not to put in `docs/`

- Grades, solution keys, or PII
- Large datasets, GDSII, or model weights
- Generated HTML besides `index.html`

Solution keys: `labs/**/solutions/` (gitignore on student forks if needed).

## Preview

```bash
npx docsify-cli serve docs
```
