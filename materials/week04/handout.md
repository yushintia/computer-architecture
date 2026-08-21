# Week 4 Handout: ISA I

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **Instruction** | One exact command a processor can carry out, like "add these two numbers" |
| **Bit pattern** | A specific sequence of 0s and 1s, like `0101` |
| **Opcode** | Short for "operation code," the part of an instruction that says what to do |
| **Operand** | The part of an instruction that says what to do it to |
| **Register** | A tiny, very fast storage spot inside the processor, holds one value |
| **Memory** | Larger, slower storage outside the processor, holds most data and programs |
| **ISA (Instruction Set Architecture)** | The fixed agreement between hardware and software about what each instruction means |
| **Instruction format** | The fixed pattern of fields inside every instruction's bits |
| **R-type instruction** | An instruction that computes using only registers, like `add` and `sub` |
| **Opcode field** | The part of an instruction's bits that names its job |
| **Register number** | The small number that identifies one register, like `$t0` = 8 |
| **Encode** | Turn an assembly instruction into its exact fields |
| **Decode** | Turn an instruction's fields back into its meaning |

---

## 2. The SmartPick Story, Worked Out Step by Step

This is the full version of the case study from class. Read it slowly if
the in-class pace felt fast.

**The situation.** Inside Studio's video-export program sits one
instruction, sitting in memory exactly as the processor will carry it
out. It is written as one bit pattern. Nothing about the raw bits says
what that pattern means: it could be "add two numbers" or "load a saved
value from memory." The bits look identical either way.

**Step 1: See why guessing fails.** A technician tries reading nearby
instructions and guessing the pattern's meaning from context. Sometimes
the guess is right, by luck. It is never something a whole company can
build software on — a compiler team, a chip team, and a support team all
need one fixed, written-down answer, not a series of educated guesses.

**Step 2: Meet the fix — the ISA.** An **Instruction Set Architecture
(ISA)** is the fixed agreement between hardware and software. It lists
which bit patterns exist as instructions, and exactly what each one
means. Think of the ISA as a **menu**, not a kitchen: it lists what can
be ordered, not how it gets cooked. Two very different machines —
SmartPick's Value and Studio laptops — can share one ISA.

**Step 3: Learn the two kinds of storage instructions work on.**

| | Register | Memory |
|---|---|---|
| Location | Inside the processor | Outside the processor |
| Speed | Very fast | Slower |
| Amount | Very few (a handful) | A large amount |
| Holds | One value at a time | Most of a program's data |

Registers have short names, like `$t0`, `$t1`, `$t2`. This week's
instructions only use registers.

**Step 4: Meet this week's two instructions.**

- `add $t0, $t1, $t2` means: `$t0 = $t1 + $t2`
- `sub $t0, $t1, $t2` means: `$t0 = $t1 - $t2`

Both read two registers, compute one result, and write it to a third
register. Neither touches memory, and neither can make a decision.

**Step 5: Split an instruction into its two parts.** Every instruction
has an **opcode** (the "what to do" part, like `add` or `sub`) and
**operands** (the "what to do it to" part, like which registers hold the
numbers). Neither part alone is a complete instruction.

**Step 6: Meet the R-type format.** `add` and `sub` both follow one
fixed shape called **R-type** — compute using only registers already
loaded, no memory involved. Every R-type instruction has the same four
fields, in the same order: **Opcode**, **Dest**, **Src 1**, **Src 2**.

**Step 7: Decode the case-study instruction, field by field.** Somewhere
inside Studio's video-export program sits the instruction
**`add $t3, $t4, $t5`**. Using the register numbers `$t3` = 11,
`$t4` = 12, `$t5` = 13:

| Field | Value | Meaning |
|---|---|---|
| Opcode | shared R-type opcode | this is an R-type computation |
| Dest | `$t3` (11) | where the answer goes |
| Src 1 | `$t4` (12) | first input |
| Src 2 | `$t5` (13) | second input |

In plain words: `$t3 = $t4 + $t5`.

**Step 8: State clearly what we can, and cannot, say yet.** Value and
Studio both decode this exact instruction the same way — dest `$t3`,
src1 `$t4`, src2 `$t5`, same meaning. That shared agreement is the ISA.
We *cannot* yet say exactly how the chip tells `add` apart from `sub` in
the bits — both share the same opcode, and a hidden field separates
them. That hidden field, and how fast each machine actually carries the
instruction out (a microarchitecture question), wait until Week 6.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations trimmed from the slides to keep
class time short. Read it if you are curious or want more examples.

