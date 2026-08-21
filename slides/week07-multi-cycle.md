---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 7: Multi-Cycle

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Welcome back. Ask: "Last week we built a working chip. Did anyone
notice a problem with it?" Let a few guesses land, then say: today we fix
exactly that problem, without throwing away the chip.
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
<div class="wk now"><div class="n">Wk 7</div><div class="t">Multi-Cycle</div></div>
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
notes: Point at Week 6 and Week 7. Say: last week we built the chip.
This week we make it waste less time. Week 8 is the midterm, covering
everything from Week 1 through today.
-->

---

<!-- SLOT 3: Recap + open wound -->

# Last Week, This Week

- **Last week delivered:** a working chip (a single-cycle datapath) that correctly runs every instruction in exactly one clock cycle
- **Last week left broken:** it wastes a full clock cycle on every instruction, even fast ones

<div class="why">
That second line is today's whole problem. We are not throwing away
last week's chip. We are fixing exactly this one weakness.
</div>

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **Multi-cycle design:** a chip design that gives each instruction only as many clock ticks as it actually needs
- **Step:** one small piece of work a chip does while running an instruction, such as "read a register"
- **Reuse:** using the same piece of hardware more than once, for different jobs, instead of building it twice
- **Cycle count:** how many clock ticks one instruction actually takes to finish

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE) -->

# The Chip That Never Hurries Up

<div class="pain">

An engineer tests last week's chip on a real program: 1,000 simple "add"
instructions and 100 slow "fetch from memory" instructions.

She expects the adds to finish quickly, since they do less work. They do
not. Every single instruction, fast or slow, waits out the exact same
long tick. The chip was built to always wait for the slowest case, even
when the actual work is almost done.

1,000 quick jobs, each one forced to wait as long as the slowest job.
That time is gone, and it never comes back.

</div>

<!--
notes: Let this sit for a second. Ask: "Why would a chip make a fast
instruction wait for no reason?" Take 2-3 guesses without confirming
any yet. This mirrors last week's Limit slide almost word for word —
say that out loud if it helps students connect the two weeks.
-->

---

# One Slow Tick, Repeated a Thousand Times

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">"add" actual work needed</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 50%"></div></div>
  <div class="bar-value">short</div>
</div>
<div class="bar-row">
  <div class="bar-label">"add" time it is forced to wait</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">full slow tick, every time</div>
</div>
</div>
<div class="bar-note">example pattern, not measured data — the gap is the point</div>

"add" only needs part of one tick. It still pays for the whole tick,
1,000 times over, because the chip cannot tell the two apart.

---

<!-- SLOT 5: Cost of not knowing -->

# What This Actually Costs

- A laptop with this chip burns extra time, and extra battery, on ordinary tasks like typing or scrolling
- A phone chip built this way runs hotter than it needs to, for no real benefit
- A company shipping a product on this design loses a real, measurable speed advantage to competitors
- A cloud provider running slower chips than rivals loses customers to faster, cheaper alternatives

<div class="why">
<strong>In industry:</strong> "how would you speed up this datapath
without a full redesign" is a real interview question for chip design
roles. Real processors from the 1980s onward used exactly this
multi-cycle fix before moving to today's even faster designs.
</div>

---

# The Same Waste, at a Bigger Scale

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One phone, one day of use</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 22%"></div></div>
  <div class="bar-value">a little extra battery drain</div>
</div>
<div class="bar-row">
  <div class="bar-label">One laptop model, one product line</div>
  <div class="bar-track"><div class="bar-fill risk-med" style="width: 58%"></div></div>
  <div class="bar-value">a real, felt speed disadvantage</div>
</div>
<div class="bar-row">
  <div class="bar-label">One datacenter, millions of chips</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 95%"></div></div>
  <div class="bar-value">huge wasted power and money</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

The same wasted tick, multiplied by every chip a company ships.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"How can a chip give each instruction only the time it actually needs, without slowing the whole thing down?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

