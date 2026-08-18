---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 1: Introduction

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Welcome the class. Ask: "Have you ever compared two laptops before
buying one?" A few hands will go up. Say: today we solve a real mystery
about laptops. Keep it light, this is the hook for the whole semester.
-->

---

<!-- SLOT 2: Where we are -->

# Where We Are

<div class="roadmap">
<div class="wk now"><div class="n">Wk 1</div><div class="t">Introduction</div></div>
<div class="wk"><div class="n">Wk 2</div><div class="t">Performance &amp; Cost</div></div>
<div class="wk"><div class="n">Wk 3</div><div class="t">Data Representation</div></div>
<div class="wk"><div class="n">Wk 4</div><div class="t">ISA I</div></div>
<div class="wk"><div class="n">Wk 5</div><div class="t">ISA II · Quiz 1</div></div>
<div class="wk"><div class="n">Wk 6</div><div class="t">Single-Cycle</div></div>
<div class="wk"><div class="n">Wk 7</div><div class="t">Multi-Cycle</div></div>
<div class="wk review"><div class="n">Wk 8</div><div class="t">Midterm Exam</div></div>
<div class="wk"><div class="n">Wk 9</div><div class="t">Pipelining I</div></div>
<div class="wk"><div class="n">Wk 10</div><div class="t">Pipelining II</div></div>
<div class="wk"><div class="n">Wk 11</div><div class="t">Memory Hierarchy I</div></div>
<div class="wk"><div class="n">Wk 12</div><div class="t">Memory Hierarchy II</div></div>
<div class="wk"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

<!--
notes: Point at the row. Say: fifteen weeks, one machine. We measure it,
then describe it, then build it, then make it fast. Don't explain every
word yet, just the shape.
-->

---

<!-- NEW: warm-up + Try-It for 차시 1, placed right after the roadmap (slot 2) -->

# Before We Start: Quick Pair Check

Pair up with the person next to you. Answer these together. Two minutes.

1. Write the number **13** in binary (0s and 1s only).
2. In your own words: what is a "program"?
3. True or false: a computer only understands 0s and 1s.

<div class="why">
This checks two things you already learned: <strong>binary numbers</strong>
(Digital Logic) and <strong>what a program is</strong> (Programming). We
build on both today.
</div>

<!--
notes: Give students 2 minutes to discuss in pairs, then ask ALOUD:
(1) "Who can say 13 in binary?" (answer: 1101)
(2) "What is a program, in one sentence?" (answer: a list of instructions
a computer follows, step by step)
(3) "Does a computer only understand 0s and 1s?" (answer: true, at the
lowest level; everything else is built on top of that)
If most pairs struggle, slow down today's pace and revisit binary
briefly before continuing.
-->

---

<!-- SLOT 3: What you already bring -->

# What You Already Bring

- **Digital Logic:** you already know gates and flip-flops. Today's computer is built from those same parts
- **Computer Programming:** you have written code that runs. This course opens the box underneath it
- **Data Structure:** you know arrays and pointers live "in memory." This course shows what memory really is

You are not starting from zero. You already know the pieces. This course
shows how they fit together into one real machine.

---

<!-- Course logistics appendix: administrative, outside the spine, placed here so it doesn't blunt slot 4 -->

<!-- _class: section -->

# Course Logistics
<div class="driving-q">Read once now, use all semester.</div>

---

# Grading & Materials

| Item | Weight |
|---|---|
| Attendance | 10% |
| Midterm | 30% |
| Final | 30% |
| Assignments | 10% |
| Presentation | 10% |
| In-class items | 10% |

<!-- notes: Assignment 1 is due Week 4. Assignment 2 is due Week 11. Quiz 1 is Week 5, Quiz 2 is Week 13. Week 14 is a group presentation on a real processor. -->

---

# Textbook, Policy & Contact

