---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 9: Pipelining I

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Welcome the class back from the midterm. Ask: "What was the one
thing our multi-cycle chip still could not do?" Let a student answer in
their own words. Today we remove that exact limit.
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
<div class="wk now"><div class="n">Wk 9</div><div class="t">Pipelining I</div></div>
<div class="wk"><div class="n">Wk 10</div><div class="t">Pipelining II</div></div>
<div class="wk"><div class="n">Wk 11</div><div class="t">Memory Hierarchy I</div></div>
<div class="wk"><div class="n">Wk 12</div><div class="t">Memory Hierarchy II</div></div>
<div class="wk"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

<!--
notes: Point at Week 7 and Week 9. Say: the midterm covered everything up
through multi-cycle. Today we start the second half: making the chip do
more than one thing at once.
-->

---

<!-- SLOT 3: Recap + open wound -->

# Last Week, This Week

- **Last week delivered:** Week 8's midterm review confirmed a working, tested chip, covering every layer through multi-cycle design
- **Last week left broken:** multi-cycle saves time per instruction type, but the processor still does only one thing at a time

<div class="why">
That second line is Week 7's limit, carried straight through the
midterm. We are not fixing a small bug. We are removing that whole
limit.
</div>

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **Pipelining:** running several instructions at once, overlapped in different stages
- **Stage:** one small step of an instruction's work, done by one part of the chip
- **Throughput:** how many instructions finish per unit of time, on average
- **Latency:** how long one single instruction takes, start to finish
- **Overlap:** starting a new instruction before the previous one fully finishes

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), zero jargon -->

# One Instruction Finishes Before the Next One Starts

<div class="pain">

SmartPick's engineers just finished testing the Studio laptop's chip
from last week. Each instruction now takes only the steps it truly
needs.

But a real program still crawls. The engineers watch the chip, tick by
tick. While one instruction gets its values, the part that does math
sits idle. While the next instruction does its math, the part that gets
values sits idle instead.

The processor still does only one thing at a time. Most of the chip does
nothing, at almost every tick.

</div>

<!--
notes: Let this land. Ask: "Why would a chip leave most of itself doing
nothing?" Take 2-3 guesses without confirming any yet. This mirrors
Week 7's Limit slide almost word for word — say that out loud if it
helps students connect the two weeks.
-->

---

# Watch the Chip, Cycle by Cycle

- Tick 1: the chip gets the instruction. Every other part sits idle
- Tick 2: the chip gets the values it needs. The part from tick 1 now sits idle
- Tick 3: the chip does the math. Everything else sits idle
- Tick 4: the chip saves the answer. Everything else sits idle again

<div class="why">
Four working parts. Never more than one busy at the same tick. That is
today's whole problem, seen tick by tick.
</div>

---

<!-- SLOT 5: Cost of not knowing -->

# What Not Overlapping Instructions Actually Costs

- A real program with millions of instructions still runs slow, no matter how well each step is tuned
- A company's product feels sluggish, so customers switch to a rival's faster chip
- A student who cannot explain overlap-based speedup struggles with a standard hardware interview question

<div class="why">
<strong>In industry:</strong> "walk me through how your CPU overlaps
instructions" is a standard question for chip-design roles. Every modern
processor, phone to server, overlaps instructions this way.
</div>

---

# The Idle-Chip Problem Gets Bigger at Scale

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One student's toy program</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 20%"></div></div>
  <div class="bar-value">a few wasted seconds</div>
</div>
<div class="bar-row">
  <div class="bar-label">One company's shipped product</div>
  <div class="bar-track"><div class="bar-fill risk-med" style="width: 55%"></div></div>
  <div class="bar-value">unhappy customers, lost sales</div>
</div>
<div class="bar-row">
  <div class="bar-label">One data center, billions of requests</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 92%"></div></div>
  <div class="bar-value">huge wasted electricity and money</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

Same idle-chip waste, repeated billions of times a day, adds up fast.

---

# Who Builds This, As a Job

<div class="thread">This overlap idea is now a whole category of real engineering jobs.</div>

