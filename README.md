# {{COURSE_TITLE}}

{{DESCRIPTION}}

This is the Docsify course and lab template for the UofT ASIC Team (`uoftasic`). The published site lives under `./docs`. Runnable labs, scripts, notebooks and data stay outside it, in the repo root. GitHub Pages serves the site with no build step, and Markdown, MathJax and images work as they are.

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

3. Enable **Settings → Pages → Deploy from a branch → `main` / `/docs`**.

[TEMPLATE.md](TEMPLATE.md) has the checklist. The org is always `uoftasic`; only the course id, title and description are filled in.

The sample pages already follow the course structure: a course path table on the home page, guide pages for reading, and lab writeups for doing. [AGENTS.md](AGENTS.md) explains it.

## Quick start

```bash
git clone https://github.com/uoftasic/{{COURSE_ID}}.git
cd {{COURSE_ID}}

# Docs (requires Node.js)
npx docsify-cli serve docs
# → http://localhost:3000

# Sample script
python3 scripts/hello.py

# Sample lab
python3 labs/lab-01/src/main.py
```

Courses that need IIC-OSIC-TOOLS or SKY130 run in the shared [workspace](https://github.com/uoftasic/workspace) that students set up in IC101. Document those setup steps in the course instead of bundling Docker in every repo.

## Layout

| Path | On Pages? | Purpose |
|------|-----------|---------|
| `docs/` | Yes | The Docsify site students read |
| `docs/guide/` | Yes | Guide pages: reading only |
| `docs/labs/` | Yes | Lab writeups: the steps students follow |
| `labs/` | No | Runnable packages (HDL, Python, data, graders) |
| `scripts/` | No | Team utilities and automation |
| `notebooks/` | No | Exploratory and assignment notebooks |
| `data/`, `figures/` | No | Shared datasets and source figures |

## GitHub Pages

| Setting | Value |
|---------|--------|
| Source | Deploy from a branch |
| Branch | `main` |
| Folder | `/docs` |

The Docsify site doesn't need an Actions deploy step.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE). Copyright UofT ASIC Team / `uoftasic`.
