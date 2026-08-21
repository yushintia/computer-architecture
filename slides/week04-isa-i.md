---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 4: ISA I

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Quick reminder of where we are: Week 3 gave us bits for numbers,
text, and negative values. Today we start giving those bits a job:
telling the processor what to do. Keep energy up, this is the start of
"real" architecture content.
-->

---

<!-- SLOT 2: Where we are -->

# Where We Are

<div class="roadmap">
<div class="wk"><div class="n">Wk 1</div><div class="t">Introduction</div></div>
<div class="wk"><div class="n">Wk 2</div><div class="t">Performance &amp; Cost</div></div>
<div class="wk"><div class="n">Wk 3</div><div class="t">Data Representation</div></div>
<div class="wk now"><div class="n">Wk 4</div><div class="t">ISA I</div></div>
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
notes: Point at Week 4. Say: we measured speed, then wrote numbers as
bits. Today we write commands as bits. This is the vocabulary the rest
of the semester is built on.
-->

---

<!-- SLOT 3: Recap + open wound -->

# Last Week, This Week

- **Last week delivered:** Data Representation showed how any number, letter, or negative value can be written as bits
- **Last week left broken:** Bits are well-defined, but nothing yet says which bit pattern means "add" versus "load"

---

# Today's Session, in Three Parts

<div class="agenda-row">
<div class="agenda-badge">1</div>
<div class="agenda-text"><strong>Why we need an ISA</strong><span>The ambiguity problem, and what it actually costs</span></div>
</div>
<div class="agenda-row">
<div class="agenda-badge">2</div>
<div class="agenda-text"><strong>Where it came from, and its format</strong><span>History, the formal definition, and today's instruction format</span></div>
</div>
<div class="agenda-row">
<div class="agenda-badge">3</div>
<div class="agenda-text"><strong>Reading, writing, and practicing</strong><span>Fields, encoding practice, and a self-check</span></div>
</div>

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **Instruction:** one exact command a processor can carry out, like "add these two numbers"
- **Bit pattern:** a specific sequence of 0s and 1s, like `0101`
- **Opcode:** short for "operation code," the part of an instruction that says what to do
- **Operand:** the part of an instruction that says what to do it to

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), zero jargon -->

# One Bit Pattern, Two Guesses

<div class="pain">

At SmartPick, a technician is checking why Studio's video-export program
sometimes behaves oddly. Last week we learned that any number can be
written as a pattern of 0s and 1s. Now she is staring at one such
pattern, sitting in the laptop's memory, exactly as it will be carried
out.

Nothing about that pattern says what it means. It could be an order to
add two numbers together. It could just as easily be an order to load a
saved file from a different spot. The bits look the same either way. She
cannot tell which one it is, and neither can we, yet.

</div>

<!--
notes: Do not say "opcode" or "ISA" yet, even though those words appear
in the Key Words slide just before this one. Let the ambiguity sit. Ask:
"How would you even start solving this?" Take a few guesses.
-->

---

# The Same Bits, Read Two Ways

<div class="two-col">
<div>

<strong>Reading 1: "Add"</strong>

The pattern is read as: take two numbers already in the machine, add
them, and keep the result.

</div>
<div>

<strong>Reading 2: "Load"</strong>

The same pattern is read as: go fetch a saved value from somewhere else
in memory.

</div>
</div>

Both readings use the exact same bits. Without an agreed rule, both
guesses are equally valid, and equally useless.

<!-- notes: Let students notice this is not a trick question, it is a real gap. -->

---

# A Risky Shortcut: Guessing From Context

The technician tries a shortcut: read the instructions sitting nearby
and guess from the pattern around them. Sometimes the guess happens to
be right. Sometimes it is completely wrong, and nobody notices until the
program crashes.

<div class="why">
Guessing sometimes works, by luck. It is never something a whole company
can build software on. Every processor and every compiler needs one
fixed, written-down answer, not a series of educated guesses.
</div>

---

<!-- SLOT 5: Cost of not knowing -->

# What This Actually Costs

- A programmer cannot write a tool that turns code into working bit patterns, because "working" is undefined
- A hardware team cannot test a new chip, because there is no agreed answer for what each bit pattern should do
- Software built for one machine may not run correctly on another, if the two machines quietly disagree on meanings
- A support team burns hours debugging a crash that traces back to one misread instruction

<div class="why">
<strong>In industry:</strong> "walk me through what this instruction
does" is a common interview question for hardware and low-level software
roles. Real chip projects have failed when a new instruction set broke
compatibility with existing software.
</div>

---

