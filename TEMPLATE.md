# Template bootstrap (UofT ASIC)

Create a course or lab-notes repo from this template under **`uoftasic`**, fill the three course fields, enable Pages.

## Fixed vs fillable

| Item | Value |
|------|--------|
| GitHub org | `uoftasic` (hardcoded — do not change) |
| Team | UofT ASIC Team |

| Token | Meaning | Example |
|-------|---------|---------|
| `{{COURSE_ID}}` | Repo slug / course id | `dd103`, `ic101`, `serdes-lab` |
| `{{COURSE_TITLE}}` | Display name | `DD103 — RTL on FPGAs & ASICs` |
| `{{DESCRIPTION}}` | One-line blurb | `RTL synthesis intro with Yosys` |

## Init script

```bash
python3 scripts/init-template.py \
  --id dd103 \
  --title "DD103 — RTL on FPGAs & ASICs" \
  --description "RTL on FPGAs and open-source ASIC flows"
```

Dry run: add `--dry-run`.

## After-clone checklist

- [ ] Repo created under `uoftasic` with id matching `{{COURSE_ID}}`
- [ ] `scripts/init-template.py` run (or manual replace of the three tokens)
- [ ] Pushed to `main`
- [ ] Pages: **Settings → Pages → `main` / `/docs`**
- [ ] Live: `https://uoftasic.github.io/<course-id>/`
- [ ] Sidebar navigates Home → Getting started → Lab 01
- [ ] Math + sample figure render on the home page
- [ ] (Maintainers of this template) **Settings → Template repository** enabled

## Naming

Prefer course ids already used by the team (`ic###`, `ad###`, `dd###`) or a clear kebab-case lab name. Keep the GitHub repo name equal to `{{COURSE_ID}}` so Pages and clone URLs stay predictable.

## Related

| Repo | Role |
|------|------|
| [asic-edu-workbench](https://github.com/uoftasic/asic-edu-workbench) | Shared local toolchain (IIC-OSIC-TOOLS) |

This Docsify template gives zero-build docs under `docs/` plus first-class `labs/` and `scripts/` trees. Each course publishes at `https://uoftasic.github.io/<course-id>/`.