- **Textbook:** Hennessy & Patterson, *Computer Architecture: A Quantitative Approach*, 6th ed., 2017
- **References:** Stallings, *Computer Organization and Architecture*, 2019; Bryant & O'Hallaron, *Computer Systems*, 3rd ed., 2015
- **Policy:** come to every class and take part. Late work loses points. Cheating leads to discipline
- **Contact:** yushintia@deu.ac.kr, office hours by email

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **Clock speed (GHz):** how many times per second a chip's clock "ticks." Printed on every spec sheet
- **Spec sheet:** the list of numbers a store shows you about a device
- **Performance:** how fast a machine actually finishes real work
- **Benchmark:** a fair, repeatable test used to measure performance

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), zero jargon -->

# Two Laptops, One Confusing Afternoon

<div class="pain">

A customer walks into SmartPick, the campus electronics store. She holds
two laptop listings on her phone. Both list the exact same speed: 3.0
GHz, printed in big letters. One laptop costs more. She asks the clerk:
if the number is the same, why does one cost more?

The clerk runs the same test on both laptops: export the same video. He
starts a timer. The cheaper laptop finishes in about 4 minutes. The
expensive one finishes in about 90 seconds, less than half the time. The
number on both boxes said "3.0 GHz." He does not know why. Neither does
she.

</div>

<!--
notes: Do not say "architecture" or "microarchitecture" yet. Let the
class sit with the confusion for a moment. Ask: "Any guesses why?" Take
2-3 guesses, then move on without confirming or denying any of them.
-->

---

# The Number on the Box Was Not the Whole Story

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">Cheaper laptop, video export</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">~3 min 50 sec</div>
</div>
<div class="bar-row">
  <div class="bar-label">Expensive laptop, same export</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 38%"></div></div>
  <div class="bar-value">~1 min 25 sec</div>
</div>
</div>

Same advertised speed. More than twice the real speed. This gap is not a
mistake, and it is not marketing. It is this entire course.

<!-- notes: Let the gap between the two bars sit for a second before moving on. -->

---

<!-- SLOT 5: Cost of not knowing -->

# What Else This Actually Costs

- A student buys the wrong laptop for video editing, trusting one number on the box
- A startup rents the wrong cloud server, paying for speed it does not actually get
- A company ships a product on hardware that "should" be fast enough, then misses its deadline

<div class="why">
<strong>In industry:</strong> "why is this slow, and what would you
change" is a common interview question. It comes up for hardware and
software jobs alike. Picking the wrong processor for a datacenter can
cost a company millions of dollars a year.
</div>

---

# It Gets More Expensive the Bigger the Decision Is

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One student, one laptop</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 20%"></div></div>
  <div class="bar-value">a few hundred dollars, wasted</div>
</div>
<div class="bar-row">
  <div class="bar-label">One startup, one cloud contract</div>
  <div class="bar-track"><div class="bar-fill risk-med" style="width: 55%"></div></div>
  <div class="bar-value">real monthly budget, wasted</div>
</div>
<div class="bar-row">
  <div class="bar-label">One datacenter, wrong chip</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 92%"></div></div>
  <div class="bar-value">millions of dollars a year</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

Same mistake, three different sizes. Not knowing this **will** cost you,
at whatever scale you work.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"What actually happens, step by step, when a computer runs one line of your code?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

1. Name the layers between a line of code and the physical chip
2. Explain why the same clock speed does not mean the same real speed
3. List this semester's main topics: instructions, datapath, pipelining, memory, parallelism
4. State this course's official goals and where each one is taught

---

# This Course's Official Goals

<div class="thread">Not just this week's goals. These are the syllabus's goals for the whole course.</div>

| # | Goal (from the syllabus) | Where |
|---|---|---|
| 1 | Explain how a computer's parts work together | This week, all semester |
| 2 | Read and reason about assembly instructions | Weeks 3-5 |
| 3 | Analyze single-cycle and pipelined designs | Weeks 6-7, 9-10 |
| 4 | Evaluate cache and virtual memory designs | Weeks 11-12 |
| 5 | Explain parallelism in modern designs | Week 13 |

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Coming Up Next: Worksheet Part A

Next session, you will work in pairs on **Worksheet Part A**.

- You will see two real-looking laptop spec sheets, like the SmartPick story
- Your pair predicts: which laptop is actually faster, and why
- Then we check your prediction against the real answer together

