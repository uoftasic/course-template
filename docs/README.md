# {{COURSE_TITLE}}

{{DESCRIPTION}}

<!--
  Template: scripts/init-template.py fills in the {{...}} tokens (see
  TEMPLATE.md). Replace the _italic_ placeholders below by hand, then replace
  the course path rows with your own guide pages and labs. AGENTS.md describes
  the course structure.
-->

- Who it's for: _one line on who should take this course._
- Prerequisites: _earlier courses or background, with links._
- Total time: _about N hours, the sum of the times in the course path._

This site has the reading and the lab writeups. The code each lab runs is in the [GitHub repo](https://github.com/uoftasic/{{COURSE_ID}}) under `labs/`. Other UofT ASIC courses are listed at [edu.uoftasic.com](https://edu.uoftasic.com/).

## Course path

Work down the table in order. A Read row is one or more guide pages: you only read, and there is nothing to run. A Do row is a lab, where you run things, make something of your own and check your results.

<!--
  Template: keep this table format in every course.
  - Read and Do are plain text, and Read and Do rows alternate in the order
    a student should work.
  - A Do row names the lab as "Lab NN: Title", the same as the lab page's
    header and the sidebar, and ends with one sentence on what you'll do.
  - Separate several guide pages in one Read row with " · ".
  - Give every row a time estimate. The row times add up to the total time
    above. Leave optional lab parts out of them.
  - Keep docs/_sidebar.md in the same order.
-->

| # | | What | Time |
|---|---|---|---|
| 1 | Read | [Getting started](guide/getting-started.md) | _N_ min |
| 2 | Do | [Lab 01: Starter script](labs/lab-01-overview.md). Run the starter Python script, then change its message and predict the new checksum. | _N_ min |
