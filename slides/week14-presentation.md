---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 14: Presentation

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Presentation day. No new concept to teach today. Keep the slide
portion under 45 minutes so most of the 150-minute block stays with the
student teams. Close remaining gaps live, during Q&A, not on slides.
-->

---

<!-- SLOT 2: Where we are -->

# Where We Are

<div class="roadmap">
<div class="wk"><div class="n">Wk 1</div><div class="t">Introduction</div></div>
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
<div class="wk now"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

---

<!-- Recap + open wound, one slide, light-deck style -->

# Last Week's Limit, Today's Answer

<div class="thread">Week 13 named parallel techniques. It could not show you one running.</div>

<div class="limits">
We can name parallel techniques, pipelining, superscalar execution,
multicore, SIMD, but we have not yet seen them working in one real,
current design.
</div>

Today, your team closes that gap. You each bring one real chip or
system, and point at exactly where its parallelism lives.

---

<!-- Section divider -->

<!-- _class: section -->

# Today: You Present

<div class="driving-q">"Where does parallelism actually show up, in something real?"</div>

---

# What to Present

1. **Pick one real, current chip or system:** a phone chip, a laptop
   chip, a GPU, a game console, a cloud server
2. **Name its parallel techniques:** pipelining, superscalar, multicore,
   SIMD, multithreading, or GPU-style parallel execution
3. **Point to evidence:** a spec sheet, a die photo, or a benchmark that
   shows the technique is really there
4. **Say why it matters:** what a user actually gains, speed, battery
   life, or lower cost

<div class="why">
Use this semester's words on purpose: ISA, microarchitecture, pipeline,
cache, core, throughput. This is graded, see the rubric ahead.
</div>

---

# Presentation Schedule

<div class="thread">Eight teams, one 150-minute block. Order is posted on LMS before class.</div>

| Segment | Time | Content |
|---|---|---|
| Opening (this deck) | ~40 min | Recap, logistics, rubric |
| Teams 1-4 | ~48 min | 12 min each |
| Break | 5 min | Stretch, reset the room |
| Teams 5-8 | ~48 min | 12 min each |
| Wrap-up | ~5 min | Instructor closes remaining gaps |

Arrive on time. A missed slot cannot be rescheduled during class.

---

# Time Budget Per Team

- **12 minutes total:** 8 minutes presenting, 4 minutes questions
- **Every team member speaks.** Silent members lose clarity points
- A timer runs visibly at the front. At 8 minutes, questions start,
  finished or not
- Practice out loud beforehand. Most teams run long on a first try

---

<!-- Grading rubric table -->

# Grading Rubric

| Criterion | Weight | What we are looking for |
|---|---|---|
| Clarity | 25% | Could a classmate with no notes follow your explanation? |
| Technical accuracy | 35% | Is the parallel technique named and described correctly? |
| Vocabulary use | 15% | Do you use this semester's terms, and use them correctly? |
| Q&A handling | 25% | Do you answer directly, and admit it when you are unsure? |

<div class="why">
Full point breakdown: <a href="../materials/week14/presentation-rubric.md">materials/week14/presentation-rubric.md</a>
</div>

---

# Rubric, in Plain Words

<div class="two-col">
<div>

**Vocabulary use**
Say "pipeline," not "the steps thing."
Say "multicore," not "many chips."
Correct terms, correctly applied.

</div>
<div>

**Q&A handling**
Answer the question asked, not a
different one. "I'm not sure, but
here's my best guess" beats a
confident wrong answer.

</div>
</div>

Both criteria reward honesty and precision over polish.

---

# Presentation Tips

- **Explain the technique, don't just list features.** "It has 8 cores"
  is a fact. "8 cores means 8 instruction streams run at once" is
  understanding
- **Don't read your slide word for word.** Look at the class, not the
  screen
- **Rehearse your timing out loud, once, before class**
- **Prepare one backup answer** for the question you hope no one asks

---

# What to Bring

- Your slides on a USB drive, and on a laptop as backup
- A cloud copy (Google Slides or OneDrive link) in case the USB fails
- One printed page listing your sources, in case a link fails live
- Notebook and pen, to note good questions from other teams' Q&A

---

<!-- Closing loop -->

# Closing the Loop

<div class="thread">Back to Week 13's exact words, now answered by your own team.</div>

Week 13 left one thing unsolved: parallel techniques named on paper, not
yet seen in a real, current design. Every team today closes that gap
once, for one real chip, with real evidence.

---

# Next Week: Final Exam

Week 15 is a **short review week**, covering Weeks 1 through 14, no new
material. Format: instructor-led review, then the final exam itself.

<div class="why">
<strong>Prepare:</strong> re-read every week's Summary slide. Bring the
questions your own presentation's Q&A left unanswered.
</div>

---

# Summary

- No new concept today. Your presentations are the concept, applied to a
  real, current design
- Twelve minutes per team, graded on clarity, accuracy, vocabulary, and
  Q&A handling
- Full rubric: [materials/week14/presentation-rubric.md](../materials/week14/presentation-rubric.md)
- **Prepare for Week 15:** review every week's Summary slide as your
  final-exam outline

---

<!-- _class: end -->

# Thank You
