---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 8: Midterm Review

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Short review week, no new material. Tell students up front: today
we walk back through Weeks 1-7, then the midterm exam happens inside
this same class block. Keep the pace brisk and confident.
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
<div class="wk now review"><div class="n">Wk 8</div><div class="t">Midterm Exam</div></div>
<div class="wk"><div class="n">Wk 9</div><div class="t">Pipelining I</div></div>
<div class="wk"><div class="n">Wk 10</div><div class="t">Pipelining II</div></div>
<div class="wk"><div class="n">Wk 11</div><div class="t">Memory Hierarchy I</div></div>
<div class="wk"><div class="n">Wk 12</div><div class="t">Memory Hierarchy II</div></div>
<div class="wk"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

<!-- notes: Point out that Wk 8 is dashed like Wk 15: a checkpoint, not a
new layer of the machine. Everything behind it (Wk 1-7) is fair game
today. -->

---

<!-- SLOT 3: Recap + open wound (expanded for review week: 7 weeks, not 1) -->

# Seven Weeks, This Week

- **Weeks 1-7 delivered:** one real machine, built one layer at a time. We learned to measure it, represent its data, name its instructions, and build two circuits that run them
- **What's left today:** no new layer. Today we check that every piece you built still holds, in plain English, before the exam

Nothing here is new. If a slide feels new, it is really Week 1-7 content said a different way.

---

<!-- Recap-per-week: expansion of slot 3, one slide per week -->

# Week 1 Recap: Introduction

<div class="thread">Driving question: "What actually happens, step by step, when a computer runs one line of your code?"</div>

You should now be able to:
- Name the three layers between code and chip: **ISA**, **microarchitecture**, **hardware**
- Explain why two machines with the same clock speed can run at very different real speeds

---

# Week 2 Recap: Performance & Cost

<div class="thread">Driving question: how do we measure and compare speed precisely, instead of guessing with a stopwatch?</div>

You should now be able to:
- Compute **CPU time** from instruction count, CPI, and clock cycle time
- Apply **Amdahl's Law** to find the limit of speeding up only part of a system
- Explain why adding more cores does not always mean proportionally faster

---

# Week 3 Recap: Data Representation

<div class="thread">Driving question: how does a number become a bit pattern the ALU can actually act on?</div>

You should now be able to:
- Convert a number between decimal, binary, and hexadecimal
- Represent a negative number using **two's complement**
- Explain, in plain terms, how floating point stores a real number, and where overflow can happen

---

# Week 4 Recap: ISA I

<div class="thread">Driving question: which bit pattern means "add," and which means "load"?</div>

You should now be able to:
- Name the fields inside an instruction: opcode, registers, immediate/offset
- Tell two instruction formats apart (for example R-type versus I-type)
- Explain what an **addressing mode** is, in one sentence

---

# Week 5 Recap: ISA II · Quiz 1

<div class="thread">Driving question: is our instruction set complete enough to write a real program?</div>

You should now be able to:
- Use branch and jump instructions to write a loop or an if/else by hand
- Translate a short snippet of C-like code into assembly
- Explain what the stack holds during a procedure call

---

# Week 6 Recap: Single-Cycle

<div class="thread">Driving question: what circuit actually executes one instruction, start to finish?</div>

You should now be able to:
- Trace an instruction through the single-cycle datapath: fetch, decode, execute, memory, write-back
- Say which control signals a given instruction sets
- Explain why the clock period must fit the **slowest** instruction, even for fast ones

---

# Week 7 Recap: Multi-Cycle

<div class="thread">Driving question: how do we stop wasting a full clock cycle on every instruction, even fast ones?</div>

You should now be able to:
- Break one instruction's execution into several shorter cycles
- Explain how a finite-state-machine controller sequences those cycles
- Compare single-cycle and multi-cycle designs on cycle time versus cycles-per-instruction

---

<!-- Midterm format note: references Week 1 Course Logistics, does not repeat full policy -->

# Midterm Format, Quick Reminder

