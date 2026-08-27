---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 10: Pipelining II

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Welcome the class back from last week. Ask: "Who remembers the two
laptop bugs we ended on?" Let a student describe one in their own words.
Today we fix both bugs, for good.
-->

---

<!-- SLOT 2: Where we are (Act 0 / LOCATE) -->

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
<div class="wk now"><div class="n">Wk 10</div><div class="t">Pipelining II</div></div>
<div class="wk"><div class="n">Wk 11</div><div class="t">Memory Hierarchy I</div></div>
<div class="wk"><div class="n">Wk 12</div><div class="t">Memory Hierarchy II</div></div>
<div class="wk"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

<!--
notes: Point at Week 9 and Week 10. Say: last week we built the overlap.
This week we make the overlap trustworthy.
-->

---

<!-- SLOT 3: Recap + open wound (Act 0 / LOCATE) -->

# Last Week, This Week

- **Last week delivered:** pipelining overlaps five instruction stages, so a new instruction starts almost every clock cycle
- **Last week left broken:** pipelining overlaps instructions for speed, but overlapping them can produce wrong answers

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), ZERO jargon -->

# When Faster Also Means Wrong

<div class="pain">

SmartPick's technician is testing the new Studio laptop. Its chip starts
a new instruction almost every tick, like workers on a fast assembly
line. One program line multiplies two numbers, and the next line uses
that answer right away. Most runs give the correct total, but sometimes
Studio gives an old, wrong number instead.

A second bug shows up in a different program. One line checks "is this
item in stock?" and then picks one of two next steps. Once in a while,
the assembly line takes the wrong step, and the final answer changes.

The engineers know why overlap makes things faster. Now they need to
know why it sometimes breaks the answer.

</div>

<!--
notes: Do not say "hazard," "forward," "stall," or "branch prediction"
yet. Ask: "Any guesses why the answer changes sometimes?" Take a few
guesses, then move on without confirming or denying any of them.
-->

---

<!-- SLOT 5: Cost of not knowing (Act 1 / MOTIVATE) -->

# What This Actually Costs

- A silently wrong total is worse than a slow but correct one, because users trust the number
- A chip shipped with this bug can need an expensive recall or a firmware fix later

<div class="why">
<strong>In industry:</strong> hazard-handling questions are common in
CPU-design interviews. Early pipelined processors taught the whole
industry that overlap must be checked carefully, not just built fast.
</div>

---

# The Deeper the Pipeline, the Higher the Stakes

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">Shallow pipeline, a hazard slips through</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 30%"></div></div>
  <div class="bar-value">a few wrong answers, easy to spot</div>
</div>
<div class="bar-row">
  <div class="bar-label">Deep pipeline, a hazard slips through</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 90%"></div></div>
  <div class="bar-value">wrong answers hidden inside heavy overlap</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

Modern chips overlap many more instructions than our five-stage example.
More overlap means more chances for a hazard to hide, if it is not
handled by design.

---

<!-- SLOT 6: Driving question (Act 1 / MOTIVATE) -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"How can a pipeline stay fast without ever computing a wrong answer?"</div>

---

<!-- SLOT 7: Learning outcomes (Act 1 / MOTIVATE) -->

# By the End of This Week, You Can

These four skills turn last week's broken pipeline into a trustworthy one.

<div class="cardlist">
<div class="card"><div class="h">Data & Control Hazards</div><div class="d">Identify data hazards and control hazards in a running program</div></div>
<div class="card"><div class="h">Forwarding</div><div class="d">Explain how forwarding fixes most data hazards without losing speed</div></div>
<div class="card"><div class="h">Stalls</div><div class="d">Explain why one specific case still needs a stall, even with forwarding</div></div>
<div class="card"><div class="h">Branch Prediction</div><div class="d">Explain how branch prediction and flushing handle control hazards</div></div>
</div>

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **Hazard:** a situation where overlapping instructions could compute a wrong answer
- **Data hazard:** one instruction needs a value a previous instruction has not produced yet
- **Control hazard:** the pipeline fetches instructions before it knows which way a branch goes
- **Stall (bubble):** a pause, one or more clock cycles, that fixes a hazard by waiting

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: who first solved this problem, and how?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **Forwarding (bypassing):** sending a computed result straight to the instruction that needs it, early
- **Register file:** the small, fast storage inside the chip that holds a program's working values
- **Hazard detection unit:** a circuit that watches for hazards and pauses the pipeline when needed

