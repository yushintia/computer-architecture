---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 5: ISA II · Quiz 1

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Remind students Quiz 1 happens near the end of class today, in
차시 3, about 15 minutes, closed-book, covering Weeks 1-5. Today still
teaches new material first.
-->

---

<!-- SLOT 2: Where we are -->

# Where We Are

<div class="roadmap">
<div class="wk"><div class="n">Wk 1</div><div class="t">Introduction</div></div>
<div class="wk"><div class="n">Wk 2</div><div class="t">Performance &amp; Cost</div></div>
<div class="wk"><div class="n">Wk 3</div><div class="t">Data Representation</div></div>
<div class="wk"><div class="n">Wk 4</div><div class="t">ISA I</div></div>
<div class="wk now"><div class="n">Wk 5</div><div class="t">ISA II · Quiz 1</div></div>
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

<!-- notes: Point at Week 5. Say: last week we named instructions. Today
we finish the instruction set, then take Quiz 1 near the end of class. -->

---

<!-- SLOT 3: Recap + open wound -->

# Last Week, This Week

- **Last week delivered:** we named real instructions, like add and subtract, and saw how each becomes a pattern of bits
- **Last week left broken:** we can name instructions, but we still cannot compute with the full instruction set

<!-- notes: This is Week 4's Limit slide, restated almost verbatim. It is
today's pain, not a new idea. -->

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **Register:** a small, fast storage spot inside the processor, holding one value
- **Memory address:** a number that names one exact spot in memory
- **Load instruction:** an instruction that copies a value from memory into a register
- **Store instruction:** an instruction that copies a value from a register into memory

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), zero jargon -->

# One Exact Laptop, Ten Instructions Too Few

<div class="pain">

A customer asks SmartPick for one exact laptop: price tag $780. The
clerk needs to check ten laptops on the shelf, one by one.

She writes a program using last week's instructions: add and subtract
only. She hits two walls right away.

First, she cannot reach into the shelf's price list sitting in memory.
Her instructions only work on two values already sitting in registers.

Second, she cannot repeat "check the next laptop" without writing the
same lines by hand, ten separate times.

Her instructions can compute. They cannot look things up, and they
cannot repeat themselves.

</div>

<!-- notes: Do not say "load," "branch," or "loop" yet, even though
those are exactly the missing pieces. Let the class sit with the gap. -->

---

# One Set of Tools, Not Enough Jobs

<div class="two-col">
<div>

**What we have (Week 4)**
- add, subtract
- work only on registers already loaded

</div>
<div>

**What the job needs**
- read a price list from memory
- repeat "check the next one"
- decide: is this the right price?

</div>
</div>

Two tools, three new jobs. That gap is today's whole lecture.

---

<!-- SLOT 5: Cost of not knowing -->

# What Else This Actually Costs

- Without memory access, a program can only use values already loaded into registers
- Without loops, no program can process a list, no matter how short
- Without branches, a program can never make a decision or skip a step

<div class="why">
<strong>In industry:</strong> "write a loop in assembly" is a standard
interview and lab exercise. Real ISAs — x86, ARM, RISC-V — all need
these same three pieces to run any real software.
</div>

---

# This Gap Shows Up in Every Real Program

<div class="appgrid">
<div class="app"><div class="name">Web apps</div><div class="desc">loop over search results, one row at a time</div></div>
<div class="app"><div class="name">Games</div><div class="desc">check "did the player win?" every single frame</div></div>
<div class="app"><div class="name">Spreadsheets</div><div class="desc">sum a column by repeating one add, many times</div></div>
</div>

Every one of these needs a loop, a decision, or a memory lookup. Last
week's instructions alone cannot do any of them.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"How do we extend our instruction set so it can look things up, decide, and repeat?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

<div class="cardlist">
<div class="card"><div class="h">Load & Store</div><div class="d">Explain what load and store instructions do, and why we need them</div></div>
<div class="card"><div class="h">Branch & Jump</div><div class="d">Explain how branch and jump instructions build a decision or a loop</div></div>
<div class="card"><div class="h">Full Programs</div><div class="d">Read a short assembly program that uses the complete instruction set</div></div>
<div class="card"><div class="h">Tracing SmartPick</div><div class="d">Trace SmartPick's "find this exact price" program, instruction by instruction</div></div>
</div>

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Coming Up Next: Worksheet Part A

