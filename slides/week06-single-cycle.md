---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 6: Single-Cycle

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Welcome the class back from Quiz 1. Say: last week we finished the
full list of commands our machine understands. Today we build the actual
circuit that carries one of those commands out. Keep energy up, this is
where the course gets physical.
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
<div class="wk now"><div class="n">Wk 6</div><div class="t">Single-Cycle</div></div>
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
notes: Point at week 6. Say: we now stop drawing instructions on paper
and start building the machine that runs them. This is the halfway point
before the midterm.
-->

---

<!-- SLOT 3: Recap + open wound -->

# Last Week, This Week

- **Last week delivered:** we finished the full list of commands our machine understands, and checked our understanding with Quiz 1
- **Last week left broken:** the instruction list is complete on paper, but no circuit yet carries out a single command

<!-- notes: Keep this short. The "left broken" line is this week's pain slide, restated in plain words. Do not over-explain yet. -->

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **Datapath:** the wiring inside a chip that moves data from one part to another
- **Control unit:** the part of the chip that decides which wires turn on
- **Clock cycle:** one tick of the chip's clock, the smallest slice of time it works in
- **Instruction:** one single command, like "add these two numbers"

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), zero jargon -->

# A Perfect List, and a Silent Chip

<div class="pain">

SmartPick's chip team finishes their list of commands for the new laptop
chip. Every command is written down, checked twice, and complete. They
hand the list to the factory that builds test chips.

A week later, the first test chip arrives. An engineer feeds it one
simple command: add two numbers. Nothing happens. No light, no result,
no error. The chip has no wires connecting one part to another in the
right order. A perfect list on paper does not move a single number by
itself.

</div>

<!--
notes: Let this land. Ask: "What do you think is actually missing?"
Take 2-3 guesses. Someone will likely say "the wiring" or "the circuit."
Do not confirm yet, just move on.
-->

---

<!-- SLOT 5: Cost of not knowing -->

# What Else This Actually Costs

- A chip company cannot ship one working laptop, no matter how complete the command list is
- Software engineers have nothing to actually run their finished programs on
- A hardware team misses a launch date because "the list is done" gets mistaken for "the chip works"

<div class="why">
<strong>In industry:</strong> digital design interviews often ask you to
draw this exact wiring from memory. Companies like Intel, AMD, and Arm
hire engineers whose entire job is this circuit, not the instruction
list.
</div>

<!-- notes: Emphasize that "designing the ISA" and "building the circuit" are two different jobs, both real careers. -->

---

# Who Actually Builds This, As a Job

<div class="thread">This gap between "list" and "circuit" is a real, separate career.</div>

<div class="appgrid">
<div class="app"><div class="name">Computer Architect</div><div class="desc">designs the instruction list and the overall circuit plan</div></div>
<div class="app"><div class="name">Digital Design Engineer</div><div class="desc">draws and builds the exact datapath wiring, part by part</div></div>
<div class="app"><div class="name">Verification Engineer</div><div class="desc">tests the circuit against every instruction before it ships</div></div>
<div class="app"><div class="name">Embedded Engineer</div><div class="desc">builds small, simple chips using this same single-cycle idea</div></div>
</div>

These four jobs all exist because a finished instruction list still needs
a real circuit built underneath it.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"How do we build one circuit that carries out any instruction, start to finish, every clock tick?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

<div class="cardlist">
<div class="card"><div class="h">Datapath Parts</div><div class="d">Identify the datapath parts needed to run an instruction</div></div>
<div class="card"><div class="h">Instruction Flow</div><div class="d">Trace how one instruction flows through the datapath, step by step</div></div>
<div class="card"><div class="h">Control Signals</div><div class="d">Explain how control signals choose the right path for each instruction type</div></div>
<div class="card"><div class="h">Single-Cycle Waste</div><div class="d">Explain why a single-cycle design wastes time on simple instructions</div></div>
</div>

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Coming Up Next: Worksheet Part A

Next session, you will work in pairs on
**[Worksheet Part A](materials/week06/worksheet.html)**.

- You will see a simple datapath drawing with unlabeled wires
- Your pair predicts: which parts does an "add" instruction actually use?
- Then we check your prediction against the real datapath together

<div class="why">
Bring your notebook. No calculator needed, just the drawing we hand out.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: who actually built this circuit first?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **Register file:** a small, very fast set of storage slots inside the chip
- **ALU (Arithmetic Logic Unit):** the circuit that does math and comparisons
- **Program counter (PC):** a storage slot that always holds the address of the next instruction
- **Instruction memory:** the storage that holds the whole program, one instruction per address