- **Closed collaboration:** work alone, no sharing answers with classmates
- **Restricted network:** no general internet access during the exam
- **Open-book, limited:** you may bring compiler syntax and reference sheets, nothing else

<div class="why">
Full grading and conduct policy is in Week 1's Course Logistics. This is
just the exam-day reminder, not the whole policy.
</div>

---

<!-- _class: section -->

# Check Yourself: Weeks 1-7
<div class="driving-q">Answer each pair on your own first. The answer follows on the next slide.</div>

---

<!-- SLOT N (expanded): Check yourself, block 1 -->

# Check Yourself: Weeks 1-2

1. Two laptops share the same ISA but perform very differently. What must differ?
2. A task spends 80% of its time in a part you can speed up 4x. What is the best possible overall speedup?

---

# Answers: Weeks 1-2

1. Their **microarchitecture** differs — the internal circuit design, even though the instruction set is the same
2. About **2.5x**, from Amdahl's Law: 1 / (0.2 + 0.8 / 4) = 1 / 0.4 = 2.5

---

# Check Yourself: Week 3

3. Why do computers use two's complement instead of a plain sign bit for negative numbers?
4. Convert -5 to 8-bit two's complement.

---

# Answers: Week 3

3. Two's complement lets the **same adder circuit** handle addition and subtraction for both signs. A plain sign bit needs extra logic and has two representations of zero
4. 5 is `00000101`. Flip every bit: `11111010`. Add 1: **`11111011`**

---

# Check Yourself: Week 4

5. Name three fields common to most instruction formats.
6. What is an "addressing mode," in plain words?

---

# Answers: Week 4

5. **Opcode** (what to do), **register fields** (which registers), and an **immediate/offset field** (a constant), depending on the instruction type
6. A rule for how an instruction finds its data: a register's value, a constant, or a register plus an offset

---

# Check Yourself: Week 5

7. Which instruction type lets a program repeat itself, i.e., create a loop?
8. What holds the return address during a procedure call?

---

# Answers: Week 5

7. A **conditional branch**, which jumps back to an earlier instruction when its condition holds
8. The **stack** (or a dedicated return-address register), so the processor knows where to resume

---

# Check Yourself: Week 6

9. In a single-cycle CPU, what sets the length of the clock period?
10. Name the five stages an instruction passes through in the single-cycle datapath.

---

# Answers: Week 6

9. The **slowest instruction's** total delay through the datapath — every instruction waits that long, even fast ones
10. **Fetch, decode/register read, execute (ALU), memory access, write-back**

---

# Check Yourself: Week 7

11. Why can a multi-cycle design finish a branch instruction faster than a single-cycle design does?
12. What component sequences the multiple cycles of one instruction?

---

# Answers: Week 7

11. Multi-cycle only spends as many cycles as an instruction needs. A branch skips the memory-access cycle it does not need; single-cycle cannot skip anything
12. A **finite-state-machine (FSM) controller**, which steps through states and asserts the right signals each cycle

---

<!-- SLOT N+1: "Limits" replaced by "What to focus on next" -->

# What to Focus On Next

<div class="limits">
Most points are usually lost in three places: Amdahl's Law arithmetic
(Week 2), two's complement conversions (Week 3), and tracing an
instruction through the single-cycle datapath (Week 6). Redo those
worked examples by hand, don't just re-read them.
</div>

---

<!-- SLOT N+2: Bridge -->

# After the Midterm

Week 7 left one thing unsolved: a working CPU that still does only **one
thing at a time**. **Week 9, Pipelining I**, picks that up directly:
overlapping instructions so the processor stays busy every cycle.

---

<!-- SLOT N+3: Summary -->

# Summary

- Weeks 1-7 built one machine, layer by layer: metrics, data, instructions, then two working datapaths
- Today added no new content, only consolidation and self-check
- **Reading:** re-skim Hennessy & Patterson chapters covered in Weeks 1-7, focus on worked examples, not new pages
- **Prepare:** bring your compiler/reference sheet; review Amdahl's Law, two's complement, and the single-cycle datapath trace first

---

<!-- SLOT N+4: Thank You -->
<!-- _class: end -->

# Thank You
