# Agent guide: UofT ASIC course repos

This is a course repository for the UofT ASIC Team (`uoftasic`). It holds teaching material for IC, RTL, FPGA and open-source ASIC flows. The site under `docs/` is published on GitHub Pages with Docsify, with no build step. Everything students run lives outside `docs/`.

Write for a student working through the course, not for whoever maintains the template. Concrete labs and pages a student can follow from start to finish are worth more than meta documentation.

## Goals

- Teach IC development skills: RTL (SystemVerilog/Verilog), simulation, synthesis, FPGA bring-up and open ASIC flows (for example Yosys, LibreLane, SKY130), as the course needs them.
- Keep reading and doing apart. Guide pages explain; lab writeups are the only pages that ask the student to run anything; `labs/`, `scripts/` and `notebooks/` hold what they run.
- Never publish grades, solution keys or PII under `docs/`. Put keys in `labs/**/solutions/` and gitignore them on student forks when policy requires.

## Layout

Keep each kind of file in the folder listed for it.

| Path | Published? | Put here |
|------|------------|----------|
| `docs/README.md` | Yes | Home page with the course path table |
| `docs/guide/` | Yes | Guide pages: concepts, figures, worked examples. Reading only. |
| `docs/labs/` | Yes | Lab writeups only (`lab-NN-*-overview.md`) |
| `docs/reference/` | Yes | Optional lookup pages: cheat sheets, troubleshooting tables |
| `docs/assets/img/` | Yes | Small diagrams and waveforms for the site |
| `labs/<lab-id>/` | No | HDL, Python, testbenches, local data, graders |
| `scripts/` | No | Course utilities and automation |
| `notebooks/` | No | Exploratory or assignment notebooks |
| `data/`, `figures/` | No | Shared datasets and source figures |

The site is wired up by `docs/index.html`, `docs/_sidebar.md` and `docs/_navbar.md`. Write math as `$inline$` or `$$display$$`. The `{{...}}` tokens in the sample pages (course id, title and description) are filled in by `scripts/init-template.py`; see `TEMPLATE.md`.

## Course structure

Every course follows the same shape, so a student always knows whether they should be reading or doing, and what comes next.

- **Home page** (`docs/README.md`): who the course is for, prerequisites, total time, and a numbered course path table. Each row is either *Read* (one or more guide pages) or *Do* (one lab), with a time estimate. Read and Do rows alternate in the order a student should work. `docs/_sidebar.md` lists the same pages in the same order. The Previous and Next links at the bottom of each page (the docsify-pagination plugin in `docs/index.html`) follow the sidebar, so they walk the course path too.
- **Guide pages** (`docs/guide/`): reading only. No commands the student has to run. If a page needs the student to run or build something, make it a numbered step in the matching lab writeup and leave a one-line pointer in the guide ("You'll measure this yourself in Lab 02, Part 3."). Pencil-and-paper questions can go in a short "Check yourself" block at the end of the page.
- **Lab writeups** (`docs/labs/<lab-id>-overview.md`): the one place for doing. In this order:
  1. What the student will build or measure, in two or three lines, and a link to `labs/<lab-id>/`.
  2. Before you start: which guide pages to read first, and any setup.
  3. A time estimate.
  4. Numbered parts, each with numbered steps. Each part ends with a concrete "You should see …" check. Questions the student must answer go at the step where they come up.
  5. Finishing: how the student knows they're done (for example, `make` prints PASS) and what to submit, if anything.
- **Package READMEs** (`labs/<lab-id>/README.md`): short. A link to the writeup, how to run, a table of make targets if there is a Makefile, and the file list. Don't repeat the teaching from the writeup.
- **Reference pages** (`docs/reference/`) and `solutions/` READMEs are lookup-shaped: tables and short entries.

The sample pages show this shape: `docs/README.md`, `docs/guide/getting-started.md` and `docs/labs/lab-01-overview.md`.

## Adding a lab

Labs are the main unit of coursework. Name them `lab-NN-short-name` (for example `lab-02-counter-sv`). The sample lab is just `lab-01`; give real labs a short name.