---

<!-- SLOT 8: Origin (Act 2 / GROUND) -->

# Where This Fix Came From

<div class="thread">Last week's break, restated. Now: who noticed it first, and what did they build?</div>

- **1967:** Robert Tomasulo, at IBM, invents forwarding: sending a fresh result straight to the instruction that needs it
- **1980s:** John Hennessy at Stanford and David Patterson at Berkeley make hazard detection standard, built-in hardware, not a rare add-on

<div class="why">
Your textbook authors, Hennessy and Patterson, are the same researchers
who helped make this fix standard. What you learn today is the model
every modern chip still uses.
</div>

---

# Why This Still Takes Careful Engineering

<div class="thread">Solved in the 1980s does not mean easy today.</div>

- Every new chip design must prove its hazard logic never lets a wrong answer through
- **Verification engineers** spend months testing exactly this: forwarding paths, stall logic, and branch flushes
- A hazard bug that slips past testing can still reach real, shipped hardware

This is not only a history lesson. It is a real, ongoing engineering job.

---

<!-- SLOT 9: Core concept (Act 2 / GROUND) -->

# Hazard: Definition

<div class="thread">One clean definition covers both bugs from this week's opening story.</div>

> A **hazard** is a situation where overlapping pipeline instructions
> could compute a wrong answer, unless something is done about it.

- **Data hazard:** an instruction needs a value a previous instruction has not produced yet
- **Control hazard:** the pipeline fetches instructions before it knows which way a branch goes

Both bugs from the pain story are hazards. Both have a known, standard fix.

---

# Also Worth Knowing: Structural Hazards

<div class="thread">Data and control hazards are today's focus. A third type exists too.</div>

- A **structural hazard** happens when two instructions need the exact same piece of hardware in the same cycle
- Modern chips avoid most structural hazards by building extra hardware copies, so they show up far less often
- This week's fixes, and this week's worksheet, focus on data and control hazards, the two you will trace by hand

---

<!-- Act 3 / BUILD: expand freely from here. -->

<!-- SLOT 10: Mechanics -->

# Data Hazards: Why Timing Breaks the Answer

<div class="thread">First, see exactly where the timing goes wrong.</div>

| Cycle | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Instr 1: multiply | IF | ID | EX (computes result) | MEM | WB (writes result) |
| Instr 2: use result | | IF | ID | EX (needs result now) | MEM |

Instruction 2 reaches EX in cycle 4. Instruction 1 does not write its
result until cycle 5. Without help, instruction 2 reads an old, wrong
value.

---

<!-- SLOT 11: Mechanics -->

# Fix 1: Forwarding (Bypassing)

<div class="thread">The value already exists after EX. The pipeline was just not using it yet.</div>

- The chip adds a direct wire from instruction 1's EX output to instruction 2's EX input
- Instruction 2 grabs the fresh value the moment it is computed, skipping the slow trip through storage
- No pause is needed. Both instructions keep moving, one cycle apart, at full speed

| Cycle | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Instr 1: multiply | IF | ID | EX (forwards result) | MEM | WB |
| Instr 2: use result | | IF | ID | EX (uses forwarded value) | MEM |

Forwarding fixes this exact case completely. No cycle is wasted.

---

# A Chain of Three: Forwarding More Than Once

<div class="thread">Real programs often chain several dependent instructions in a row.</div>

| Cycle | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| I1: `add` | IF | ID | EX | MEM | WB | |
| I2: uses I1, computes | | IF | ID | EX | MEM | WB |
| I3: uses I2's result | | | IF | ID | EX | MEM |

- I1 forwards its result to I2's EX stage, one cycle later
- I2 forwards its own new result to I3's EX stage, one cycle after that
- The hazard detection unit checks every pair, not just neighbors, every single cycle

Each link in the chain gets its own forwarding wire, at the moment it is needed.

---

# Forwarding Has More Than One Source

<div class="thread">EX is not the only stage that can hand off a value early.</div>

- A result can also be forwarded from the **MEM** stage, one cycle later than from EX
- The hazard detection unit checks both distances and always picks the freshest value available
- This is why real chips need several forwarding wires, not just one

