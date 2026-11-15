# {{COURSE_TITLE}}

{{DESCRIPTION}}

This is the course and lab template for the UofT ASIC Team (`uoftasic`). The published site lives under `./docs`, and runnable labs, scripts, notebooks and data stay outside it, in the repo root. Quarto builds the site from the Markdown in `docs/` (configured in `docs/_quarto.yml`), with MathJax for the math and a PDF of every page, and `.github/workflows/site.yml` deploys it to GitHub Pages.

Org: [github.com/uoftasic](https://github.com/uoftasic)

## Live docs

- This template: https://uoftasic.com/course-template/
- Education hub: https://edu.uoftasic.com/
- A course made from this template, once Pages is enabled: https://uoftasic.com/{{COURSE_ID}}/

## Use this template

1. On [uoftasic/course-template](https://github.com/uoftasic/course-template), click **Use this template** and create a repo named after the course id (for example `dd103` or `serdes-lab`).
2. Clone it and fill in the course fields:

```bash
python3 scripts/init-template.py \
  --id {{COURSE_ID}} \
  --title "{{COURSE_TITLE}}" \
  --description "{{DESCRIPTION}}"
```

3. Set **Settings → Pages → Source** to **GitHub Actions**.

[TEMPLATE.md](TEMPLATE.md) has the checklist. The org is always `uoftasic`; only the course id, title and description are filled in.

The sample pages already follow the course structure: a course path table on the home page, guide pages for reading, and lab writeups for doing. [AGENTS.md](AGENTS.md) explains it.

## Quick start

```bash
git clone https://github.com/uoftasic/{{COURSE_ID}}.git
cd {{COURSE_ID}}

# Docs (requires Quarto 1.11)
quarto preview docs
# → http://localhost:4200
quarto render docs --profile pdf --to typst
# → the whole course as one PDF in docs/_book/

# Sample script
python3 scripts/hello.py

# Sample lab
python3 labs/lab-01/src/main.py
```

Courses that need IIC-OSIC-TOOLS or SKY130 run in the shared [workspace](https://github.com/uoftasic/workspace) that students set up in IC101. Document those setup steps in the course instead of bundling Docker in every repo.

## Layout

| Path | On Pages? | Purpose |
|------|-----------|---------|
| `docs/` | Yes | The Quarto site students read (`docs/_quarto.yml`) |
| `docs/guide/` | Yes | Guide pages: reading only |
| `docs/labs/` | Yes | Lab writeups: the steps students follow |
| `labs/` | No | Runnable packages (HDL, Python, data, graders) |
| `scripts/` | No | Team utilities and automation |
| `notebooks/` | No | Exploratory and assignment notebooks |
| `data/`, `figures/` | No | Shared datasets and source figures |

## GitHub Pages

| Setting | Value |
|---------|--------|
| Source | GitHub Actions |

`.github/workflows/site.yml` renders `docs/` with Quarto whenever a push to `main` changes `docs/`, `scripts/check_site.py` or the workflow itself, and deploys `docs/_site`, which includes a PDF of every page and the whole-course PDF.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE). Copyright UofT ASIC Team / `uoftasic`.