Next session, you will work in pairs on
**[Worksheet Part A](materials/week05/worksheet.html)**.

- You will get a short SmartPick price list, sitting in memory
- Your pair writes, in plain words, the steps a search loop needs
- Then we turn your steps into real instructions together

<div class="why">
Bring your notes from last week on add and subtract. No calculator
needed.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: where did loops and branches come from?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **Branch instruction:** jumps to a different spot, only if a condition is true
- **Jump instruction:** always jumps to a different spot, no condition needed
- **Loop:** a group of instructions repeated until some condition stops it
- **Addressing:** how an instruction says exactly which memory spot it means

---

<!-- SLOT 8: Origin -->

# Where Loops and Branches Came From

<div class="thread">You just felt the pain. Now: who solved it, and how?</div>

- **1945:** von Neumann's design already needed a way to skip or repeat steps
- **1949:** EDSAC, an early stored-program computer, built in a conditional jump from day one
- **1980s:** Patterson and Hennessy — your textbook's authors — helped design RISC at Berkeley
- RISC followed one strict rule: only load and store instructions may touch memory

<div class="why">
That rule is called <strong>load-store architecture</strong>. It splits
instructions into three clean jobs: compute, move data, and decide what
runs next.
</div>

---

# Forty Years to a Clean Rule

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1945</div><div class="d">Von Neumann<br>needs to repeat steps</div></div>
<div class="pt"><div class="dot"></div><div class="y">1949</div><div class="d">EDSAC<br>first conditional jump</div></div>
<div class="pt"><div class="dot"></div><div class="y">1980s</div><div class="d">RISC project<br>load-store rule</div></div>
<div class="pt"><div class="dot"></div><div class="y">Today</div><div class="d">RISC-V, ARM, x86<br>same three jobs, still</div></div>
</div>

Every design since keeps the same three jobs: compute, move data, and
decide what runs next.

---

<!-- SLOT 9: Core concept -->

# Instruction Types: Definition

<div class="thread">Forty years of engineering point at three clean jobs. Here they are.</div>

> An **instruction format** is the fixed layout of bits an instruction
> uses. Different jobs use different formats: one for computing, one
> for memory and constants, one for jumping.

- **R-type:** compute using only registers (last week's add, subtract)
- **I-type:** use a register plus a small built-in number, for loads, stores, and branches
- **J-type:** jump straight to a new instruction address

These three formats, together, are what "the full instruction set"
means.

---

<!-- Act 3 / BUILD -->

# Reaching Into Memory: Load and Store

<div class="thread">The first missing piece: getting data out of memory at all.</div>

- **Load (`lw`):** copies one value from a memory address into a register
- **Store (`sw`):** copies one value from a register into a memory address
- Both need an address: **register + a small offset number**, added together

SmartPick's price list, sitting in memory, is finally reachable.

---

# Constants Without a Second Register

<div class="thread">Not every number worth using is already in a register.</div>

- **`addi`** adds a small constant number directly, no second register needed
- Useful for counters: "add 1," "start at 0," "compare to 10"
- Every loop needs a counter. This is how we get one, cheaply

---

# Making a Decision: Branch Instructions

<div class="thread">The second missing piece: skipping a step, only sometimes.</div>

- **`beq`** (branch if equal): jump, only if two registers hold the same value
- **`bne`** (branch if not equal): jump, only if two registers differ
- If the condition is false, the program just continues to the next line

This is how "is this the right price?" becomes a real instruction.

---

# Always Moving: Jump Instructions

<div class="thread">The third missing piece: repeating a block of steps, on purpose.</div>

- **`j`**: always jumps to a new spot, no condition
- **`jal`**: jumps, and remembers where to come back — for calling reusable code
- Combine a jump with a branch, and you can build a loop that repeats until done

---

# Putting It Together: A Loop

<div class="thread">One small pattern, built from pieces you now have.</div>

```
loop:
  ...do work...
  addi $t1, $t1, 1     # move to the next item
  bne  $t1, $t2, loop  # if not done, jump back
```

- The branch checks: are we done yet?
- The jump sends us back to repeat, if not
- This exact pattern runs almost every loop you will ever write

---

<!-- SLOT N-2: Worked example -->

# Case Study: SmartPick's Price-Search Program

<div class="thread">Same running example. Now it finally has the tools it needs.</div>

```
addi $t0, $zero, 780   # target price we're looking for
addi $t1, $a0, 0       # t1 = address of first price
addi $t2, $a0, 40      # t2 = address just past the list

loop:
lw   $t3, 0($t1)       # t3 = this laptop's price
beq  $t3, $t0, found   # match! stop here
addi $t1, $t1, 4       # move to the next laptop
bne  $t1, $t2, loop    # if list not done, repeat

found:
```

Four kinds of instructions work together here. `addi` sets values,
`lw` reads memory, `beq` checks for a match, and the loop repeats with
`bne` until it is found.

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week05/worksheet.html">Worksheet Part A</a></strong>. You get SmartPick's price list in
memory. Turn plain steps into real instructions. About 15 minutes.
</div>

- Write out your loop in plain words first
- Then match each step to load, store, branch, or jump
- We check answers together at the start of 차시 3

<!--
notes: Hand out or project Worksheet Part A now. Walk around while
pairs work. Do not confirm any answers yet, the real check happens next
session.
-->

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: checking your loop, then Quiz 1.</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **Opcode:** the part of an instruction's bits that names which job it does
- **Encoding:** turning an instruction into its exact bit pattern
- **Complete instruction set:** enough instruction types to write any program, in principle

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week05/worksheet.html">Worksheet Part B</a></strong>. Check your Part A loop
against the answer key, then encode two instructions by hand. About 15
minutes.
</div>

- The answer key shows one correct way to write the loop, not the only way
- Encoding by hand shows exactly where opcode, registers, and offsets each live

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). After ~15 minutes, cold-call 1-2 pairs before moving on. Keep
this tight today, Quiz 1 follows shortly.
-->

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"A branch alone makes a loop":** a branch only decides. You still need a jump to actually go back and repeat
- **"Load and store are the same instruction":** load reads memory into a register. Store writes a register into memory — the opposite direction
- **"More instructions always means a better ISA":** RISC deliberately kept the set small. Fewer, simpler instructions can still compute anything