<div class="why">
Bring your notebook. No laptop or calculator needed, just the spec
sheets we hand out.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: where did this problem come from?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **ISA (Instruction Set Architecture):** the fixed list of commands a processor understands
- **Microarchitecture:** one specific way to build a processor that supports that list
- **Transistor:** a tiny switch, on or off. Chips have billions of them
- **Cache:** small, fast memory that sits close to the processor

---

<!-- SLOT 8: Origin -->

# This Problem Is Not New

<div class="thread">You just felt the pain. Now: who else felt it, and what did the field do?</div>

- **1945:** John von Neumann describes a computer with one memory for both instructions and data. Almost every computer since, including SmartPick's laptops, still works this way
- **1965:** Gordon Moore notices that the number of transistors on a chip keeps doubling. For decades, chipmakers used this to make clock speed higher and higher

<div class="why">
Around 2004, higher clock speed made chips too hot. So chipmakers
stopped pushing speed on one core, and started adding <strong>more
cores</strong> instead. That single change is why "same GHz" no longer
means "same speed."
</div>

---

# Sixty Years, Same Question

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1945</div><div class="d">One memory<br>for code and data</div></div>
<div class="pt"><div class="dot"></div><div class="y">1965</div><div class="d">Moore's Law<br>more transistors, over time</div></div>
<div class="pt"><div class="dot"></div><div class="y">~2004</div><div class="d">The power wall<br>speed stalls, cores multiply</div></div>
<div class="pt"><div class="dot"></div><div class="y">Today</div><div class="d">Multicore, GPUs, AI chips<br>same question, still evolving</div></div>
</div>

Every era asked the same question: how do we make programs run faster?
This course teaches you to answer it with numbers, not guesses.

---

<!-- SLOT 9: Core concept -->

# Computer Architecture: Definition

<div class="thread">Sixty years of engineering point at one clear field. Here it is.</div>

> **Computer architecture** is how a computer system is designed, seen as
> three connected layers: the instruction set (what software sees), the
> microarchitecture (how it is built), and the physical hardware.

- **ISA:** the contract between software and hardware
- **Microarchitecture:** one way to build circuits that follow that contract
- **Hardware:** the actual transistors and wires on the chip

Two laptops can share the same ISA, so the same software runs on both,
while having very different microarchitectures. That gap is the mystery
from slide one.

---

<!-- Act 3 / BUILD -->

# The Abstraction Stack: What Software Sees (1/2)

<div class="thread">One definition, six layers. Here is the top half: what a programmer sees.</div>

<div class="stack">
<div class="layer view"><span class="h">Application</span> <span class="s">the video editor, the game, any app you use</span></div>
<div class="layer view"><span class="h">Operating System</span> <span class="s">runs programs, manages memory and devices</span></div>
<div class="layer logical"><span class="h">Instruction Set Architecture</span> <span class="s">the fixed set of commands: Weeks 3-5</span></div>
</div>

Everything above the ISA is software's job. Everything below it is this
course's job.

---

# The Abstraction Stack: How It's Built (2/2)

<div class="thread">The bottom half: how one ISA is actually built in silicon.</div>

<div class="stack">
<div class="layer logical"><span class="h">Microarchitecture</span> <span class="s">the circuits that run those commands: Weeks 6-10</span></div>
<div class="layer physical"><span class="h">Logic Gates</span> <span class="s">AND, OR, adders — from your Digital Logic course</span></div>
<div class="layer physical"><span class="h">Transistors</span> <span class="s">tiny switches, billions per chip</span></div>
</div>

This course mostly lives in the middle two layers. That is exactly where
the two laptops were different.

---

# Case Study: Meet the Running Example

<div class="thread">The stack above is abstract. Here is the concrete pair we return to all semester.</div>

This semester, our worked examples come back to **SmartPick's two
laptops**, "Value" and "Studio":

<div class="chip-row">
<span class="chip">Value: 3.0 GHz</span>
<span class="chip">Studio: 3.0 GHz</span>
<span class="chip">Same ISA (x86-64)</span>
<span class="chip">Different microarchitecture</span>
</div>

Week 2 gives both machines real numbers and computes exactly why Studio
wins. Later weeks reopen this same pair.

---

# Worked Example: Same Numbers, Different Result

<div class="thread">One demo, using everything from the last three slides.</div>

