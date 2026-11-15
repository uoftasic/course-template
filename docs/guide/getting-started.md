# Getting started

<!--
  Template sample of a guide page. Guide pages are for reading: concepts,
  figures, worked examples and the reasoning behind them. They have no
  commands the student must run. When a page needs the student to run or
  build something, put that in a lab writeup as a numbered step and leave a
  one-line pointer here. Replace this page with your course's first reading.
-->

This page explains how the course is laid out and how its pages show math and figures. Read it before [Lab 01: Starter script](../labs/lab-01-overview.md).

## Course layout

The [course path](../index.md#course-path) on the home page lists every page in the order you should work through them. Each row is one of two kinds:

- A Read row points to guide pages like this one, which explain the ideas with figures and worked examples. You don't need a terminal open to read them.
- A Do row points to a lab writeup, and the labs are where you run things.

The files a lab runs (code, data, and any scripts that check your results) are in the course's [GitHub repo](https://github.com/uoftasic/{{COURSE_ID}}) under `labs/`, and this site has only the writeups. You'll run your first script, `labs/lab-01/src/main.py`, in [Lab 01](../labs/lab-01-overview.md), Part 2.

## Lab structure

Each lab is split into numbered parts with numbered steps. Most parts open with the question they answer, and the steps then work out the answer. Each part has a "You should see" check, which tells you whether what you did worked. In at least one part you make something yourself, such as editing a file, writing a test, or working out a number before a script or tool prints it.

Some steps ask you to write down what you expect before you run something. Write your prediction down first, so that you have something to compare the result with.

When a step asks a question, its answer is in a collapsed block right under it. Try to answer the question yourself first, and then click "Answer" to open the block. The questions in Check yourself at the end of this page work the same way.

A part marked "(optional)" comes after all the required parts. You can skip it, because no later part needs it and the lab's time estimate doesn't include it.

Every lab ends with a Finishing section. It tells you how to know you're done, asks any questions that you can answer from your own work, and says what to submit, if anything. The last line of each lab points to the next row on the course path.

## Math and figures

<!--
  Template sample: shows that MathJax and images render. Images live in
  docs/assets/img/. Replace this section with your own content.
-->

Math on these pages is typeset with MathJax. Inline math sits inside the sentence, like $y[n] = x[n] * h[n]$ for discrete convolution, and display math gets a line of its own:

$$
y[n] = x[n] * h[n] = \sum_{k=-\infty}^{\infty} x[k]\, h[n-k]
$$

Figures look like this:

![Sample figure](../assets/img/sample-figure.png)

## Check yourself

1. Which kind of course path row has you run commands?

   <details>
   <summary>Answer</summary>

   A Do row, which points to a lab writeup. The labs are where you run things.

   </details>

2. Where are the files that a lab runs?

   <details>
   <summary>Answer</summary>

   They're in the course's GitHub repo, under `labs/`. This site has only the writeups.

   </details>