<div class="why">
Rule of thumb: forward whenever a value is ready before it is needed.
Stall only when even the earliest forwarding path still arrives too
late.
</div>

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week10/worksheet.html">Worksheet Part A</a></strong>. You will
trace a small pipeline and find where forwarding is needed. About 15
minutes.
</div>

- Mark each cycle where an instruction needs a value that is not written back yet
- Draw the forwarding wire that fixes each case
- We check your answers together at the start of 차시 3

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work. Do not confirm any answers yet, the real discussion happens next
session.
-->

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: what if forwarding still is not fast enough?</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **Load-use hazard:** a data hazard forwarding alone cannot fully fix, because the value arrives one stage too late
- **Branch prediction:** a guess about which way a branch will go, made before the answer is known
- **Flush:** throwing away wrongly fetched instructions after a guessed branch turns out wrong
- **Misprediction penalty:** the cycles lost when a branch guess turns out wrong

---

<!-- SLOT 12: Mechanics -->

# When Forwarding Is Not Enough

<div class="thread">Forwarding solves the multiply example. One case still breaks it.</div>

A value loaded from memory is not ready until the MEM stage finishes,
one stage later than a normal computed result.

| Cycle | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Instr 1: load value | IF | ID | EX | MEM (value ready here) | WB |
| Instr 2: use value | | IF | ID | EX (needs it now) | MEM |

Instruction 2 needs the value one cycle before instruction 1 has it.
Forwarding cannot send a value that does not exist yet.

---

<!-- SLOT 13: Mechanics -->

# Fix 2: Stalling (Bubbles)

<div class="thread">When forwarding cannot reach back far enough, the pipeline must wait.</div>

- The **hazard detection unit** checks every instruction pair for exactly this pattern
- When it finds a load-use hazard, it freezes instruction 2 for one cycle, a "bubble"
- After the one-cycle pause, forwarding delivers the value normally, and both instructions continue

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">Stall on every data hazard</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">many cycles wasted</div>
</div>
<div class="bar-row">
  <div class="bar-label">Forward, stall only for load-use</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 20%"></div></div>
  <div class="bar-value">very few cycles wasted</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

---

<!-- SLOT 14: Mechanics -->

# Control Hazards: Guessing the Next Instruction

<div class="thread">Data hazards are handled. A branch causes a different kind of timing problem.</div>

- A branch instruction decides "go here" or "go there," but the answer is not known until a later stage
- The pipeline must fetch the next instruction immediately, before that answer is ready
- If it fetches from the wrong path, those instructions must never affect the final answer

---

<!-- SLOT 15: Mechanics -->

# Fix 3: Branch Prediction and Flushing

<div class="thread">Guessing beats waiting, as long as wrong guesses are caught and undone.</div>

- The chip predicts which way the branch will likely go, and keeps fetching down that path
- If the guess is correct, no time is lost at all
- If the guess is wrong, the chip flushes the wrong instructions before they finish, then restarts on the correct path

<div class="why">
Always stalling until every branch is known would waste a cycle on
almost every branch. Predicting is faster on average, even though some
guesses are wrong.
</div>

---

# How Good Is a Guess?

<div class="thread">Prediction only pays off if the guesses are usually right.</div>

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">Random 50/50 guess</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 50%"></div></div>
  <div class="bar-value">wrong about half the time</div>
</div>
<div class="bar-row">
  <div class="bar-label">Real branch predictor</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 92%"></div></div>
  <div class="bar-value">right most of the time</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

Real predictors remember how a branch behaved recently, so most guesses
are right. The rare wrong guess still costs a flush, but rare is the key
word.

---

# Where These Fixes Actually Run

<div class="thread">Forwarding, stalling, and prediction are not classroom-only ideas.</div>

<div class="appgrid">
<div class="app"><div class="name">Phone chips</div><div class="desc">forwarding and prediction, built into a battery-limited design</div></div>
<div class="app"><div class="name">Laptop CPUs</div><div class="desc">like Studio's chip, forwarding and prediction run on every instruction</div></div>
<div class="app"><div class="name">Cloud servers</div><div class="desc">millions of predictions per second, across many rented cores</div></div>
<div class="app"><div class="name">Game consoles</div><div class="desc">branch-heavy game logic depends heavily on accurate prediction</div></div>
</div>