<div class="appgrid">
<div class="app"><div class="name">Computer Architect</div><div class="desc">decides how many pipeline stages a chip should have</div></div>
<div class="app"><div class="name">Digital Design Engineer</div><div class="desc">builds the pipeline registers and stage circuits</div></div>
<div class="app"><div class="name">Verification Engineer</div><div class="desc">tests that overlapped instructions still finish correctly</div></div>
<div class="app"><div class="name">Performance Engineer</div><div class="desc">measures real speedup on real programs, not just the ideal number</div></div>
</div>

These four jobs all exist because overlapping instructions safely is genuinely hard to get right.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"Can a processor start a new instruction before the last one finishes, without breaking anything?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

<div class="cardlist">
<div class="card"><div class="h">Throughput vs. Latency</div><div class="d">Explain why overlapping instructions raises throughput, even though one instruction still takes the same time</div></div>
<div class="card"><div class="h">Five Pipeline Stages</div><div class="d">Name the stages of a classic five-stage pipeline and what each stage does</div></div>
<div class="card"><div class="h">Pipeline Speedup</div><div class="d">Compute a pipeline's speedup for a simple program, given its instruction and stage counts</div></div>
<div class="card"><div class="h">Hazard Preview</div><div class="d">Identify why overlapping instructions can produce wrong answers, without solving it yet</div></div>
</div>

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Coming Up Next: Worksheet Part A

Next session, you will work in pairs on
**[Worksheet Part A](materials/week09/worksheet.html)**.

- You will see a small program run two ways: one instruction at a time, and overlapped
- Your pair predicts how many ticks each way takes
- We check your prediction once the mechanics start

<div class="why">
Bring your notebook. No calculator needed, just simple counting.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: who first overlapped work like this, and why?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **Fetch (IF):** the stage that gets the next instruction from memory
- **Decode (ID):** the stage that figures out what the instruction means and reads its values
- **Execute (EX):** the stage that does the math or comparison
- **Pipeline register:** a small holding spot between two stages, so results do not get mixed up
- **Fill time:** the first few ticks, while the pipeline is still filling up with instructions

---

<!-- SLOT 8: Origin -->

# This Overlap Idea Is Not New

<div class="thread">You just felt the pain. Now: who solved it first, and how?</div>

- **1913:** Henry Ford's car factory splits work into stations on a moving line. Every station works on a different car at the same time
- **1959:** IBM's Stretch computer becomes one of the first to overlap instruction steps in hardware, copying that same factory idea
- **1964:** the CDC 6600 refines the idea into a fast, reliable design

<div class="why">
Engineers did not invent a brand-new trick here. They copied a working
factory idea and built it into a chip.
</div>

---

# From Factory Floor to Every Modern Chip

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1913</div><div class="d">Moving assembly line<br>one station, one job, always overlapped</div></div>
<div class="pt"><div class="dot"></div><div class="y">1959</div><div class="d">IBM Stretch<br>first hardware to overlap instruction steps</div></div>
<div class="pt"><div class="dot"></div><div class="y">1964</div><div class="d">CDC 6600<br>overlap becomes fast and reliable</div></div>
<div class="pt"><div class="dot"></div><div class="y">Today</div><div class="d">Every phone and laptop chip<br>pipelining is now the default design</div></div>
</div>

Same idea, sixty years later: split the work, overlap the stations,
finish more each second.

---

<!-- SLOT 9: Core concept -->

# Pipelining: Definition

<div class="thread">One factory idea, sixty years old. Here is its formal name in computing.</div>

> **Pipelining** is a hardware technique that splits an instruction's
> work into stages, so several instructions can be in different stages
> at the same time.

- **Stage:** one small, independent piece of the work, done by its own part of the chip
- **Overlap, not shortcut:** one instruction still passes through every stage — pipelining skips no steps
- **Throughput goes up:** more instructions finish per second, even though each one still takes the same number of stages

---

<!-- Act 3 / BUILD -->

# Pipelines Are Everywhere, Not Just Chips

<div class="thread">Once you see one pipeline, you start noticing them everywhere.</div>

<div class="appgrid">
<div class="app"><div class="name">Car wash</div><div class="desc">wash, rinse, dry — different cars at each station, all at once</div></div>
<div class="app"><div class="name">Fast-food drive-through</div><div class="desc">order, pay, pick up — three windows, three cars, overlapped</div></div>
<div class="app"><div class="name">Laundromat</div><div class="desc">wash, dry, fold — one load per stage, several loads in progress</div></div>
</div>

Same shape every time: split the work, give each station its own step,
keep every station busy.

