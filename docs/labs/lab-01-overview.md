# Lab 01

<!--
  Template sample of a lab writeup. The writeup is the one place where
  students do things. Keep this shape: two or three lines on what they'll
  build or measure, before you start, time, numbered parts with numbered
  steps (each part ends in a "you should see" check), then finishing. Put
  each question at the step where it comes up.
-->

You'll run a starter Python script and check what it prints. The script and the other files for this lab are in [`labs/lab-01/`](https://github.com/uoftasic/{{COURSE_ID}}/tree/main/labs/lab-01) in the course repo.

## Before you start

- Read [Getting started](guide/getting-started.md).
- You need Python 3.10 or newer and a clone of the course repo:

  ```bash
  git clone https://github.com/uoftasic/{{COURSE_ID}}.git
  ```

- This starter only needs Python. Labs that use the EDA tools (IIC-OSIC-TOOLS) run in the shared [workspace](https://github.com/uoftasic/workspace) you set up in [IC101](https://uoftasic.com/ic101/).

Time: about _N_ minutes.

## Part 1: Set up the lab package

1. From the root of your clone, go to the lab folder:

   ```bash
   cd labs/lab-01
   ```

2. Install the lab's Python dependencies:

   ```bash
   python3 -m pip install -r requirements.txt
   ```

You should see pip finish without an error. The starter's `requirements.txt` has no packages in it, so nothing gets installed.

If pip stops with `error: externally-managed-environment`, your system Python doesn't let pip install into it (the system Python on Ubuntu 24.04 does this). Make a virtual environment in the lab folder and run the install inside it:

```bash
python3 -m venv .venv      # on Ubuntu, install the python3-venv package first
. .venv/bin/activate
python3 -m pip install -r requirements.txt
```

## Part 2: Run the starter

1. Open `src/main.py`. Which function works out the number the script prints after `checksum=`?

2. Run the script:

   ```bash
   python3 src/main.py
   ```

You should see:

<!-- Template: replace this with your lab's own known-good output. -->

```text
lab-01 ready
checksum=13
```

## Finishing

You're done when `python3 src/main.py` prints the two lines in Part 2. There is nothing to submit for this lab.

Outputs from a lab go in its `results/` folder (here `labs/lab-01/results/`), never in `docs/`.
