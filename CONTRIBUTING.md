# Contributing

Thanks for improving the UofT ASIC Team's course materials.

## After creating a course from this template

1. Run `scripts/init-template.py` with `--id`, `--title` and `--description`. The org is always `uoftasic`.
2. Enable GitHub Pages from branch `main`, folder `/docs`.
3. Name the repo after the course id (`dd103`, `ic101`, …).

[TEMPLATE.md](TEMPLATE.md) has the full checklist.

## Placeholders

Only these three are filled in:

| Token | Example |
|-------|---------|
| `{{COURSE_ID}}` | `dd103` |
| `{{COURSE_TITLE}}` | `DD103 — RTL on FPGAs & ASICs` |
| `{{DESCRIPTION}}` | `RTL synthesis intro with Yosys` |

## Conventions

| Item | Convention |
|------|------------|
| Org | `uoftasic` |
| Default branch | `main` |
| Docs pages | kebab-case `.md` under `docs/` |
| Lab IDs | `lab-NN-short-name` |
| Course path table | Four columns: `#`, a column with no header for Read or Do (plain text), What, and Time. Each Do row ends with a sentence on what the student does, and the row times add up to the course total. [AGENTS.md](AGENTS.md) has the format. |
| Lab titles | `Lab 01: Title`, the same in the page's `#` header, the course path and the sidebar |
| Adding a guide page | `.md` under `docs/guide/`, a Read row in the home page's course path, and an entry in `docs/_sidebar.md` in the same position |
| Adding a lab | `labs/<id>/`, `docs/labs/<id>-overview.md`, a Do row in the course path, and an entry in `docs/_sidebar.md` in the same position |
| Links between pages | relative to `docs/`, for example `guide/yosys-basics.md` |
| Images | `docs/assets/img/`, linked relative to the page (`../assets/img/…` from `docs/guide/` or `docs/labs/`) |
| Binaries | small images in `docs/assets/`; large data in Git LFS or external storage |

## Where things go

- `docs/guide/` is reading only: concepts, figures and worked examples, with no commands the student must run.
- `docs/labs/` holds the lab writeups. They are the only pages with steps to run, and each part ends with what the student should see. In at least one required part the student makes something, optional parts come after the required ones, and each lab ends with a Finishing section: you're done when, questions, and what to submit.
- `labs/` holds the runnable HDL, Python and data. Each `labs/<id>/README.md` is short: it links to its Docsify writeup, shows how to run, and lists the files.
- `scripts/` holds utilities. List entry points in `scripts/README.md`.

[AGENTS.md](AGENTS.md) describes each page type in more detail.

Don't put grades, solution keys or PII under `docs/`. Use `labs/**/solutions/`, and gitignore it on student forks when needed.

## Local docs preview

```bash
npx docsify-cli serve docs
```

Then open http://localhost:3000.

## Pull requests

Keep changes focused. For doc-only PRs, check the navigation and math locally when you can. The docs link check runs on changes under `docs/**`.