| Spec line | Value laptop | Studio laptop |
|---|---|---|
| Processor | 3.0 GHz, 8 cores | 3.0 GHz, 8 cores |
| Released | 2019 | 2023 |
| Cache | 8 MB | 24 MB |

Both run the same software: **same ISA**, so the ISA is not the answer.
The **released year** and **cache size** point to a different
microarchitecture. More cache means fewer slow trips to memory. We still
cannot put an exact number on the gap — that is Week 2's job.

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong>Worksheet Part A</strong>. You will see two full
spec sheets and predict which laptop is faster, and why. About 15
minutes.
</div>

- Write down your prediction and your reason
- It is OK to be unsure — write down what you do not know too
- We compare answers together at the start of 차시 3

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work. Do not confirm any answers yet, the real discussion happens next
session. If a pair finishes early, ask them to also read the "optional
reading" box on the handout.
-->

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: what does the map still not tell us?</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **Power wall:** the limit that stopped clock speed from rising forever
- **Multicore:** a chip with more than one processor core
- **Parallelism:** doing more than one piece of work at the same time
- **Trade-off:** gaining one thing (speed) by giving up another (power, cost)

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong>Worksheet Part B</strong>. Check your Part A
prediction against the real answer, then answer two new questions. About
15 minutes.
</div>

- The answer key explains **why we still cannot fully explain the gap** without Week 2's tools
- That "we cannot tell yet" feeling is exactly why this course exists

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). Let pairs self-check. After ~15 minutes, cold-call 2-3 pairs
to share their reasoning out loud before moving to the next slide.
-->

---

# Let's Look at the Whole Machine Together

<div class="thread">Before closing, connect every layer back to today's opening story.</div>

<div class="pipeline">
<div class="stage"><div class="h">Application</div><div class="s">the "export video" button</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">ISA</div><div class="s">same on both laptops</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Microarchitecture</div><div class="s">different, so different speed</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Transistors</div><div class="s">where the work happens</div></div>
</div>

Every later week zooms into one stage of this picture.

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"Higher GHz always means faster":** clock speed is only one factor. How the chip is built matters just as much
- **"Architecture is only hardware":** software design shapes real speed too, not just circuits
- **"More cores always means faster":** a task that cannot be split up gains little from extra cores. Week 13 explains why

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. Two laptops have the same clock speed but very different real speed. Give one reason, using today's words
2. Put these in order, from your code to the physical chip: microarchitecture, application, transistors, ISA, logic gates

<div class="why">
After this, take the short self-check quiz (paper or online) for more
practice. It is ungraded.
</div>

---

# Answers

1. They can share the same **ISA** but have different **microarchitectures** — one design needs fewer steps to do the same job
2. **Application -> ISA -> Microarchitecture -> Logic Gates -> Transistors**

---

<!-- SLOT 14: Limits (Act 4 / CLOSE), becomes Week 2 slot 4 -->

# What Today's Map Cannot Do Yet

<div class="limits">
We now have the words and the layered map: ISA, microarchitecture,
hardware. But we still cannot put a number on which machine is faster,
or by how much. Knowing the layers exist is not the same as measuring
them.
</div>

---

<!-- SLOT 15: Bridge -->

# Next Week

Week 1 leaves **how to measure and compare speed precisely** unsolved.
**Week 2, Performance and Cost**, solves it: CPU time, clock rate, CPI,
and Amdahl's Law. The exact tools to settle the SmartPick question with
numbers, not a stopwatch.

---

<!-- SLOT 16: Summary -->

# Summary

- Computer architecture has three layers: ISA, microarchitecture, hardware, built on logic gates and transistors
- Same clock speed does not mean same real speed, because microarchitecture can differ
- Around 2004, chip speed hit a wall, so the field moved to multicore. That is this course's final major topic
- **You did today:** warm-up quiz, Worksheet Parts A and B, self-check quiz
- **Reading:** Hennessy & Patterson, 6th ed., Chapter 1
- **Prepare:** find one real spec sheet (laptop or phone). Bring one number you cannot yet fully explain

---

<!-- SLOT 17: Thank You -->
<!-- _class: end -->

# Thank You