1. Create `labs/<lab-id>/` with at least:
   - `README.md`: link to the writeup and how to run
   - `src/`: HDL, Python and entry points
   - `data/`: small inputs (large binaries go in Git LFS or external storage)
   - `results/`: local outputs
   - `requirements.txt` or tool notes when needed
2. Add `docs/labs/<lab-id>-overview.md` in the writeup shape above.
3. Add a *Do* row to the course path table on the home page, and an entry in `docs/_sidebar.md` at the same position. Add it to `_navbar.md` only if it belongs in the top nav.
4. Cross-link: the writeup links to `labs/<lab-id>/` on GitHub, and the package README links to `docs/labs/<lab-id>-overview.md`.

Don't paste long HDL into Docsify pages. Link to the files under `labs/` instead.

## Adding a guide page

1. Add a kebab-case Markdown file under `docs/guide/` (for example `yosys-synth.md`).
2. Add it to a *Read* row in the course path table, and to `docs/_sidebar.md` at the same position.
3. Put images in `docs/assets/img/`.
4. Link to `labs/` and `scripts/` with GitHub URLs (`https://github.com/uoftasic/<course-id>/tree/main/labs/...`).

Docsify runs with `relativePath: false`. With that setting, page links and images resolve from different places:

- Links to other pages are relative to `docs/`, from any page: `guide/yosys-synth.md`, `labs/lab-01-overview.md`.
- Images are relative to the page they're on: `../assets/img/foo.png` from a page in `docs/guide/` or `docs/labs/`, and `assets/img/foo.png` from `docs/README.md`.

The link check in `.github/workflows/docs-link-check.yml` follows the same rules.

## Pedagogy checklist

- Say what the student will do in their own terms ("You'll synthesize a counter and inspect the netlist").
- Assume the student has cloned this repo. Courses that need EDA tools (LibreLane, SKY130, IIC-OSIC-TOOLS) run in the shared [workspace](https://github.com/uoftasic/workspace) that students set up in IC101. Point to IC101 for that setup, and document the steps specific to your course in the course, such as `mod add <course-id>` (the workspace command that clones a course into it). Don't invent a one-off container setup or bundle Docker in every lab unless the course already does.
- Keep steps copy-pasteable: `cd`, install, simulate or synthesize, check the output.
- End every lab part with an expected result (a printout, a waveform check, an area or timing ballpark, a golden hash) so students know they succeeded.
- Raise the difficulty from lab to lab, and reuse naming and directory conventions so later labs feel familiar.
- Prefer small, inspectable designs over opaque blobs. When you use IP or PDK files, keep secrets and huge binaries out of git.

## Writing style

- Write in the second person, in plain and friendly language, for a 2nd–3rd year ECE student. Short sentences for facts, longer ones for reasoning.
- Headers are labels ("Load lines", "Part 2: Sweep V_GS"), not verdicts.
- Use bold only for a term where it's defined, or for a real warning. Use em dashes rarely.
- Say each thing once. Don't cut numbers, caveats, warnings or troubleshooting to make a page shorter.

## Tooling

- Python helpers and graders go under `labs/<id>/src/` or `scripts/`. List entry points in the nearest `README.md`.
- SystemVerilog/Verilog goes under `labs/<id>/src/`, or `rtl/` and `tb/` if you split them. Stay consistent within the course.
- Heavy outputs (GDS, large FSDB/VCD, PDK caches) go in a local `results/` or in LFS, never under `docs/`.
- Preview the site locally with `npx docsify-cli serve docs`, then open http://localhost:3000.

## Don't

- Don't add maintainer-only pages to the published site (contributing guides, template notes, notation stubs "for debugging").
- Don't put solution keys or rubrics in `docs/`.
- Don't replace student-facing content with template or bootstrap instructions. Point people at `CONTRIBUTING.md` or `TEMPLATE.md` only when they're bootstrapping a repo or changing its conventions.
- Don't change the org assumptions: the GitHub org is `uoftasic`, and the course id matches the repo name.

## Quick references

- Repo conventions: `CONTRIBUTING.md`
- Bootstrap tokens and Pages checklist: `TEMPLATE.md`
- Sample lab: `labs/lab-01/` and `docs/labs/lab-01-overview.md`