1. Explain why last week's chip forces every instruction to wait for the slowest one
2. Describe how a multi-cycle chip splits one instruction into several short steps
3. Explain how a control unit decides which step runs next, for each instruction type
4. Compare single-cycle and multi-cycle total run time for a small program

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Coming Up Next: Worksheet Part A

Next session, you will work in pairs on
**[Worksheet Part A](materials/week07/worksheet.html)**.

- You will see the steps a chip needs for "add" and for "load from memory"
- Your pair predicts how many steps each instruction needs, and why
- Then we check your prediction against the real answer together

<div class="why">
Bring your notebook. No calculator needed, just the step list we hand
out.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: who first thought of building a chip this way?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **Control unit:** the part of a chip that decides what happens on each clock tick
- **Finite state machine:** a small circuit that moves through a fixed set of steps, one tick at a time
- **Microprogramming:** storing a list of control steps, instead of wiring one giant fixed circuit
- **Register (temporary):** a small storage spot that holds one value between ticks, so it is not lost

---

<!-- SLOT 8: Origin -->

# This Problem Is Not New Either

<div class="thread">You just felt the pain again. Now: who solved it, and how?</div>

- **1951:** Maurice Wilkes, at Cambridge, builds a computer (EDSAC) whose control logic is hard to fix once wired. Rewiring circuits by hand, for every small change, is slow and error-prone
- **His idea:** store the control steps as data in a small memory. Read one step per tick, like a recipe list. He calls this **microprogramming**

<div class="why">
This is the ancestor of today's idea: split one instruction into steps,
and let a small controller walk through them, one tick at a time.
</div>

---

# From Rewiring to Reading a Recipe

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1949</div><div class="d">EDSAC runs<br>hardwired control</div></div>
<div class="pt"><div class="dot"></div><div class="y">1951</div><div class="d">Wilkes proposes<br>microprogramming</div></div>
<div class="pt"><div class="dot"></div><div class="y">1960s-80s</div><div class="d">Most real chips<br>use step-by-step control</div></div>
<div class="pt"><div class="dot"></div><div class="y">Today</div><div class="d">Still used for complex<br>instructions in modern chips</div></div>
</div>

Wilkes solved a wiring problem. We reuse his idea to solve a speed
problem: let each instruction take only the steps it needs.

---

# Real Chips That Used This Idea

<div class="thread">Not just history class. This idea shipped in real, working machines.</div>

- **IBM System/360 (1964):** one of the first widely used commercial computers to run on microprogrammed, step-by-step control
- **DEC PDP-11 and VAX:** popular 1970s-80s computers, built with multi-cycle, microprogrammed designs
- **Early Intel x86 chips:** used multi-cycle control well into the 1980s, before faster designs took over

<div class="why">
These were not toy examples. Multi-cycle, step-by-step control ran real
software, for real companies, for decades.
</div>

---

<!-- SLOT 9: Core concept -->

# Multi-Cycle Datapath: Definition

<div class="thread">One historical idea, one formal definition. Here it is.</div>

> A **multi-cycle datapath** splits each instruction into several short
> steps, run one per clock tick. The clock tick is only as long as the
> single slowest step, not the slowest whole instruction.

- **Shared hardware:** one ALU, one memory, reused for several steps of the same instruction
- **Temporary registers:** small storage that holds a value from one tick until a later step needs it
- **Control unit:** decides which step runs next, and which wires turn on, each tick

---

<!-- Act 3 / BUILD -->

# Why One Clock Length Never Fit All

<div class="thread">Back to last week's chip, with real numbers this time.</div>

Last week, every instruction shared one fixed, long clock tick, sized
for the slowest instruction, "load from memory":

- Fetch the instruction, read registers, compute, access memory, save the result. All five, back to back, in one tick
- A simple "add" only needs three of those five actions, but still waits for the same full tick

That fixed tick is the exact thing multi-cycle removes.

---

# Breaking One Instruction Into Steps

<div class="thread">Instead of one long tick, give each action its own short tick.</div>

