---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 15: Final Exam Review

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Short review week, no new content. Goal: rebuild the whole
semester's arc in students' heads, then drill the questions most likely
to appear on the cumulative final. Keep pace brisk on recap, slow down
on the check-yourself blocks.
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
<div class="wk"><div class="n">Wk 10</div><div class="t">Pipelining II</div></div>
<div class="wk"><div class="n">Wk 11</div><div class="t">Memory Hierarchy I</div></div>
<div class="wk"><div class="n">Wk 12</div><div class="t">Memory Hierarchy II</div></div>
<div class="wk"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk now review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

---

<!-- SLOT 3: Recap + open wound (Act 0 / LOCATE), adapted for review week -->

# Fourteen Weeks, One Machine

- **Fourteen weeks delivered:** a full picture of a machine, from layers to metrics to a fast, parallel datapath
- **What's still shaky:** turning that picture into fast, confident recall under exam conditions

Today we rebuild the arc, then drill the questions most likely to trip you up.

---

<!-- Course logistics appendix: final exam facts, outside the spine numbering, from Week 1's grading table -->

# The Final Exam, By the Numbers

<div class="thread">From Week 1's grading table, so you know exactly what is riding on today.</div>

| Item | Weight |
|---|---|
| Attendance | 10% |
| Midterm (Wk 1-7) | 30% |
| **Final (Wk 1-14, cumulative)** | **30%** |
| Assignments | 10% |
| Presentation | 10% |
| In-class items | 10% |

The final is worth as much as the midterm, and it covers **twice the material**.

---

<!-- Act 3 (Build), thematic recap: overview -->

# The Semester in Three Acts

<div class="thread">Fourteen weeks, three thematic groups. Same shape as the roadmap, seen from further back.</div>

<div class="groupviz">
<div class="bucket">
<div class="label">Weeks 1-5</div>
<div class="rows">Layers, then a way to<br>measure and describe<br>any machine</div>
<div class="agg">Measuring &amp; Describing</div>
</div>
<div class="bucket">
<div class="label">Weeks 6-10</div>
<div class="rows">Build a datapath, then<br>make it fast without<br>breaking correctness</div>
<div class="agg">Building &amp; Speeding Up</div>
</div>
<div class="bucket">
<div class="label">Weeks 11-14</div>
<div class="rows">Feed that datapath, then<br>scale it past one core</div>
<div class="agg">Memory &amp; Parallel Scale</div>
</div>
</div>

---

# Weeks 1-5: Measuring and Describing a Machine

<div class="cardlist">
<div class="card"><div class="h">Wk 1</div><div class="d">three layers — ISA, microarchitecture, hardware. Same ISA can hide very different speeds</div></div>
<div class="card"><div class="h">Wk 2</div><div class="d">CPU time, clock rate, CPI, and Amdahl's Law — the tools to put a number on "faster"</div></div>
<div class="card"><div class="h">Wk 3</div><div class="d">how numbers become bits — binary, two's complement, IEEE floating point</div></div>
<div class="card"><div class="h">Wk 4-5</div><div class="d">a complete ISA — R/I/J-type formats, branches and jumps, what "add" and "load" mean as bit patterns</div></div>
</div>

These five weeks gave us words and numbers for any machine, before opening the box.

---

# Weeks 6-10: Building and Speeding Up a Datapath

<div class="cardlist">
<div class="card"><div class="h">Wk 6</div><div class="d">single-cycle datapath — every instruction takes exactly one clock cycle</div></div>
<div class="card"><div class="h">Wk 7</div><div class="d">multi-cycle — shorter cycles, but more control states to track</div></div>
<div class="card"><div class="h">Wk 9</div><div class="d">pipelining — overlap instructions for speed, but hazards can break correctness</div></div>
<div class="card"><div class="h">Wk 10</div><div class="d">hazard fixes — forwarding, stalling, and branch prediction</div></div>
</div>

Same instruction set, three different builds, each one faster and more fragile than the last.

---

# Weeks 11-14: Memory, Parallel Scale, and Real Designs

<div class="cardlist">
<div class="card"><div class="h">Wk 11</div><div class="d">cache — hit, miss, and Average Memory Access Time (AMAT)</div></div>
<div class="card"><div class="h">Wk 12</div><div class="d">virtual memory — paging, the TLB, and what a page fault does</div></div>
<div class="card"><div class="h">Wk 13</div><div class="d">parallelism — multicore, SIMD, Amdahl's Law again, and cache coherence</div></div>
<div class="card"><div class="h">Wk 14</div><div class="d">a real processor design, seen through every layer above</div></div>
</div>

A fast pipeline is wasted if memory can't feed it or if only one core does the work.

---

# One Machine, Every Layer at Once

<div class="thread">Back to Week 1's picture, now with everything we added since.</div>

<div class="pipeline">
<div class="stage"><div class="h">ISA</div><div class="s">Wks 1, 4-5</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Pipelined Datapath</div><div class="s">Wks 6-10</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Cache + Virtual Memory</div><div class="s">Wks 11-12</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Multicore</div><div class="s">Wk 13</div></div>
</div>

SmartPick's Studio laptop wins on all four stages, not just clock speed. That is the whole course, in one row.

---

<!-- Act 3 / Check Yourself divider -->

