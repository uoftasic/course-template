# CI for a course's reference solutions

A course whose labs have a starter, a reference solution and a checker should run all three in CI.
This page says what to check, how to set the job up, and what it costs, with two courses as worked
examples: DD105-A, whose labs build UVM testbenches with Verilator in the 11.7 GB workbench image,
and PB101, whose labs check KiCad boards in KiCad's own image.

Nothing on this page goes on the course site. The workflow lives in `.github/workflows/labs.yml`,
next to `site.yml`.

## What CI catches

A lab's expected outputs and its checker are known to be right only as of the last time someone
ran them. These are the ways they go wrong between runs:

- An edit to one lab breaks the next one. In DD105-A each lab's starter from Lab 03 on is the
  previous lab's solution, so a fix in one lab's files has to reach the next lab's starter as well.
- A change to a shared checker or makefile changes a verdict in a lab nobody opened.
- Something outside the repo moves: an image tag that now points somewhere else, a pinned commit
  or image digest that its host stops serving, or a change to GitHub's runners.

Running every reference solution by hand takes too long to do after every change: the local
rehearsal of DD105-A's checks took 30 minutes with an empty build cache.

## The checks

Check each lab from both sides, the way a student's work is graded:

| Check | Must give | Why both |
|---|---|---|
| the reference solution's check | PASS | the solution still does the lab |
| the starter's check | FAIL, for the reason the lab intends | a check that also passes the untouched starter grades nothing |
| the checker's own self-test, if it has one | PASS | proves each verdict class still fires on known inputs, so a broken checker can't report every lab as passing |

Make the starter's FAIL specific. DD105-A's labs plant bugs in a design, and the starter's test
misses the lab's bug, so CI requires the verdict `VERDICT: FAIL -- your test passes <bug> too.` A
starter that fails because its build broke, or because its test fails on the correct design, fails
CI instead.

Run the solution the way its `solutions/README.md` tells a student to, so CI tests those
instructions too. DD105-A copies each file in a lab's `solutions/` over its namesake in `tb/`,
runs `make check`, and puts the starter's files back; Lab 07's solution has its own Makefile and
runs from its own folder.

Add anything the course as a whole depends on. DD105-A also runs its reference environment, which
must catch all 15 planted bugs, and PB101 runs its board checker on four boards whose verdicts are
known before it checks any lab.

## Running the checks in the course image

**Use the course's image, pinned by digest.** A tag can be moved to another image, while a digest
names exactly one, so pinning the digest makes CI run the same tool versions that every expected
output on the course's pages came from. DD105-A pins
`hpretl/iic-osic-tools@sha256:3c371645…` in the workflow's `env`, and PB101 keeps
`kicad/kicad:10.0.8@sha256:3f4a0178…` in `labs/common/kicad-image.txt`, which its wrapper reads.

**Run the image the way students do.** Use `docker run` from a script rather than the job's
`container:` setting, and pass the user and limits students have:

- PB101's `labs/common/kicad.sh` runs KiCad as your own uid with the image's default library
  tables. Its workflow's comments give the reason: run as root with no library tables, the same
  board gives different warning counts (the SKY130 breakout's ERC warnings go from 103 to 236).
- DD105-A's `scripts/ci/in-image.sh` runs with `--cpus 2 --memory 3g` and your uid and gid, the
  limits every time on its pages was measured with. A CI time then compares with the pages, and a
  build that outgrows 3 GB fails in CI as it would for a student.

**Put every step in a script, and call it from the workflow.** Then each step is one command that
you can run on your own machine with Docker to rehearse it. DD105-A's steps are all
`scripts/ci/in-image.sh scripts/ci/check-labs.sh <step>`, and PB101's are
`labs/common/kicad.sh python3 <script>`. Rehearse every step before you push the workflow.

**Make room for a big image.** GitHub documents 14 GB of SSD for its standard Linux runners
(`ubuntu-latest` and `ubuntu-24.04`), for public and private repositories alike. DD105-A's image is
3.76 GB to download and 11.7 GB unpacked, so its workflow first runs
`jlumbroso/free-disk-space`, pinned by commit, which removes preinstalled toolchains (Android,
.NET, Haskell, and the runner's cached Docker images), and then fails with a clear message if less
than 20 GB is free. It skips that action's apt removals, which its README says are the slow part.
PB101 pulls the KiCad image without freeing anything; its wrapper gives the download as 812 MB.

**Pin every action by commit.** A tag on a third-party action can be moved to different code. Write
the tag in a comment beside the commit, as DD105-A does:
`jlumbroso/free-disk-space@54081f138730dfa15788a46383842cd2f914a1be # v1.3.1`.

**Keep going after a failure.** Give each lab its own step, with `if: success() || failure()` on
every step after the first, so one run reports every lab. DD105-A writes one `CI:` line per step
into the job summary, and uploads the failed step's logs, which its script leaves in place when a
check fails. PB101 uploads its reports on every run.

## Triggers

```yaml
on:
  push:
    branches: [main]
    paths: ["labs/**", ".github/workflows/labs.yml"]   # and anything else the labs read
  pull_request:
    paths: ["labs/**", ".github/workflows/labs.yml"]
  schedule:
    - cron: "41 6 * * 1"   # weekly
  workflow_dispatch:
```

Both examples use these triggers. DD105-A adds `third_party/**` (its UVM library) and
`scripts/ci/**` (its CI scripts) to the paths. The weekly run is the one that catches what moves
outside the repo, which no push or pull request triggers.

## Jobs and minutes

One job that runs the labs one after another is usually enough, and it pulls the image once.
Splitting the labs over several jobs makes a run finish sooner, but each job pulls the image and
frees the disk again, so the total minutes go up.

DD105-A builds 16 simulators in a run (a starter and a solution for each of seven labs, the
reference environment, and the self-test's), each of which took 82 to 123 s on 2 CPUs from cold
in the rehearsal. It keeps Verilator's ccache between runs with `actions/cache`. ccache reuses a
compiled file only when the same compiler compiles the same input again, so a restored cache saves
time without changing what is built.

| Rehearsal of DD105-A's checks, 2 CPUs and 3 GB | Time |
|---|---|
| empty ccache | 29 min 39 s |
| the ccache from the run above | 6 min 42 s, with every build taking 10 to 19 s |

GitHub's runner adds the time to free the disk and pull the image, which a local rehearsal can't
measure.

## Adding CI to a course

1. Write each lab's check so that it exits 0 on PASS and non-zero on FAIL, and prints a verdict you
   can tell apart from a crash.
2. Write a script with one step per lab: the starter's check must fail with the intended verdict,
   the solution's must pass, and the starter's files are put back afterwards.
3. Write the wrapper that runs a command in the course's image, pinned by digest, with the students'
   user and limits.
4. Rehearse every step with the same commands, and note how long the whole run takes.
5. Write `.github/workflows/labs.yml`: the triggers above, actions pinned by commit, the disk check
   if the image is big, the pull, a cache if the build tools have one, and one step per lab.
6. Add a line to the course's `README.md` that says what the workflow checks and how to run one step
   locally.

## The two workflows

- DD105-A: [`.github/workflows/labs.yml`](https://github.com/uoftasic/dd105-a/blob/main/.github/workflows/labs.yml),
  with [`scripts/ci/check-labs.sh`](https://github.com/uoftasic/dd105-a/blob/main/scripts/ci/check-labs.sh)
  and [`scripts/ci/in-image.sh`](https://github.com/uoftasic/dd105-a/blob/main/scripts/ci/in-image.sh).
- PB101: [`.github/workflows/labs.yml`](https://github.com/uoftasic/pb101/blob/main/.github/workflows/labs.yml),
  with [`labs/common/kicad.sh`](https://github.com/uoftasic/pb101/blob/main/labs/common/kicad.sh).