---

<!-- SLOT 8: Origin -->

# Where the Single-Cycle Idea Came From

<div class="thread">You just felt the pain. Now: who solved it first, and how?</div>

- **Early 1980s:** researchers at Stanford (John Hennessy) and Berkeley (David Patterson) wanted a simple, correct-by-design processor
- A **single-cycle datapath** was the natural first design: one shared circuit, one clock tick per instruction

<div class="why">
Their research produced <strong>MIPS</strong>, one of the first RISC
processors. It is still the standard example used to teach datapath
design, which is why we use it this week.
</div>

<!-- notes: Note for students: RISC-V and Arm datapaths taught in later courses follow this exact same starting design. -->

---

<!-- SLOT 9: Core concept -->

# Single-Cycle Datapath: Definition

<div class="thread">One historical answer became this week's formal idea. Here it is.</div>

> A **single-cycle datapath** is a circuit design where every
> instruction, no matter its type, starts and finishes within exactly
> one clock cycle.

- The same physical circuit is reused for every instruction type
- The clock cycle length is fixed: it must fit the slowest instruction
- A **control unit** reads each instruction and switches on the right wires

---

<!-- Act 3 / BUILD -->

# The Five Main Parts of the Datapath

<div class="thread">Before tracing a single instruction, meet the parts it travels through.</div>

<div class="appgrid">
<div class="app"><div class="name">Program Counter</div><div class="desc">holds the address of the next instruction</div></div>
<div class="app"><div class="name">Instruction Memory</div><div class="desc">stores the program, returns one instruction per address</div></div>
<div class="app"><div class="name">Register File</div><div class="desc">small, fast storage the ALU reads and writes</div></div>
<div class="app"><div class="name">ALU</div><div class="desc">does math and comparisons on two values</div></div>
<div class="app"><div class="name">Data Memory</div><div class="desc">bigger, slower storage, used only by load and store</div></div>
<div class="app"><div class="name">Control Unit</div><div class="desc">reads the instruction, switches on the right wires</div></div>
</div>

---

# Following an Add Instruction

<div class="thread">One instruction type, four steps, one clock cycle.</div>

<div class="pipeline">
<div class="stage"><div class="h">Fetch</div><div class="s">PC points to instruction memory, reads the command</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Decode</div><div class="s">register file reads the two input values</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Execute</div><div class="s">the ALU adds the two values together</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Write Back</div><div class="s">the result is stored back in the register file</div></div>
</div>

An add instruction never touches data memory at all. Four steps, one
clock cycle.

---

# Following a Load Instruction

<div class="thread">A different instruction, one extra stop.</div>

<div class="pipeline">
<div class="stage"><div class="h">Fetch</div><div class="s">read the load command from instruction memory</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Decode</div><div class="s">register file reads the base address value</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Execute</div><div class="s">ALU computes the exact memory address</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Memory</div><div class="s">data memory is read at that address</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Write Back</div><div class="s">the loaded value is stored in a register</div></div>
</div>

A load instruction needs one extra real step: an actual trip to data
memory. Five steps, the same one clock cycle.

---

# Following a Branch Instruction

<div class="thread">A third instruction type, shorter this time.</div>

<div class="pipeline">
<div class="stage"><div class="h">Fetch</div><div class="s">read the branch command from instruction memory</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Decode</div><div class="s">register file reads the two values to compare</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Execute</div><div class="s">the ALU compares them and picks the next PC</div></div>
</div>

A branch instruction skips the memory and write-back steps entirely. It
still gets the exact same clock cycle as the other two.

---

# Following a Store Instruction

<div class="thread">A fourth path, the mirror image of load.</div>

<div class="pipeline">
<div class="stage"><div class="h">Fetch</div><div class="s">read the store command from instruction memory</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Decode</div><div class="s">register file reads the base address and the value to store</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Execute</div><div class="s">ALU computes the exact memory address</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Memory</div><div class="s">data memory is written at that address</div></div>
</div>

A store instruction writes to data memory instead of reading from it. It
skips write-back, because no register changes.

---

# Who Decides Which Path: The Control Unit

<div class="thread">Three different paths through one shared circuit. Something has to pick the path.</div>

The **control unit** reads the **opcode**, the short code naming the
instruction, and switches on only the wires that instruction needs.