Every chip you use today already runs the fixes from this week, on
every single instruction.

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week10/worksheet.html">Worksheet Part B</a></strong>. Check
your Part A answers, then trace a branch prediction and a flush. About
15 minutes.
</div>

- The answer key explains exactly which cycles are flushed when a guess is wrong
- Notice how few cycles are actually lost, even on a wrong guess

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). After about 15 minutes, cold-call 2-3 pairs to share their
reasoning out loud before moving on.
-->

---

<!-- SLOT N-2: Worked example -->

# Case Study: Studio's Pipeline, Fixed

<div class="thread">Back to the two bugs from this week's opening story.</div>

- **Multiply-then-use bug:** forwarding sends the multiply result straight into the next instruction's EX stage. Correct answer, every time, no pause
- **Stock-check branch bug:** the chip predicts a path, keeps running, and flushes if wrong. The wrong path never reaches WB, so it never changes a stored value

Studio's pipeline is now both fast and correct. That is the whole point
of this week.

---

# Three Fixes, One Pipeline

<div class="thread">Before the checklist, one clean picture of everything from this week.</div>

<div class="pipeline">
<div class="stage"><div class="h">Data hazard</div><div class="s">forward the result early</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Load-use hazard</div><div class="s">stall one cycle, then forward</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Control hazard</div><div class="s">predict, then flush if wrong</div></div>
</div>

Three different problems, three matched fixes. Every one keeps the
pipeline both fast and correct, most of the time at full speed.

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

<div class="cardlist">
<div class="card"><div class="h">"Just always stall to be safe"</div><div class="d">correct, but wastes speed on nearly every instruction. Defeats the reason pipelining exists</div></div>
<div class="card"><div class="h">"Forwarding fixes every data hazard"</div><div class="d">it does not. The load-use case still needs one stall cycle</div></div>
<div class="card"><div class="h">"A wrong branch guess is a bug"</div><div class="d">it is expected sometimes. Flushing is the planned fix, not an error</div></div>
<div class="card"><div class="h">"More pipeline stages are always better"</div><div class="d">deeper pipelines also pay a bigger penalty for every wrong guess</div></div>
</div>

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. An instruction needs a value from the instruction right before it. Which hazard is this, and what usually fixes it?
2. Why can forwarding alone not fix a load-use hazard?
3. A branch prediction turns out wrong. What must the pipeline do next?

<div class="why">
After this, take the short <a href="materials/week10/quiz.html">self-check quiz</a> for more
practice. It is ungraded.
</div>

---

# Answers

1. A **data hazard**. Forwarding usually fixes it, sending the result straight to the instruction that needs it
2. Because the loaded value is not ready until the MEM stage, one stage later than forwarding can reach
3. It must **flush** the wrongly fetched instructions and restart fetching on the correct path

---

<!-- SLOT N+1: Limits (Act 4 / CLOSE), becomes Week 11 slot 4 -->

# What Hazard Handling Cannot Do Yet

<div class="limits">
Hazards are handled: forwarding, stalling, and branch prediction keep
overlapping instructions correct. But every pipeline still waits on a
slow memory system. Every load, store, and instruction fetch has to
reach out to memory before it can finish. A fast, correct pipeline gains
nothing if every one of those trips stalls on memory.
</div>

---

<!-- SLOT N+2: Bridge -->

# Next Week

Week 10 leaves **a slow memory system** unsolved. **Week 11, Memory
Hierarchy I**, addresses it: caching, so most memory trips become fast.

---

<!-- SLOT N+3: Summary -->

# Summary

- A hazard is a situation where overlapping instructions could compute a wrong answer
- Forwarding fixes most data hazards without losing a single cycle
- The load-use hazard still needs one stall cycle, even with forwarding
- Branch prediction, with flushing on a wrong guess, handles control hazards
- **You did today:** Worksheet Parts A and B, self-check quiz
- **Reading:** Hennessy & Patterson, 6th ed., Appendix C, Pipelining
- **Handout:** [materials/week10/handout.md](materials/week10/handout.html), glossary and the full SmartPick pipeline walkthrough
- **Prepare:** think of one time a "guess now, fix if wrong" strategy worked in real life

---

<!-- SLOT N+4: Thank You -->
<!-- _class: end -->

# Thank You