---

<!-- NEW: Quiz 1 logistics, required by this week's embedded graded quiz -->

# Quiz 1 Today

<div class="why">
<strong>Quiz 1</strong> is next: closed-book, covers Weeks 1-5, about
15 minutes.
</div>

- Put away notes and laptops when your instructor says start
- We resume the slides right after

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. Which instruction type reaches into memory: R-type, I-type, or J-type?
2. In your own words, explain why a branch alone cannot build a loop
3. True or false: RISC's load-store rule lets every instruction touch memory directly

<div class="why">
After Quiz 1, take the short <a href="materials/week05/quiz.html">self-check quiz</a> for more
practice. It is ungraded.
</div>

---

# Answers

1. **I-type** — loads and stores both use a register plus a small offset number
2. A branch only decides whether to jump. Without a jump back, the program never repeats the steps
3. **False** — only load and store touch memory. That is the whole point of the load-store rule

---

<!-- SLOT 14: Limits (Act 4 / CLOSE), becomes Week 6 slot 4 -->

# What This Week's Instruction Set Cannot Do Yet

<div class="limits">
We now have a complete instruction set: compute, move data, decide, and
repeat. But nothing yet executes it — no circuit reads these
instructions and actually runs them. Knowing the instructions is not
the same as building the machine that carries them out.
</div>

---

<!-- SLOT 15: Bridge -->

# Next Week

Week 5 leaves **no circuit yet executes this instruction set** unsolved.
**Week 6, Single-Cycle**, solves it: a real datapath that reads,
decodes, and runs every instruction we defined this week.

---

<!-- SLOT 16: Summary -->

# Summary

- The instruction set now has three formats: R-type (compute), I-type (memory, constants, branches), J-type (jump)
- Load and store move data between memory and registers; branch and jump build decisions and loops
- RISC's load-store rule, from the 1980s, keeps the instruction set small and clean
- **You did today:** Worksheet Parts A and B, Quiz 1, self-check quiz
- **Reading:** Hennessy & Patterson, 6th ed., Chapter 2 (instruction set sections)
- **Handout:** [materials/week05/handout.md](materials/week05/handout.html), glossary and the full SmartPick program walkthrough
- **Prepare:** think about what "runs" an instruction — what would a circuit need to do, step by step?

---

<!-- SLOT 17: Thank You -->
<!-- _class: end -->

# Thank You
