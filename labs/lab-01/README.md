# Lab 01: Starter script

Starter lab package for {{COURSE_TITLE}}. It needs Python 3.10 or newer. The steps are in the writeup: [`docs/labs/lab-01-overview.md`](../../docs/labs/lab-01-overview.md), published at `https://uoftasic.com/{{COURSE_ID}}/#/labs/lab-01-overview`.

<!--
  Template: keep package READMEs short. Link to the writeup, show how to run
  the lab, list the make targets in a table if the lab has a Makefile, and
  list the files. Put the teaching in the guide pages and the writeup.
-->

## How to run

```bash
cd labs/lab-01        # from the repo root
python3 -m pip install -r requirements.txt
python3 src/main.py
```

If pip stops with `error: externally-managed-environment`, Part 1 of the writeup shows how to use a virtual environment.

## Files

| Path | What it is |
|------|------------|
| `src/main.py` | Starter entry point; prints `lab-01 ready` and a checksum. Part 3 of the writeup has you edit its message. |
| `data/` | Lab-local inputs (empty in the starter) |
| `results/` | Your local outputs, and any baseline outputs you keep to compare against (empty in the starter) |
| `requirements.txt` | Python dependencies (empty in the starter) |