**Why the field order stays fixed.** A chip does not "read" an
instruction the way a person reads a sentence — it has fixed wires
running to fixed bit positions. If one instruction's dest field could
sit anywhere, the hardware would need to guess where to look each time.
Keeping every R-type instruction's fields in the same order, same width,
same position is what makes cheap, fast decoding hardware possible at
all.

**Assembly language is a readability layer, not a new language.**
`add $t0, $t1, $t2` is not the actual instruction — it is a human-
readable stand-in for the exact bit pattern the processor stores and
executes. Kathleen Booth and colleagues introduced this idea in the
early 1950s, giving instructions names like "ADD" instead of raw numeric
codes. The bits underneath never change; only how conveniently a human
can write and read them changes.

**Why IBM System/360 (1964) mattered so much.** Before System/360, each
computer model typically had its own instruction set. A customer who
outgrew their machine and bought a bigger one usually had to rewrite
their software from scratch. System/360 was a whole family of machines,
cheap to expensive, that all shared one ISA. A customer's existing
software kept working when they upgraded — the first time that
promise held at large commercial scale.

**Itanium vs. x86-64, in a bit more detail.** In 2001, Intel released
Itanium with a brand-new instruction set, incompatible with existing
x86 software. Running old programs required either slow emulation or a
full rewrite; most companies did not bother rewriting, and Itanium sales
fell far short of expectations. In 2003, AMD took the opposite approach:
x86-64 *extended* the existing x86 ISA with new 64-bit capabilities
instead of replacing it. Old 32-bit software kept running unchanged, and
x86-64 became the industry standard. The lesson generalizes: an ISA is a
promise to every piece of software ever written against it, and breaking
that promise is expensive even when the new design is technically
better.

**Real ISAs you will meet outside this course.**

- **x86-64:** most laptops and desktops
- **ARM:** phones, tablets, Apple Silicon
- **RISC-V:** newer, open-source design, increasingly used in research and embedded systems
- **MIPS:** this course's own teaching ISA — simpler, and enough to build a real working processor by Week 6

**Where "opcode sharing" shows up elsewhere.** MIPS `add` and `sub`
sharing one opcode, with a hidden field telling them apart, is not a
one-off trick — it is a common way real ISAs pack many related
operations under one broad instruction family, saving opcode space for
other instructions. You will see the exact hidden field (the "function"
field) in Week 6, once the datapath needs to actually use it.

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.
Register numbers you may need: `$t0`=8, `$t1`=9, `$t2`=10, `$t3`=11,
`$t4`=12, `$t5`=13, `$t6`=14.

**Problem 1.** Write the assembly form of an R-type instruction with
dest `$t2`, src1 `$t0`, src2 `$t1`, that computes an addition.
> **Answer:** `add $t2, $t0, $t1`, meaning `$t2 = $t0 + $t1`

**Problem 2.** Decode `sub $t5, $t3, $t4` into its fields, and state its
meaning in words.
> **Answer:** Opcode: shared R-type opcode. Dest: `$t5` (13). Src1:
> `$t3` (11). Src2: `$t4` (12). In words: `$t5 = $t3 - $t4`.

**Problem 3.** True or false: since `add` and `sub` do different jobs,
they must use different opcodes. Explain in one sentence.
> **Answer:** False. Many R-type instructions, including `add` and
> `sub`, share the same opcode; a separate hidden field (revealed in
> Week 6) tells them apart.

**Problem 4.** A friend says: "The opcode alone tells you everything the
instruction does." Explain in one sentence why this is wrong.
> **Answer:** The opcode alone only names the general job; the operand
> fields (dest, src1, src2) say which specific registers it acts on, and
> the same opcode with different operands does completely different
> work.

**Problem 5.** Two laptops, Value and Studio, both decode
`add $t3, $t4, $t5` the same way. Does this tell you anything about
which laptop runs it *faster*? Explain in one sentence.
> **Answer:** No. Sharing an ISA guarantees both machines agree on what
> the instruction *means*; it says nothing about how fast either machine
> actually carries it out — that is a microarchitecture question.

**Problem 6.** Why can this week's instructions (`add`, `sub`) not check
SmartPick's price list, sitting in memory?
> **Answer:** `add` and `sub` only read and write values already sitting
> in registers. Reaching into memory needs a different kind of
> instruction, which this week has not named yet — that is next week's
> job.