---

# Five Stages for Every Instruction

<div class="thread">The classic pipeline design splits work into five named stages.</div>

<div class="pipeline">
<div class="stage"><div class="h">Fetch (IF)</div><div class="s">get the instruction from memory</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Decode (ID)</div><div class="s">figure out what it means, read its values</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Execute (EX)</div><div class="s">do the math or comparison</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Memory (MEM)</div><div class="s">read or write data, if needed</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Write Back (WB)</div><div class="s">save the result where it belongs</div></div>
</div>

Every instruction passes through all five stages, one stage per tick.

---

# One Station per Tick, Five Instructions at Once

<div class="thread">Now put several instructions on the line together.</div>

| Tick | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| Instr 1: `add` | IF | ID | EX | MEM | WB | – | – |
| Instr 2: `lw` | – | IF | ID | EX | MEM | WB | – |
| Instr 3: `beq` | – | – | IF | ID | EX | MEM | WB |

Instruction 1 still takes five ticks, start to finish, same as before.
But instruction 3 finishes by tick 7, not tick 15.

---

# Throughput vs. Latency, Side by Side

<div class="thread">Two different measurements, two different results from the same change.</div>

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One instruction's own time (latency)</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 50%"></div></div>
  <div class="bar-value">500 ns, before and after</div>
</div>
<div class="bar-row">
  <div class="bar-label">Instructions finishing per microsecond (throughput)</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">about 4x more, after pipelining</div>
</div>
</div>

Pipelining changes the second bar, never the first. That difference is
this week's whole idea.

---

# What Keeps the Five Stages From Colliding

- Between each pair of stages sits a small holding spot, called a **pipeline register**
- Each pipeline register stores one instruction's partial result until the next tick
- Without it, a fast-moving instruction could overwrite a slower one's data by mistake

<div class="why">
Think of a tray at each station in a cafeteria line. It holds your food
until you are ready for the next station.
</div>

---

# At Any Tick, Five Instructions Could Be Mid-Flight

<div class="thread">Zoom into one single tick, once the pipeline is full.</div>

- One instruction is in Fetch, just entering the line
- Another is in Decode, reading its values
- Another is in Execute, doing its math
- Another is in Memory, if it needs a value
- Another is in Write Back, finishing up

<div class="why">
Five different instructions, five different stages, all busy on the
very same tick. This is exactly what Week 7's idle chip never achieved.
</div>

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week09/worksheet.html">Worksheet Part A</a></strong>. You will
count ticks for a small program, one instruction at a time versus
overlapped. About 15 minutes.
</div>

- Write down both tick counts and the difference between them
- It is OK to be unsure about the exact numbers — write your reasoning too
- We check your answer against the worked example next

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work. Do not confirm any answers yet, the real discussion happens next
session.
-->

---

<!-- SLOT N-2: Worked example -->

# Case Study: Timing the Studio Chip's Pipeline

<div class="thread">Same test program as Week 7, now overlapped instead of one at a time.</div>

Studio's chip now uses a five-stage pipeline. Assume every stage still
takes 100 ns, same as last week's steps.

| | One at a time (Week 7) | Pipelined (this week) |
|---|---|---|
| Test program | 1,000 `add` + 100 `lw` | same 1,100 instructions |
| Total ticks | varies per instruction type | 5 + 1,099 = 1,104 |
| Total time | 450,000 ns | 110,400 ns |

About **4x faster**, on the exact same program. After the first five
ticks fill the line, a new instruction starts almost every single tick.

<!-- notes: numbers are illustrative for this course, not exact textbook picosecond values; the pattern (fill once, then one instruction per tick) is the real teaching point. -->

---

# Pipeline Depth: Not Just Five Stages

<div class="thread">Five stages is the classic teaching design. Real chips often go further.</div>

- Some real processors split work into ten, fifteen, or even twenty pipeline stages
- More stages means even more instructions can overlap at once, raising throughput further
- But more stages also means more pipeline registers, more control logic, and more chances for a hazard

<div class="why">
This is why "just add more stages" is not automatically the best
design. Depth has real costs too.
</div>

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: what could still go wrong?</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **Hazard:** a situation where overlapping instructions could produce a wrong answer
- **Speedup:** how many times faster a pipelined program finishes, compared to one instruction at a time
- **Drain time:** the last few ticks, while the pipeline empties out
- **Stall:** pausing a stage for one or more ticks to avoid a wrong answer

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week09/worksheet.html">Worksheet Part B</a></strong>. Check
your Part A prediction, then compute a bigger example's speedup. About
15 minutes.
</div>

