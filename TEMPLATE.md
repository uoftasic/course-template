# Template bootstrap (UofT ASIC)

To start a course or lab-notes repo: create it from this template under `uoftasic`, fill in the three course fields, and enable Pages.

## Fixed and fillable values

| Item | Value |
|------|--------|
| GitHub org | `uoftasic` (hardcoded, don't change it) |
| Team | UofT ASIC Team |

| Token | Meaning | Example |
|-------|---------|---------|
| `{{COURSE_ID}}` | Repo slug and course id | `dd103`, `ic101`, `serdes-lab` |
| `{{COURSE_TITLE}}` | Display name | `DD103 — RTL on FPGAs & ASICs` |
| `{{DESCRIPTION}}` | One-line blurb | `RTL synthesis intro with Yosys` |

## Init script

```bash
python3 scripts/init-template.py \
  --id dd103 \
  --title "DD103 — RTL on FPGAs & ASICs" \
  --description "RTL on FPGAs and open-source ASIC flows"
```

Add `--dry-run` to see what it would change without writing anything.

## After-clone checklist

- [ ] Repo created under `uoftasic`, named the same as `{{COURSE_ID}}`
- [ ] `scripts/init-template.py` run (or the three tokens replaced by hand)
- [ ] Pushed to `main`
- [ ] Pages: **Settings → Pages → `main` / `/docs`**
- [ ] Live at `https://uoftasic.com/<course-id>/` (org Pages; the hub is https://edu.uoftasic.com/)
- [ ] Sidebar goes Home → Getting started → Lab 01: Starter script
- [ ] Math and the sample figure render on the Getting started page
- [ ] Home page filled in: who the course is for, prerequisites, total time, and the course path rows, with times that add up to the total
- [ ] (Maintainers of this template only) **Settings → Template repository** enabled

The sample pages follow the course structure in [AGENTS.md](AGENTS.md). The home page has the course path, guide pages are for reading only, and lab writeups are the one place where students run things. The sample lab shows the parts of a lab: a required part where the student edits the script and predicts the result, an optional part at the end, and the Finishing section.

## Naming

Use a course id the team already follows (`ic###`, `ad###`, `dd###`) or a clear kebab-case lab name. Keep the GitHub repo name equal to `{{COURSE_ID}}` so the Pages and clone URLs are predictable.

## Related

Each course made from this template is published at `https://uoftasic.com/<course-id>/`, with Docsify pages under `docs/` (no build step) and its runnable code in `labs/` and `scripts/`. The education hub is https://edu.uoftasic.com/.