<div class="pipeline">
<div class="stage"><div class="h">Fetch</div><div class="s">get the instruction from memory</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Decode</div><div class="s">figure out what it means, read registers</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Execute</div><div class="s">do the math, or compute an address</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Memory</div><div class="s">read or write data, if needed</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Write Back</div><div class="s">save the result to a register, if needed</div></div>
</div>

Each step is short. One tick now equals one step, not five.

---

# Different Instructions, Different Step Counts

<div class="thread">The whole point: not every instruction visits every step.</div>

| Instruction | Steps it uses | Steps it skips | Total ticks |
|---|---|---|---|
| `add` (R-type) | Fetch, Decode, Execute, Write Back | Memory | 4 |
| `lw` (load word) | Fetch, Decode, Execute, Memory, Write Back | none | 5 |
| `sw` (store word) | Fetch, Decode, Execute, Memory | Write Back | 4 |
| `beq` (branch) | Fetch, Decode, Execute | Memory, Write Back | 3 |

`beq` finishes in 3 short ticks now, instead of waiting through one long
tick built for `lw`.

---

# Reusing Hardware, Remembering Between Steps

<div class="thread">Splitting into steps creates a new problem: how does the chip remember?</div>

- One ALU now does several jobs per instruction: computing an address, then later comparing two values
- The chip needs small "notepads": temporary registers that hold one value from one tick until a later step needs it
- Example: the fetched instruction itself must be remembered across every one of its own steps

<div class="why">
Last week's chip never needed this, because every instruction finished
inside one single tick. Now, work is spread across several ticks.
</div>

---

# Who Decides the Next Step? The Control Unit

<div class="thread">Wilkes's idea, applied directly: a small circuit that reads out steps.</div>

- The **control unit** tracks which step of which instruction is happening right now
- Each tick, it turns on the right wires for that one step, and picks the next step
- Different instruction types take different paths: `add` skips the memory step, `beq` skips both memory and write-back

This "which step next" logic can be built as a **finite state machine**,
or stored step by step as **microcode** — Wilkes's original idea, still
in use.

---

# Counting Total Ticks for a Whole Program

<div class="thread">One more link back to Week 2's CPU-time idea.</div>

- Multiply each instruction type's own step count by how many times that type appears in the program
- Add up every instruction type's total, to get the whole program's total ticks
- Multiply total ticks by the length of one short tick, to get the real total time

This is the same CPU-time idea from Week 2, now computed one
instruction type at a time, instead of one single average number.

---

<!-- SLOT N-2: Worked example -->

# Case Study: Timing the Fix

<div class="thread">Back to the engineer's test: 1,000 adds, 100 loads. Real numbers now.</div>

Say the old single-cycle tick is 500 ns. Say each new short step takes
100 ns:

| Design | Time for 1,000 `add` | Time for 100 `lw` | Total |
|---|---|---|---|
| Single-cycle | 1,000 × 500 ns | 100 × 500 ns | 550,000 ns |
| Multi-cycle | 1,000 × 400 ns (4 steps) | 100 × 500 ns (5 steps) | 450,000 ns |

Same program, same instructions, about **18% less total time** — just
by not forcing `add` to wait for `lw`'s full tick.

<!-- notes: numbers are illustrative for this course, not exact textbook picosecond values; the pattern (fewer steps, shorter tick) is the real teaching point. -->

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week07/worksheet.html">Worksheet Part A</a></strong>. You will trace
the steps `add`, `lw`, `sw`, and `beq` each need, and predict their
total ticks. About 15 minutes.
</div>

- Use the step table from a few slides ago if you need it
- It is OK to be unsure — write down what you do not know too
- We compare answers together at the start of 차시 3

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work. Do not confirm any answers yet, the real discussion happens next
session.
-->

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: what does multi-cycle still not fix?</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **Instruction register (IR):** a temporary spot that holds the current instruction while it runs
- **Memory data register (MDR):** a temporary spot that holds a value just read from memory
- **Idle:** doing no useful work while waiting
- **Overlap:** starting a new piece of work before the current one is fully finished

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week07/worksheet.html">Worksheet Part B</a></strong>. Check your Part
A predictions against the real step counts, then answer two new
questions. About 15 minutes.
</div>