| Instruction | RegWrite | MemRead | MemWrite | Branch |
|---|---|---|---|---|
| Add (R-type) | on | off | off | off |
| Load word | on | on | off | off |
| Store word | off | off | on | off |
| Branch | off | off | off | on |

Every instruction shares the same wires. Only the switches change.

---

# ALU Control: One Opcode, Many Operations

<div class="thread">One row of the table above, "Add (R-type)," actually hides several operations.</div>

- R-type instructions (add, subtract, and, or) all share the same opcode
- A second, smaller field inside the instruction, called **funct**, names the exact operation
- A small extra circuit, **ALU control**, reads funct and tells the ALU which operation to run

One opcode, one shared path, several possible ALU operations underneath.

---

# Sign Extension and Multiplexers: Handling Immediates

<div class="thread">Load and store carry a built-in number. It needs a special path too.</div>

- Load and store instructions include a small built-in number, an **immediate**, for the memory offset
- **Sign extension** stretches that short number to full size before the ALU can use it
- A **multiplexer**, or mux, then picks: does the ALU use a register value, or this extended immediate?

The mux is how one ALU input wire safely carries two different kinds of
value.

---

# One Clock Length for Every Instruction

<div class="thread">The control unit picks the path. The clock decides how long every path gets.</div>

- The clock cycle must be long enough for the **slowest** instruction: load word, which touches every part of the datapath
- A fast instruction, like add, finishes early but still must wait out the rest of that same clock cycle
- Nothing in a single-cycle design lets one instruction use a shorter cycle than another

This waiting is the seed of next week's problem.

---

# Picking the Next PC

<div class="thread">One more mux, hiding right before the next cycle even starts.</div>

- Normally, the next instruction address is simply the current one plus four
- If a branch is taken, the next address instead comes from the ALU's comparison result
- A mux at the program counter picks between these two, based on the **Branch** control signal

Even choosing "what comes next" needs its own small piece of the
datapath.

---

# Two Adders, Not One

<div class="thread">A small design detail that trips students up every year.</div>

- The main ALU is busy every cycle doing the instruction's real work: add, compare, compute an address
- The PC still needs "current address plus four" computed every single cycle, even during that same work
- Real single-cycle datapaths add a **second**, separate adder, just for this PC-plus-four step

One shared ALU cannot also handle PC math without a second adder beside
it.

---

# Datapath Recap: All Four Paths, Side by Side

<div class="thread">Four instruction types, one shared circuit, very different real work.</div>

| Instruction | Fetch | Decode | Execute | Memory | Write Back |
|---|---|---|---|---|---|
| Add (R-type) | yes | yes | yes | no | yes |
| Load word | yes | yes | yes | read | yes |
| Store word | yes | yes | yes | write | no |
| Branch | yes | yes | yes | no | no |

Every row shares the same fetch, decode, and execute steps. Only memory
and write-back actually differ.

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week06/worksheet.html">Worksheet Part A</a></strong>. You will see an
unlabeled datapath drawing and mark which parts an add instruction
actually uses. About 15 minutes.
</div>

- Circle every part the signal actually passes through
- Cross out any part add does not need
- We compare answers together at the start of 차시 3

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work. Do not confirm any answers yet, the real discussion happens next
session.
-->

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: exactly how much time does this waste?</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **Opcode:** the short code inside an instruction that names which operation to do
- **Multiplexer (mux):** a switch that picks one of several input wires to pass through
- **Control signal:** one on/off wire the control unit sets, like RegWrite or MemRead
- **Critical path:** the slowest chain of steps a single clock cycle must wait for

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week06/worksheet.html">Worksheet Part B</a></strong>. Check your Part A
answer against the real datapath, then compute real timing numbers.
About 15 minutes.
</div>

- The answer key shows exactly which wires add, load, and branch each use
- You will compute how much time add and branch waste, in picoseconds

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). Let pairs self-check, then work the timing numbers. Cold-call
2-3 pairs to share their wasted-time number before moving on.
-->

---

# Trace It Together: One Real Instruction

<div class="thread">Every part from this session, now with real numbers instead of names.</div>

Instruction: `add $t0, $t1, $t2`, where `$t1` holds 5 and `$t2` holds 7.

<div class="cardlist">
<div class="card"><div class="h">Fetch</div><div class="d">PC points to this instruction in instruction memory</div></div>
<div class="card"><div class="h">Decode</div><div class="d">register file reads <code>$t1</code> = 5 and <code>$t2</code> = 7</div></div>
<div class="card"><div class="h">Execute</div><div class="d">the ALU adds them, producing 12</div></div>
<div class="card"><div class="h">Write Back</div><div class="d">12 is stored into <code>$t0</code></div></div>
</div>