- The answer key explains why a "perfect" 5x speedup rarely happens exactly
- That small gap is a preview of a bigger problem we open next week

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). After about 15 minutes, cold-call 2-3 pairs to share their
reasoning out loud before moving on.
-->

---

# Putting the Five Stages Back Together

<div class="thread">Before closing, connect the whole pipeline back to today's opening story.</div>

<div class="pipeline">
<div class="stage"><div class="h">Fetch</div><div class="s">get it</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Decode</div><div class="s">read it</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Execute</div><div class="s">compute it</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Memory</div><div class="s">store or load it</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Write Back</div><div class="s">save it</div></div>
</div>

Five stages, five instructions in flight at once, a new one starting
almost every tick.

---

# Three Designs, Side by Side

<div class="thread">Three weeks, three designs, on the exact same test program.</div>

<div class="groupviz">
<div class="bucket"><div class="label">Single-Cycle (Week 6)</div><div class="rows">One long, fixed tick<br>Every instruction waits the same time</div><div class="agg">Slow on every instruction</div></div>
<div class="bucket"><div class="label">Multi-Cycle (Week 7)</div><div class="rows">Several short ticks<br>Each instruction uses only its own steps</div><div class="agg">Faster, still one at a time</div></div>
<div class="bucket"><div class="label">Pipelined (Week 9)</div><div class="rows">Same five short ticks<br>Several instructions overlap at once</div><div class="agg">A new instruction starts almost every tick</div></div>
</div>

Same chip family, three designs, each one removing the previous week's
limit.

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"Pipelining makes one instruction faster":** it does not. One instruction still takes the same five ticks, start to finish
- **"Five stages always means 5x speedup":** fill time, drain time, and real-world stalls always eat into that ideal number
- **"More stages is always better":** deeper pipelines add overhead and make the control logic harder to build correctly

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. A pipelined program finishes an instruction almost every tick, but each instruction still takes 5 ticks alone. Explain why both are true
2. A program has 50 instructions on a five-stage pipeline. Estimate the total ticks, assuming nothing stalls
3. Name one reason overlapping instructions can produce a wrong answer, even though each stage works correctly alone

<div class="why">
After this, take the short <a href="materials/week09/quiz.html">self-check quiz</a> for more
practice. It is ungraded.
</div>

---

# Answers

1. **Throughput** (instructions finishing per tick) and **latency** (one instruction's own time) measure different things — overlap improves the first, not the second
2. 5 + (50 − 1) = 54 ticks, assuming every stage takes one tick and nothing stalls
3. A later instruction can need a value an earlier instruction has not produced yet, since they now overlap in time

---

<!-- SLOT 14: Limits (Act 4 / CLOSE), becomes Week 10 slot 4 -->

# What Pipelining Cannot Do Yet

<div class="limits">
Pipelining overlaps instructions for speed, but overlapping them can
produce wrong answers. Two overlapped instructions can now interfere
with each other in ways a one-at-a-time chip never allowed.
</div>

---

<!-- SLOT 15: Bridge -->

# Next Week

Week 9 leaves **overlapping instructions safely, without wrong
answers**, unsolved. **Week 10, Pipelining II**, solves it: the hazards,
forwarding, and stalls that keep every answer correct.

---

<!-- SLOT 16: Summary -->

# Summary

- Pipelining splits instruction work into stages, so several instructions overlap and throughput rises
- One instruction's own time (latency) does not shrink — only how many finish per second (throughput) does
- A five-stage pipeline needs fill and drain ticks, so real speedup is always a bit less than the stage count
- **You did today:** key-word reviews, Worksheet Parts A and B, self-check quiz
- **Reading:** Hennessy & Patterson, 6th ed., Chapter 4 (pipelining introduction)
- **Handout:** [materials/week09/handout.md](materials/week09/handout.html), glossary and the full Studio-pipeline walkthrough
- **Prepare:** think of one everyday line you wait in. Bring one guess about what could go wrong if it overlapped customers

---

<!-- SLOT 17: Thank You -->
<!-- _class: end -->

# Thank You
