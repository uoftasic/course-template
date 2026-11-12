# Getting started

<!--
  Template sample of a guide page. Guide pages are for reading: concepts,
  figures, worked examples and the reasoning behind them. They have no
  commands the student must run. When a page needs the student to run or
  build something, put that in a lab writeup as a numbered step and leave a
  one-line pointer here. Replace this page with your course's first reading.
-->

This page explains how the course is laid out and how its pages show math and figures. Read it before [Lab 01](labs/lab-01-overview.md).

## How the course is laid out

The [course path](README.md) on the home page lists every page in the order you should work through them. Each row is one of two kinds:

- A *Read* row points to guide pages like this one. They explain the ideas with figures and worked examples. You don't need a terminal open to read them.
- A *Do* row points to a lab writeup. Labs are where you run things. Each lab is split into numbered parts, and each part ends with what you should see if it worked.

The files a lab runs (code, data and checkers) are in the course's [GitHub repo](https://github.com/uoftasic/{{COURSE_ID}}) under `labs/`. This site only has the writeups. You'll run your first script, `labs/lab-01/src/main.py`, in [Lab 01](labs/lab-01-overview.md), Part 2.

## Math and figures

<!--
  Template sample: shows that MathJax and images render. Images live in
  docs/assets/img/. Replace this section with your own content.
-->

Math is typeset with MathJax. Inline math sits in the sentence, like $y[n] = x[n] * h[n]$ for discrete convolution. Display math gets its own line:

$$
y[n] = x[n] * h[n] = \sum_{k=-\infty}^{\infty} x[k]\, h[n-k]
$$

Figures look like this:

![Sample figure](../assets/img/sample-figure.png)

## Check yourself

1. Which kind of course path row has you run commands?
2. Where are the files that a lab runs?