<!-- _class: section -->

# Check Yourself: The Full Semester

<div class="driving-q">15 questions, weighted toward Weeks 9-14. Answers follow each block.</div>

<!--
notes: Week 8's midterm review already drilled Weeks 1-7 in depth, so
spend less time there. Slow down on pipelining, memory, and parallelism
questions — that is where the final leans hardest.
-->

---

# Questions 1-3: Weeks 1-5

1. Value's video export runs 2 billion instructions at CPI 3, at 3.0 GHz. Find the CPU time
2. Write **-9** as an 8-bit two's complement binary number
3. Which instruction format computes using only registers, and which one adds an offset to reach memory?

---

# Answers 1-3

1. CPU time = (instructions x CPI) / clock rate = (2G x 3) / 3.0G = **2.0 s**
2. `00001001` -> invert bits -> `11110110` -> add 1 -> **`11110111`**
3. **R-type** computes using only registers (e.g. `add`). **I-type** adds a register plus a small offset, used by `lw`/`sw`

---

# Questions 4-5: Weeks 6-7

4. A single-cycle CPU gives every instruction one full clock cycle. What's the main downside of fixing the cycle length this way?
5. Give one reason a multi-cycle `beq` finishes in fewer cycles than a multi-cycle `lw`

---

# Answers 4-5

4. The cycle must be long enough for the **slowest** instruction (`lw`). Fast instructions like `add` still waste time waiting out the rest
5. `beq` skips steps it does not need, like the memory-access cycle. `lw` needs every step: fetch, register read, address compute, memory access, write-back

---

# Questions 6-8: Weeks 9-10

6. Name the three types of pipeline hazards, one line each
7. Forwarding fixes most data hazards right away. Why can't it fully fix a **load-use** hazard?
8. A branch is mispredicted 20% of the time, with a 4-cycle penalty. What is the expected extra cycles per branch?

---

# Answers 6-8

6. **Structural:** two instructions need the same hardware at once. **Data:** an instruction needs a value that isn't ready yet. **Control:** a branch outcome isn't known yet
7. The loaded value is only ready after the memory stage, one stage later than an ALU result. At least one stall cycle is still needed
8. 0.20 x 4 = **0.8 extra cycles per branch**, on average

---

# Questions 9-10: Week 11 (Cache)

9. A program touches a new array for the very first time, and it isn't in the cache yet. Which type of miss is this?
10. Hit time is 1 ns, miss rate is 8%, miss penalty is 90 ns. Compute AMAT

---

# Answers 9-10

9. A **compulsory miss** — the data was never in the cache before, no matter how big the cache is
10. AMAT = hit time + (miss rate x miss penalty) = 1 + (0.08 x 90) = **8.2 ns**

---

# Questions 11-12: Week 12 (Virtual Memory)

11. What does a TLB store, and why does that make address translation fast?
12. What happens, step by step, on a page fault?

---

# Answers 11-12

11. A TLB stores recently used virtual-to-physical page translations, so most lookups skip the slower full page-table walk
12. The OS finds the missing page on disk and loads it into a free physical frame. It updates the page table, then re-runs the instruction

---

# Questions 13-15: Weeks 13-14

13. A program is 80% parallelizable. What is the max speedup on 4 cores, by Amdahl's Law?
14. Two cores each cache the same address, and one writes to it. What problem can occur, and what prevents it?
15. A laptop chip and a phone chip can share the same ARM ISA. Name two microarchitecture differences that could still make one faster

---

# Answers 13-15

13. Speedup = 1 / (0.2 + 0.8/4) = 1 / 0.4 = **2.5x** (same formula as Week 2, now applied to cores)
14. Stale data across caches; a **coherence protocol** invalidates or updates the other copies so both see the new value
15. Any two: pipeline depth, cache size, core count, in-order vs. out-of-order execution, clock speed vs. power budget

---

<!-- SLOT N+1: "Limits" replaced by "What to focus on next" -->

# What to Focus On Next

<div class="limits">
Weeks 1-7 were already reviewed in depth at the midterm — spend less time
there. Put your remaining study time on <strong>pipelining hazards</strong>
(Wks 9-10), <strong>memory hierarchy</strong> (Wks 11-12), and
<strong>parallelism</strong> (Wk 13). Those weeks carry the most weight on
this review, and the most calculation-style questions on the final.
</div>

---

<!-- SLOT N+2: Bridge, adapted — no next week, so it bridges to the exam itself -->

# From Review to Exam

This review leaves one thing unsolved: doing it **without notes, under
time pressure**. The final exam is where you prove you can.

---

<!-- SLOT N+3: Summary -->

# Summary

- Fifteen weeks, one machine: layers, then metrics, then data, then a datapath, then pipelining, then memory, then parallel scale
- The final is cumulative (Weeks 1-14) and worth 30% of your grade, same weight as the midterm
- Heaviest review load: pipelining hazards, cache/AMAT, virtual memory, and Amdahl's Law with multiple cores
- **Reading:** re-skim your Week 9-13 handouts and worksheets tonight
- **Prepare:** bring your ID, arrive early, and rework today's 15 questions from memory once before the exam

---

<!-- SLOT N+4: Thank You -->
<!-- _class: end -->

# Thank You