Control signals for this instruction: RegWrite = on, MemRead = off,
MemWrite = off, Branch = off.

---

<!-- SLOT N-2: Worked example -->

# Case Study: Timing SmartPick's Chip

<div class="thread">Same running example, now with real numbers on the datapath.</div>

| Step | Time it takes |
|---|---|
| Instruction fetch | 200 ps |
| Register read | 100 ps |
| ALU operation | 200 ps |
| Data memory access | 200 ps |
| Register write | 100 ps |

**Add:** fetch + read + ALU + write = 600 ps
**Load:** fetch + read + ALU + memory + write = 800 ps
**Branch:** fetch + read + ALU = 500 ps

---

# Case Study: Where the Wasted Time Goes

<div class="thread">One shared clock cycle, three very different real needs.</div>

The clock cycle must fit the slowest instruction, load, at **800 ps**.
Every instruction gets exactly that same length, whether it needs it or
not.

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">Add (needs 600 ps)</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 75%"></div></div>
  <div class="bar-value">wastes 200 ps every cycle</div>
</div>
<div class="bar-row">
  <div class="bar-label">Branch (needs 500 ps)</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 62%"></div></div>
  <div class="bar-value">wastes 300 ps every cycle</div>
</div>
<div class="bar-row">
  <div class="bar-label">Load (needs 800 ps)</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">wastes nothing</div>
</div>
</div>

---

# Why Not Just Skip the Wait?

<div class="why">
Every part of the datapath shares one single clock signal. A chip
cannot quietly hand add a shorter tick and load a longer one within the
same design. All instructions must fit inside one shared cycle length,
which is why the slowest instruction sets the pace for every other one.
</div>

That single shared clock is exactly what next week's design changes.

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"A faster instruction gets a faster clock cycle":** it does not. Single-cycle design gives every instruction the exact same fixed length
- **"More datapath parts always make a design better":** any part adds delay to every instruction, even ones that skip it
- **"Single-cycle means the chip does only one thing":** it means one instruction finishes per clock tick, not one operation type

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. Put these steps in order for a load instruction: write back, execute, memory, fetch, decode
2. Using this week's timing numbers, why does a branch instruction waste more time than an add instruction?
3. True or false: a single-cycle datapath can give a fast instruction a shorter clock cycle than a slow one

<div class="why">
After this, take the short <a href="materials/week06/quiz.html">self-check quiz</a> for more
practice. It is ungraded.
</div>

---

# Answers

1. **Fetch -> Decode -> Execute -> Memory -> Write Back**
2. Branch only needs 500 ps (fetch, decode, compare), but the clock cycle
   is fixed at 800 ps for load, so branch wastes 300 ps every cycle
3. **False.** Every instruction shares one clock signal, so all
   instructions get the exact same fixed cycle length

---

<!-- SLOT 14: Limits (Act 4 / CLOSE), becomes Week 7 slot 4 -->

# What Single-Cycle Design Cannot Do Yet

<div class="limits">
A working datapath exists, but it wastes a full clock cycle on every
instruction, even fast ones. Knowing every instruction works is not the
same as making every instruction run without waste.
</div>

---

<!-- SLOT 15: Bridge -->

# Next Week

Week 6 leaves **wasted time on every fast instruction** unsolved. **Week
7, Multi-Cycle**, addresses it: breaking execution into separate steps,
so each instruction only uses the cycles it actually needs.

---

<!-- SLOT 16: Summary -->

# Summary

- The datapath has five main parts: PC, instruction memory, register file, ALU, data memory, plus a control unit
- Add, load, and branch each take a different real path, but single-cycle design gives every one the same cycle length
- The control unit reads the opcode and sets control signals like RegWrite, MemRead, MemWrite, and Branch
- One shared clock cycle, fixed to the slowest instruction, is exactly what wastes time on every faster one
- **You did today:** Worksheet Parts A and B, self-check quiz
- **Reading:** Hennessy & Patterson, 6th ed., Chapter 4 (The Processor)
- **Handout:** [materials/week06/handout.md](materials/week06/handout.html), glossary and the full SmartPick timing walkthrough
- **Prepare:** think about how you would split load's five steps into separate, shorter cycles

---

<!-- SLOT 17: Thank You -->
<!-- _class: end -->

# Thank You
