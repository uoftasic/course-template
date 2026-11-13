# Lab 01: Starter script

<!--
  Template sample of a lab writeup, the one place where students do things.
  Keep this shape (AGENTS.md has the details):
  - Two or three lines on what they'll build or measure, then Before you
    start, then the time.
  - Numbered parts with numbered steps. Open each part with the question it
    answers and end it with a "You should see" check.
  - At least one required part where the student makes something: edits a
    file, writes a test, draws a cell, or works out a number before the tool
    prints it (Part 3 here).
  - Prediction steps where the student can reasonably predict. When a check
    would also explain why, ask it as a question and put the answer in a
    collapsed <details> block under it.
  - Optional parts after the required ones, marked "(optional)", with their
    time given separately.
  - Finishing: You're done when, Questions, Submit. Then Going further
    (optional), if any, and the "Next on the Course path" line.
  Copy every expected output from a real run.
-->

You'll run a starter Python script, then change the message it prints and predict what happens to its checksum. The script and the other files for this lab are in [`labs/lab-01/`](https://github.com/uoftasic/{{COURSE_ID}}/tree/main/labs/lab-01) in the course repo.

## Before you start

- Read [Getting started](guide/getting-started.md).
- You need git, Python 3.10 or newer, and a clone of the course repo:

  ```bash
  git clone https://github.com/uoftasic/{{COURSE_ID}}.git
  ```

- This starter only needs Python. Labs that use the EDA tools (IIC-OSIC-TOOLS) run in the shared [workspace](https://github.com/uoftasic/workspace) you set up in [IC101](https://uoftasic.com/ic101/).

Time: about _N_ minutes, plus _N_ minutes for the optional Part 4.

## Part 1: Set up the lab package

<!--
  Template: if your course runs on the workbench, Lab 01 Part 1 is
  "Load the course" instead. AGENTS.md says what goes in it.
-->

1. From the root of your clone, go to the lab folder:

   ```bash
   cd labs/lab-01
   ```

2. Install the lab's Python dependencies:

   ```bash
   python3 -m pip install -r requirements.txt
   ```

   If pip stops with `error: externally-managed-environment`, your system Python doesn't let pip install into it (the system Python on Ubuntu 24.04 does this). Make a virtual environment in the lab folder and run the install inside it:

   ```bash
   sudo apt install python3-venv   # Ubuntu only: python3 -m venv needs this package
   python3 -m venv .venv
   . .venv/bin/activate
   python3 -m pip install -r requirements.txt
   ```

   If you open a new terminal later in the lab, run `. .venv/bin/activate` in it again.

   You should see pip finish without an error. The starter's `requirements.txt` has no packages in it, so pip doesn't install anything.

## Part 2: Run the starter

What does the starter print, and where does its checksum come from?

1. Open `src/main.py`. Which function works out the number the script prints after `checksum=`, and how?

   <details>
   <summary>Answer</summary>

   `checksum()`. It adds up the character code of each character in the message (`ord(c)`) and keeps the remainder after dividing the total by 997 (`% 997`).

   </details>

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

## Part 3: Change the message

What happens to the checksum when the message gets shorter?

1. In `src/main.py`, change `ready` to `done` in the line `message = "lab-01 ready"`. Keep the four spaces at the start of the line, or Python stops with an `IndentationError`. The line should now read:

   ```python
       message = "lab-01 done"
   ```

2. `done` is one character shorter than `ready`. Before you run the script, write down whether you expect the new checksum to be bigger or smaller than 13.

3. Run the script again:

   ```bash
   python3 src/main.py
   ```

   You should see:

   ```text
   lab-01 done
   checksum=899
   ```

4. Compare the result with your prediction. The message got shorter, so why did the checksum go up?

   <details>
   <summary>Answer</summary>

   The character codes of `lab-01 ready` add up to 1010, and those of `lab-01 done` add up to 899. 1010 is more than 997, so the old checksum was the remainder, $1010 - 997 = 13$. 899 is less than 997, so the new checksum is 899 itself.

   </details>

## Part 4 (optional): Swap two characters

Can this checksum tell when two characters swap places? No later part needs this one.

1. Your Part 3 message with the `0` and `1` swapped is `lab-10 done`. Before you run anything, write down what you expect its checksum to be.

2. From `labs/lab-01`, run `checksum()` on the swapped message. `PYTHONPATH=src` lets Python find `main.py` in `src/`.

   ```bash
   PYTHONPATH=src python3 -c 'from main import checksum; print(checksum("lab-10 done"))'
   ```

   You should see `899`, the same checksum as `lab-01 done` in Part 3.

3. Why didn't the checksum change?

   <details>
   <summary>Answer</summary>

   Addition doesn't depend on order, so the same characters in any order add up to the same total and give the same checksum. A checksum that only adds character codes can't catch two characters swapping places.

   </details>

## Finishing

You're done when `python3 src/main.py` prints `lab-01 done` and `checksum=899`, from your edit in Part 3.

### Questions

1. Your Part 3 message gives `checksum=899`. What character code would one more character at the end of the message need, to make the checksum 0?

   <details>
   <summary>Answer</summary>

   A character with code 98. The total becomes $899 + 98 = 997$, and the remainder after dividing 997 by 997 is 0. Code 98 is `b`, so `message = "lab-01 doneb"` prints `checksum=0`.

   </details>

### Submit

Nothing to submit.

This starter doesn't write any files. When a lab does write large outputs, such as GDS files or waveform dumps, keep them in its `results/` folder (here `labs/lab-01/results/`) and out of `docs/`. Use Git LFS if you need to share them.

<!--
  Template: extra reading or experiments that no part depends on go under
  "## Going further (optional)" here, before the Next line.
-->

Next on the [Course path](README.md#course-path): _the next row, with links to its guide pages or lab._