- The answer key explains **why fewer total steps still means real, measurable time saved**
- It also asks what part of the problem multi-cycle still leaves open

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). Let pairs self-check. After ~15 minutes, cold-call 2-3 pairs
to share their reasoning before moving on.
-->

---

# Single-Cycle and Multi-Cycle, Side by Side

<div class="thread">Before closing, put both weeks' chips next to each other.</div>

<div class="groupviz">
<div class="bucket"><div class="label">Single-Cycle (Week 6)</div><div class="rows">One fixed, long tick<br>Every instruction waits the same time<br>Simple control logic</div><div class="agg">Slow on every instruction</div></div>
<div class="bucket"><div class="label">Multi-Cycle (Week 7)</div><div class="rows">Several short ticks<br>Each instruction uses only its own steps<br>Needs a control unit and temp registers</div><div class="agg">Faster overall, still one instruction at a time</div></div>
</div>

Real time drops. But notice: still just **one** instruction running at a
time, on both designs.

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"More cycles per instruction always means slower":** wrong — each cycle is much shorter, so total real time usually drops
- **"Every instruction now takes the same number of steps":** wrong — that was last week's problem. The whole point is that they differ
- **"The control unit is just a fixed table":** it is more like a small program. Its next step depends on the instruction type and the step before it
- **"Multi-cycle already overlaps instructions":** wrong — it still finishes one instruction fully, step by step, before the next one starts

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. Why does `add` need fewer steps than `lw` in a multi-cycle chip?
2. If one short step takes 100 ns, how long does a 4-step `sw` take? Faster or slower than a 500 ns single-cycle tick?
3. Name one new piece of hardware multi-cycle needs that single-cycle did not

<div class="why">
After this, take the short <a href="materials/week07/quiz.html">self-check quiz</a> for more
practice. It is ungraded.
</div>

---

# Answers

1. `add` skips the memory-access step, since it never reads or writes memory — only `lw` and `sw` need that step
2. 4 × 100 ns = 400 ns, faster than the old 500 ns single tick
3. A temporary register, such as the instruction register or a memory data register. Or the control unit itself

---

<!-- SLOT 14: Limits (Act 4 / CLOSE), becomes Week 9 slot 4 -->

# What Multi-Cycle Still Cannot Do

<div class="limits">
Multi-cycle now gives every instruction only the steps it actually
needs, saving real time. But the chip still finishes one instruction
completely before starting the next one. While step 1 of the next
instruction waits, the rest of the chip sits idle, doing nothing.
</div>

---

<!-- SLOT 15: Bridge -->

# Next Week

Week 7 leaves **one instruction running at a time, with the rest of the
chip idle** unsolved. Week 8 is the midterm review, covering Weeks 1-7.
**Week 9, Pipelining**, then solves this directly: overlapping several
instructions so no part of the chip sits idle.

---

<!-- SLOT 16: Summary -->

# Summary

- Multi-cycle splits each instruction into short steps, so simple instructions no longer wait for the slowest step of every instruction
- Different instructions now take different numbers of ticks, and the tick itself is much shorter than last week's fixed tick
- The chip still runs only one instruction at a time — that gap is next week's story, after the midterm
- **You did today:** Worksheet Parts A and B, self-check quiz
- **Reading:** Stallings, *Computer Organization and Architecture*, chapters on Control Unit Operation and Microprogrammed Control
- **Handout:** [materials/week07/handout.md](materials/week07/handout.html), glossary and the full step-timing walkthrough
- **Midterm next week:** Week 8 covers Weeks 1-7. Review this week's step table and the CPU-time idea from Week 2
- **Prepare:** look back at your Week 2 notes on CPU time and CPI before the midterm review

---

<!-- SLOT 17: Thank You -->
<!-- _class: end -->

# Thank You