# Small Mix-Up, Company-Wide Failure

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One student misreads one instruction</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 20%"></div></div>
  <div class="bar-value">one wrong homework answer</div>
</div>
<div class="bar-row">
  <div class="bar-label">One compiler team codes the wrong meaning</div>
  <div class="bar-track"><div class="bar-fill risk-med" style="width: 55%"></div></div>
  <div class="bar-value">every program it builds breaks</div>
</div>
<div class="bar-row">
  <div class="bar-label">One chip vendor changes instruction meanings</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 92%"></div></div>
  <div class="bar-value">existing software stops running</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

Same kind of mistake, three different sizes. This is why the agreement
we build today has to be exact.

---

# When Compatibility Breaks: A Real Example

<div class="thread">This is not hypothetical. It has happened to entire product lines.</div>

In 2001, Intel released Itanium, a processor with a new instruction set,
incompatible with existing x86 software. Companies had to rewrite their
programs to use it. Most did not bother.

<div class="why">
Itanium sales fell far short of expectations. Meanwhile, AMD's 2003
x86-64 extended the existing x86 instruction set instead of replacing
it, so old software kept running unchanged. x86-64 won the market.
</div>

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"How does hardware agree with software on what each bit pattern means, so 'add' always means add, everywhere?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

1. Define an ISA and explain what problem it solves
2. Identify the two parts of one instruction: opcode and operands
3. Read and write a simple add or subtract instruction using register names
4. Identify the fields of an R-type instruction, and encode one by hand

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Try It Preview: Worksheet Part A

Next session, you will work in pairs on
**[Worksheet Part A](materials/week04/worksheet.html)**.

- You will write and decode simple add and subtract instructions, using SmartPick's own registers
- Your pair identifies each instruction's fields: opcode, destination, and sources
- Then we compare answers together at the start of 차시 3

<div class="why">
Bring your notebook. No calculator needed, just the field names we
practice together first.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: who first solved this problem, and how?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **Register:** a tiny, very fast storage spot inside the processor, holds one value
- **Memory:** larger, slower storage outside the processor, holds most data and programs
- **ISA (Instruction Set Architecture):** the fixed agreement between hardware and software about what each instruction means
- **Instruction format:** the fixed pattern of fields inside every instruction's bits

---

<!-- SLOT 8: Origin -->

# This Problem Is Not New

<div class="thread">You just felt the pain. Now: who else felt it, and what did the field do?</div>

- **Early 1950s:** Kathleen Booth and colleagues build some of the first assembly languages, giving instructions readable names like "ADD" instead of raw numeric codes
- **1964:** IBM releases the System/360, a family of computers of very different sizes and prices, all sharing one instruction set. A customer's software now keeps working when they upgrade to a bigger machine

<div class="why">
Naming instructions did two things at once. It made programs easier for
humans to write, and it gave hardware one exact, fixed target to build
toward.
</div>

---

# From Names to a Standard

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1950s</div><div class="d">Assembly language<br>naming instructions for humans</div></div>
<div class="pt"><div class="dot"></div><div class="y">1964</div><div class="d">IBM System/360<br>one ISA, many machines</div></div>
<div class="pt"><div class="dot"></div><div class="y">2001</div><div class="d">Itanium vs x86-64<br>compatibility decides winners</div></div>
<div class="pt"><div class="dot"></div><div class="y">Today</div><div class="d">x86, ARM, RISC-V, MIPS<br>same idea, many implementations</div></div>
</div>

Every era needed the same fixed agreement between hardware and software.
Today we learn exactly what that agreement looks like.

---

<!-- SLOT 9: Core concept -->

# ISA: Definition

<div class="thread">Decades of solving the same problem point at one clear idea. Here it is.</div>

> An **Instruction Set Architecture (ISA)** is the fixed agreement
> between hardware and software. It says which bit patterns exist as
> instructions, and exactly what each one means.

- The ISA is a **menu**, not a kitchen: it lists what can be ordered, not how it gets cooked
- Two very different machines can share one ISA, the way SmartPick's Value and Studio laptops do
- The ISA does not change often. Software written years ago can still run, because the agreement held

---

# Real ISAs You Will Meet

<div class="thread">The ideas we build today are not just for this classroom.</div>

<div class="chip-row">
<span class="chip">x86-64: most laptops and desktops</span>
<span class="chip">ARM: phones, tablets, Apple Silicon</span>
<span class="chip">RISC-V: newer, open-source design</span>
<span class="chip">MIPS: this course's own teaching ISA</span>
</div>

