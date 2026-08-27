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
notes: Welcome the class. Say: today is the course contract - what this
course covers, how you're graded, and what's expected of you. No
architecture yet, that starts next week.
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
notes: Point at the row. Say: fifteen weeks, one machine. Today's the
odd one out - it's about how this course works, not the machine itself.
-->

---

# Why This Course

<div class="thread">One reason, before the contract.</div>

Every app, website, and AI tool you use in the end runs on a real,
physical chip. Someone has to understand how that chip actually works,
and pick the right one for the job - that person is often paid very
well to know this. This course teaches you what is really happening
inside a computer, and how to measure "fast" and "slow" with numbers,
not guesses.

---

# Two Laptops, One Confusing Afternoon

<div class="thread">The story we return to all semester. Not solved today.</div>

A customer at SmartPick, the campus electronics store, is choosing
between two laptops. The spec sheet shows the exact same processor
speed for both. One laptop costs more than the other. She asks the
clerk: if the number is the same, why does one cost more?

Nobody in the store can answer her yet.

---

# One Question to Sit With

<div class="thread">Not answered today. Week 2 opens with this.</div>

Does a bigger number on a spec sheet always mean a faster machine?

- Think about your own phone or laptop. What number did you look at
  when you bought it?
- Was that number the whole story?

<!--
notes: A discussion prompt, not a lesson - do not answer it today. Take
a few guesses out loud, then move on without confirming or denying any
of them. Week 2 opens with exactly this question, answered with real
numbers.
-->

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Course's Question

<div class="driving-q">"What is actually happening inside a computer, and what makes one machine faster than another?"</div>

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

Every one of these five goals gets built, piece by piece, using
SmartPick's two laptops as the running illustration - not as an
abstract exercise.

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. Next: the course contract - what's covered, how you're graded, and what's expected of you.</div>

---

# Course Description

<div class="thread">From the official course plan.</div>

This course opens the box underneath the code you already know how to
write. It covers how a program becomes instructions a chip can run
(the instruction set), how a processor design - single-cycle,
multi-cycle, pipelined - carries those instructions out, and how
memory and parallel hardware make a real machine fast. Every idea ties
back to one question: what makes a real computer fast or slow?

---

# Learning Objectives

<div class="thread">The official course objectives, from the syllabus - what you'll be able to do by Week 15.</div>

By the end of this course, you can:

<style scoped>
.cardlist { gap: 10px; margin-top: 6px; }
.cardlist .card { padding: 8px 18px; }
.cardlist .card .h { font-size: 17px; margin-bottom: 2px; }
.cardlist .card .d { font-size: 15px; line-height: 1.25; }
</style>

<div class="cardlist">
<div class="card"><div class="h">Code to Hardware</div><div class="d">Explain how a line of code becomes work a physical chip performs.</div></div>
<div class="card"><div class="h">CPU Performance</div><div class="d">Compute and compare CPU performance using CPU time, CPI, and Amdahl's Law.</div></div>
<div class="card"><div class="h">Data Representation</div><div class="d">Represent numbers, text, and instructions as bits.</div></div>
<div class="card"><div class="h">Assembly</div><div class="d">Read and write basic assembly instructions.</div></div>
<div class="card"><div class="h">Processor Design</div><div class="d">Explain how a single-cycle and a multi-cycle processor design work.</div></div>
<div class="card"><div class="h">Pipelining</div><div class="d">Explain how pipelining speeds up a processor, and what can go wrong.</div></div>
<div class="card"><div class="h">Memory &amp; Parallelism</div><div class="d">Explain how cache, virtual memory, and parallelism make a modern machine fast.</div></div>
</div>

---

# Prerequisites

<div class="thread">What this course assumes you already have.</div>

- **Digital Logic**
- **Computer Programming I & II**
- **Data Structure**

We do not start from zero. If gates and flip-flops, writing working
code, or arrays and pointers feel shaky, say so early - it compounds
fast otherwise.

---

# Textbooks

<div class="thread">One primary text. Everything else is optional support.</div>

- **Primary:** Hennessy & Patterson, *Computer Architecture: A
  Quantitative Approach*, 6th ed., 2017
- **Secondary:** Stallings, *Computer Organization and Architecture*,
  2019; Bryant & O'Hallaron, *Computer Systems: A Programmer's
  Perspective*, 3rd ed., 2015
- **Also:** these lecture slides themselves are a listed course
  reference

---

# How This Course Runs

<div class="thread">What to expect from a 3-hour block, every week.</div>

Each 150-minute class is split into three 50-minute sessions (차시 1,
2, 3). Each session mixes short lectures with:

<div class="cardlist">
<div class="card"><div class="h">A warm-up</div><div class="d">a short, concrete question to start, before any jargon</div></div>
<div class="card"><div class="h">A recap</div><div class="d">what last week delivered, and what it left unsolved</div></div>
<div class="card"><div class="h">Pair and group activities</div><div class="d">work through a problem together, with the answer discussed right after</div></div>
<div class="card"><div class="h">A self-check quiz</div><div class="d">ungraded, just for you, at the end of most weeks</div></div>
</div>

You will talk in this class, not just listen.

---

# Weekly Schedule

<div class="thread">One line per week - the full walkthrough.</div>

