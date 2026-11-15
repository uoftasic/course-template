# Scripts

Utilities for {{COURSE_TITLE}} under the UofT ASIC org (`uoftasic`).

## Entry points

| Script | Purpose |
|--------|---------|
| `check_site.py` | Check that every local link and `#anchor` in the rendered site resolves; `.github/workflows/site.yml` runs it on `docs/_site` |
| `hello.py` | Smoke-check that Python runs in this clone |
| `init-template.py` | Fill `{{COURSE_ID}}` / title / description after using the template |

## Usage

```bash
# From repo root
python3 scripts/hello.py

python3 scripts/init-template.py \
  --id dd103 \
  --title "DD103 — RTL on FPGAs & ASICs" \
  --description "RTL on FPGAs and open-source ASIC flows"
```

## Conventions

- Write scripts in Python where you can. HDL tooling belongs in `labs/` or the shared workbench.
- Keep secrets out of the repo. If a script needs configuration, add a `.env.example`.
- When you add a script, add it to the table above.