Each real ISA lists hundreds of instructions. This week we start with
just two, using **MIPS**, the exact ISA this course builds a working
processor around, starting Week 6.

---

<!-- Act 3 / BUILD -->

# Two Kinds of Storage: Registers and Memory

<div class="thread">Before we can define an instruction, we need to know what it works on.</div>

| | Register | Memory |
|---|---|---|
| Location | Inside the processor | Outside the processor |
| Speed | Very fast | Slower |
| Amount | Very few (a handful) | A large amount |
| Holds | One value at a time | Most of a program's data |

Registers have short names, like `$t0`, `$t1`, `$t2`. This week's
instructions only use registers. Reaching into memory is next week's
job.

---

# This Week's Two Instructions: add and sub

<div class="thread">Just two instructions, but enough to see the whole idea clearly.</div>

- **`add`:** `add $t0, $t1, $t2` means: $t0 = $t1 + $t2
- **`sub`:** `sub $t0, $t1, $t2` means: $t0 = $t1 - $t2

Both read two registers, compute one result, and write it to a third
register.

<div class="why">
Neither instruction touches memory, and neither can make a decision.
Those two abilities are exactly what next week adds.
</div>

---

# Anatomy of an Instruction

<div class="thread">Now we can define the shape every instruction shares.</div>

Every instruction in our machine has two parts:

- **Opcode:** the "what to do" part. Example: `add`, `sub`
- **Operands:** the "what to do it to" part. Example: which registers hold the numbers

Think of it like a short command: **"add"** (opcode) **"the values in
$t1 and $t2"** (operands). Neither part alone is a complete instruction.

---

# Meet This Week's Instruction Format: R-type

<div class="thread">Add and sub both follow one fixed shape, called R-type.</div>

**R-type** means: compute using only registers already loaded, no
memory involved. Every R-type instruction has the same four fields, in
the same order:

<div class="pipeline">
<div class="stage"><div class="h">Opcode</div><div class="s">names the job</div></div>
<div class="stage"><div class="h">Dest</div><div class="s">where the answer goes</div></div>
<div class="stage"><div class="h">Src 1</div><div class="s">first input register</div></div>
<div class="stage"><div class="h">Src 2</div><div class="s">second input register</div></div>
</div>

<div class="why">
Here is a twist: add and sub actually share the exact same opcode. A
separate, hidden field tells them apart. Week 6 shows exactly how.
</div>

---

# Reading Your First Instruction

<div class="thread">Time to actually read one, in plain words first.</div>

Written in assembly form: **`add $t0, $t1, $t2`**

This means: take the value in **$t1**, add the value in **$t2**, and put
the result in **$t0**. $t1 and $t2 keep their original values.

- Opcode: shared with every R-type instruction
- Dest: `$t0`
- Src 1: `$t1`
- Src 2: `$t2`

---

# Identifying the Fields: Encoding by Hand

<div class="thread">Same instruction, now split into the exact fields a chip reads.</div>

Every register also has a number. For today's example: `$t0` = 8, `$t1`
= 9, `$t2` = 10.

`add $t0, $t1, $t2` becomes: opcode `0` (shared by every R-type
instruction), dest register `$t0` (8), src1 register `$t1` (9), src2
register `$t2` (10).

<div class="why">
We now know exactly where each piece lives. The one missing piece, the
hidden field that separates add from sub, waits until Week 6.
</div>

---

<!-- SLOT N-2: Worked example -->

# Case Study: One Instruction, Two Laptops

<div class="thread">Same running example, one new lens: what does this instruction actually mean?</div>

Somewhere inside Studio's video-export program sits the instruction
**`add $t3, $t4, $t5`**. Decoded: dest `$t3` (11), src1 `$t4` (12), src2
`$t5` (13). In plain words: $t3 = $t4 + $t5.

<div class="chip-row">
<span class="chip">Value: same ISA</span>
<span class="chip">Studio: same ISA</span>
<span class="chip">Same opcode, same fields</span>
<span class="chip">Same decoded meaning</span>
</div>

Value and Studio decode this exact instruction the same way. That shared
agreement is the ISA. How fast each machine actually carries it out is a
microarchitecture question, starting Week 6.

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week04/worksheet.html">Worksheet Part A</a></strong>. Write and label the
fields of a few add and sub instructions for SmartPick's checkout
register. About 15 minutes.
</div>

