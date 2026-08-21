# Week 5 Handout: ISA II — Completing the Instruction Set

Computer Architecture (503872-004) — for students to keep and read
again. Use plain, simple English on purpose, so it is easy to read even
if English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **Register** | A small, fast storage spot inside the processor, holding one value |
| **Memory address** | A number that names one exact spot in memory |
| **Load instruction (`lw`)** | Copies one value from a memory address into a register |
| **Store instruction (`sw`)** | Copies one value from a register into a memory address |
| **Immediate value** | A small constant number written directly inside an instruction, not stored in a register |
| **Branch instruction** | An instruction that jumps to a different spot, only if a condition is true |
| **Jump instruction** | An instruction that always jumps to a different spot, no condition needed |
| **Loop** | A group of instructions repeated until some condition stops it |
| **Addressing** | How an instruction states exactly which memory spot it means, usually register plus offset |
| **Opcode** | The part of an instruction's bits that names which job it does |
| **Encoding** | Turning an instruction into its exact bit pattern |
| **Complete instruction set** | Enough instruction types to write any program, in principle |
| **R-type** | An instruction format that computes using only registers, like `add` and `sub` |
| **I-type** | An instruction format that uses a register plus a small built-in number, for loads, stores, branches, and constants |
| **J-type** | An instruction format that jumps straight to a new instruction address |
| **RISC** | A style of instruction set kept deliberately small and simple, from a 1980s Berkeley project |
| **Load-store architecture** | The RISC rule that only load and store instructions may touch memory; every other instruction works on registers only |

---

## 2. The SmartPick Story, Worked Out Step by Step

This is the full version of the story from class. Read it slowly if the
in-class pace felt fast.

**The situation.** A customer at SmartPick wants one exact laptop:
price tag **$780**. The clerk needs to check the shelf's price list, one
laptop at a time, and say whether that price is on the shelf today.

**What Week 4's instructions could not do.** Last week's instruction
set only had `add` and `sub`, working on values already sitting in
registers. It could not reach the price list sitting in memory, and it
could not repeat "check the next laptop" without writing the same lines
by hand, over and over.

**Step 1: Reach into memory.** The `lw` (load word) instruction copies
one price from memory into a register, so the processor can actually
look at it. Its address is built from a register plus a small offset
number, added together — this is called **addressing**.

**Step 2: Keep constants without a second register.** The `addi`
instruction adds a small constant directly into an instruction, with no
second register needed. This is how we set up a starting point (the
first price's address) and a counter (move to the next price).

**Step 3: Decide.** The `beq` (branch if equal) instruction jumps to a
different spot, only if two registers hold the same value. This is how
"is this the right price?" becomes a real, checkable instruction.

**Step 4: Repeat.** Combining a branch with a plain jump (`bne`, or `j`
for an unconditional jump) lets the program go back and check the next
laptop, instead of writing the same check ten separate times.

**The complete program:**

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

**Step 5: State clearly what we can, and cannot, say yet.** We *can* now
write a complete program on paper: load, decide, repeat, using the full
instruction set. We *cannot* yet say what actually happens, circuit by
circuit, when the processor runs even one of these instructions. That is
Week 6's job.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations trimmed from the slides to keep
class time short. Read it if you are curious or want more examples.

**Why "load-store" is a rule, not just a habit.** Some older instruction
sets (called CISC, "complex instruction set computer") let almost any
instruction touch memory directly, in many different ways. RISC's
1980s designers, including your textbook's own authors, chose the
opposite: keep memory access to exactly two instructions, `lw` and `sw`,
and make every other instruction work only on registers. Fewer rules
made chips easier to build fast — a theme Week 6 picks up directly.

**Branches versus jumps, one more time.** A branch instruction always
asks a question first: "are these two values equal?" A jump instruction
never asks anything — it always goes. Loops need both: the branch
decides whether to keep going, and the jump (built into `bne`/`beq`'s
own behavior, or a plain `j`) sends the program back to repeat.

**Where this shows up around you.**

- **RISC-V:** a modern, open-source ISA that follows the same load-store rule taught this week
- **ARM:** the RISC-style ISA inside almost every phone, tablet, and now many laptops
- **x86:** the older, CISC-style ISA inside most desktop and server processors
- **Compilers:** turn loops written in Python or C into exactly this pattern of load, branch, and jump instructions

**Who actually designs this, as a job.**

- **ISA designers** decide exactly which instructions exist, and how each is encoded
- **Compiler engineers** turn everyday loops and if-statements into instruction sequences like today's example
- **Verification engineers** check that a chip's circuits actually match what the ISA promises

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** Which instruction copies a value **from** memory **into**
a register: `lw` or `sw`?
> **Answer:** `lw` (load word). `sw` (store word) goes the opposite
> direction, from a register into memory.

**Problem 2.** A program needs to add the number 5 directly, with no
second register involved. Which instruction type is this: R-type,
I-type, or J-type?
> **Answer:** I-type. Instructions using a small built-in constant,
> like `addi`, are I-type.

**Problem 3.** In one sentence, explain why a branch instruction alone
cannot build a working loop.
> **Answer:** A branch only decides whether to jump; without a plain
> jump back to the top, the program never actually repeats the steps.

**Problem 4.** True or false: in a load-store architecture, an `add`
instruction can read one of its values directly from memory.
> **Answer:** False. Only `lw` and `sw` touch memory; `add` works only
> on values already sitting in registers.

**Problem 5.** Put these steps in the correct order for a search loop:
`check for a match (beq)`, `move to the next item (addi)`, `load the next
price (lw)`, `jump back if not done (bne)`.
> **Answer:** load the next price -> check for a match -> move to the
> next item -> jump back if not done.

**Problem 6.** A friend says: "RISC's small instruction set must be
weaker than a big one." Write one sentence of pushback, using this
week's ideas.
> **Answer (example):** A small, clean instruction set can still
> compute anything a big one can — RISC just builds every complex task
> out of a few simple, fast instructions instead of many complicated
> ones.