| Wk | Topic | Wk | Topic |
|---|---|---|---|
| 1 | Introduction (today) | 9 | Pipelining I |
| 2 | Performance & Cost | 10 | Pipelining II |
| 3 | Data Representation | 11 | Memory Hierarchy I - **Assignment 2** |
| 4 | ISA I - **Assignment 1** | 12 | Memory Hierarchy II |
| 5 | ISA II - **Quiz 1** | 13 | Parallelism - **Quiz 2** |
| 6 | Single-Cycle | 14 | Presentation - **Group Presentation** |
| 7 | Multi-Cycle | 15 | **Final Exam** (Wks 9-14) |
| 8 | **Midterm Exam** (Wks 1-7) | | |

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. Next: grading, assignments, and policy.</div>

---

# Grading

<div class="thread">Six components, 100% total.</div>

| Component | Weight |
|---|---|
| Attendance | 10% |
| Midterm | 30% |
| Final | 30% |
| Assignments (×2) | 10% |
| Presentation | 10% |
| In-class items | 10% |

<div class="why">
<strong>Grade distribution guideline:</strong> A ≤30%, B ≤40%, C-F ≤30%
of the class. This may shift after the add/drop period, based on final
enrollment.
</div>

<!-- notes: Assignment 1 is due Week 4. Assignment 2 is due Week 11. Quiz 1 is Week 5, Quiz 2 is Week 13. Week 14 is a group presentation on a real processor. -->

---

# Assignments

<div class="thread">Two assignments, spaced across the semester.</div>

| # | Released | Due | Topics |
|---|---|---|---|
| 1 | Wk 2 | Wk 4 | Binary representation, instruction encoding basics |
| 2 | Wk 9 | Wk 11 | Datapath/pipelining trace, cache behavior |

---

# Feedback Policy

<div class="thread">From the course policy, verbatim.</div>

> Assignments graded within one week with rubric and model answers;
> exam item-analysis shared with weak-topic guidance and individual
> review on request.

In plain terms: you will know what you got wrong, and why, quickly
enough for it to still matter for the next assignment or exam.

---

# Attendance & Late Work

<div class="thread">Concrete rules, stated once, so nobody is surprised later.</div>

<div class="cardlist">
<div class="card"><div class="h">Attendance</div><div class="d">is 10% of your grade and is recorded every session.</div></div>
<div class="card"><div class="h">Late arrival</div><div class="d">arriving within 15 minutes of the start is on-time; after that, you're marked late. Three lates equal one absence.</div></div>
<div class="card"><div class="h">Can't attend?</div><div class="d">Email the instructor <em>before</em> the session to be marked excused - unexcused absences aren't eligible for makeup credit.</div></div>
<div class="card"><div class="h">Late work</div><div class="d">loses 10% of that assignment's grade per day late, up to 3 days. No credit after 3 days, unless arranged with the instructor in advance.</div></div>
</div>

---

# Academic Integrity

<div class="thread">Same principle as attendance: stated once, plainly.</div>

- **Academic integrity:** submit your own work. Copying another
  student's work, having someone else complete it for you, or
  submitting unattributed AI-generated work as your own is a
  violation.
- **First violation:** zero credit on that assignment or exam, plus a
  formal report. **Repeat violation:** may result in failing the
  course, per university policy.
- If anything here is unclear, ask - now is the cheapest time to ask.

---

# Support for Students with Disabilities

<div class="thread">From the syllabus's accommodations section.</div>

- **Hearing-impaired:** front-row seating, lecture material files
  provided where possible, urgent notices given in writing
- **Mobility-impaired:** extended exam time
- **Other documented conditions:** extended exam time, materials
  provided in advance, enlarged exam copies, or other reasonable
  accommodation based on need

Contact the instructor early, and the Disability Student Support
Center or Academic Affairs Team, so accommodations are ready before
you need them.

---

# Contact

<div class="thread">How to reach the instructor.</div>

- **Email:** yushintia@deu.ac.kr
- **Office hours:** by appointment, email first
- Email is the fastest way to reach the instructor outside of class.

---

<!-- SLOT N+1: Limits (Act 4 / CLOSE), reused verbatim in Week 2's slot 3 recap and echoed in its slot 4 pain slide - see SPINE.md's orientation-variant note -->

# What Today Doesn't Give You Yet

<div class="limits">
You now know how this course runs, how you're graded, and what's
expected of you. You also met SmartPick's two laptops - same spec
sheet, one clearly slower in real use - and we still do not know why.
Knowing the rules of the course is not the same as knowing why the
spec sheet did not tell the whole story.
</div>

---

<!-- SLOT N+2: Bridge -->

# Next Week

Week 1 leaves **why the spec sheet did not tell the whole story**
unsolved. **Week 2, Performance and Cost**, starts to answer it: real
numbers for how fast a machine actually runs, so "faster" stops being
a guess.

---

<!-- SLOT N+3: Summary -->

# Summary

- This course: how a program becomes real work inside a physical chip
  - instructions, datapath, pipelining, memory, parallelism - one
  semester, one machine.
- Grading: Attendance 10%, Midterm 30%, Final 30%, Assignments 10%,
  Presentation 10%, In-class items 10%.
- Assignments due Weeks 4 and 11. Quizzes in Weeks 5 and 13. Group
  presentation in Week 14.
- Primary text: Hennessy & Patterson, 6th ed. Contact:
  yushintia@deu.ac.kr.
- **Prepare:** think of one laptop, phone, or computer spec sheet you
  have seen. Bring one number you are not fully sure you understand.

---

<!-- SLOT N+4: Thank You -->
<!-- _class: end -->

# Thank You