- Write down each field: opcode, dest, src1, src2
- It is OK to write "shared, not sure yet" for the opcode value
- We compare answers together, then reveal the register-number table

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work. Do not reveal the register-number table yet, that happens with
Part B.
-->

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: one more full round trip.</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **R-type instruction:** an instruction that computes using only registers, like `add` and `sub`
- **Opcode field:** the part of an instruction's bits that names its job
- **Register number:** the small number that identifies one register, like `$t0` = 8
- **Encode:** turn an assembly instruction into its exact fields
- **Decode:** turn an instruction's fields back into its meaning

---

# Practice: Decode and Encode One More

<div class="thread">One more full round trip, before the paired practice on the worksheet.</div>

Decode `sub $t6, $t1, $t2` (register numbers: `$t6` = 14, `$t1` = 9,
`$t2` = 10). Opcode: shared R-type opcode. Dest: `$t6` (14). Src1: `$t1`
(9). Src2: `$t2` (10). In words: $t6 = $t1 - $t2.

Now try encoding `add $t0, $t3, $t4` yourself, using `$t0` = 8, `$t3` =
11, `$t4` = 12. Check your fields against the next slide's reveal.

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week04/worksheet.html">Worksheet Part B</a></strong>. Check your Part A
fields against the register-number table, then encode and decode two new
instructions yourselves. About 15 minutes.
</div>

- The answer key explains why add and sub still share one opcode
- That hidden field is exactly what Week 6 reveals

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). Let pairs self-check, then try the encode/decode problems.
Cold-call 2-3 pairs to share an answer before moving on.
-->

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"The opcode alone is the whole instruction":** the operand fields matter just as much. The same opcode with different operands does completely different work
- **"add and sub must use different opcodes, since they do different jobs":** many R-type instructions actually share one opcode. A different field tells them apart, revealed in Week 6
- **"The ISA changes often, like an app update":** it does not. ISAs stay fixed for years, so old software keeps running on new hardware
- **"A register's number and its stored value are the same thing":** `$t0` is just a label for a storage spot. The number stored inside it can be anything

---

# What We Can Fully Describe So Far

| Category | This week's status |
|---|---|
| `add`, `sub` (R-type) | Named, and we can find every field, except one hidden one |
| Memory, decisions, loops | Not yet named — next week's job |

We can read and write add and sub by hand, field by field. Reaching
memory, deciding, and repeating still need instructions we have not
named yet.

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. Write the assembly form of an R-type instruction with dest `$t1`, src1 `$t2`, src2 `$t3`, that computes a subtraction
2. True or false: `add` and `sub` use different opcodes to tell them apart
3. Why can this week's instructions not check SmartPick's price list, sitting in memory?

<div class="why">
After this, take the short <a href="materials/week04/quiz.html">self-check quiz</a> (about 10 minutes) for more
practice. It is ungraded.
</div>

---

# Answers

1. **`sub $t1, $t2, $t3`**, meaning $t1 = $t2 - $t3
2. **False** — R-type instructions like add and sub share the same opcode. A hidden field tells them apart, revealed in Week 6
3. Add and sub only work on values already sitting in registers. Reaching memory needs a different kind of instruction, not covered yet

---

<!-- SLOT N+1: Limits (Act 4 / CLOSE), becomes Week 5 slot 4 -->

# What This Week's ISA Cannot Do Yet

<div class="limits">
We can name instructions, but not yet compute with the full instruction
set. We can read, write, and find the fields of add and sub by hand. But
nothing we learned reaches into memory, makes a decision, or repeats a
step. We do not even know yet exactly how the chip tells add apart from
sub in the bits. That gap is not a mistake, it marks exactly where next
week begins.
</div>

---

<!-- SLOT N+2: Bridge -->

# Next Week

Week 4 leaves **the complete instruction set** unsolved. **Week 5, ISA
II**, completes it: instructions that reach memory, make decisions, and
repeat, enough vocabulary to trace a whole program by hand. Week 5 also
carries **Quiz 1**.

---

<!-- SLOT N+3: Summary -->

# Summary

- An ISA is the fixed agreement between hardware and software about what each bit pattern means
- An instruction has two parts: opcode (what to do) and operands (what to do it to)
- This week: add and sub (R-type), named and split into fields; everything else waits for Week 5
- **You did today:** Worksheet Parts A and B, self-check quiz
- **Reading:** Hennessy & Patterson, Appendix A, Instruction Set Principles
- **Handout:** [materials/week04/handout.md](materials/week04/handout.html), glossary and the full SmartPick decode walkthrough
- **Prepare:** think about how a program could search a list of prices — what would it need, that add and sub alone cannot give it?

---

<!-- SLOT N+4: Thank You -->
<!-- _class: end -->

# Thank You
