# Week 8 Review Guide: Midterm (Weeks 1-7)

Computer Architecture (503872-004) — for students to study from before
the midterm. Same 12 questions as the "Check Yourself" section of the
Week 8 slides, with fuller worked explanations than fit on a slide.
Organized by week. Read the matching week's slides first if a question
still feels unfamiliar.

Midterm format reminder: closed collaboration (work alone), restricted
network (no general internet), open-book for compiler syntax and
reference sheets only. Full policy is in Week 1's Course Logistics.

---

## Week 1: Introduction

**Q1. Two laptops share the same ISA but perform very differently. What must differ?**

> **Answer:** Their **microarchitecture** — the actual circuit design
> used to carry out the ISA's instructions.

**Why:** The ISA is the fixed "menu" of commands a processor understands
— it only guarantees that the *same software* runs on both machines. It
says nothing about *how fast* that software runs. Two processors can
implement the identical menu with very different internal designs: one
may finish an instruction in fewer effective steps, use a bigger cache
so it visits slow main memory less often, or run at a newer, more
efficient microarchitecture generation. That is exactly the SmartPick
"Value vs. Studio" story: same 3.0 GHz, same ISA, but Studio's newer
microarchitecture and larger cache make it more than twice as fast on
the same task.

---

## Week 2: Performance & Cost

**Q2. A task spends 80% of its time in a part you can speed up 4x. What is the best possible overall speedup?**

> **Answer:** About **2.5x**.

**Why (Amdahl's Law):**

```
Speedup = 1 / ( (1 - F) + F/S )
```

where `F` is the fraction of time spent in the part you can improve, and
`S` is how much faster that part becomes.

Here `F = 0.8` and `S = 4`:

```
Speedup = 1 / ( (1 - 0.8) + 0.8/4 )
        = 1 / ( 0.2 + 0.2 )
        = 1 / 0.4
        = 2.5
```

**Common mistake:** students forget the *unimproved* 20% of the task
still takes its full original time. No matter how much you speed up the
80% part — even making it instant (`S = infinity`) — the overall speedup
caps at `1 / (1 - F) = 1 / 0.2 = 5x`. This is why Amdahl's Law is also
the reason "just add more cores" has diminishing returns: the serial
(non-parallelizable) fraction of a program limits the total speedup no
matter how many cores you add.

---

## Week 3: Data Representation

**Q3. Why do computers use two's complement instead of a plain sign bit for negative numbers?**

> **Answer:** Two's complement lets the same adder circuit handle both
> addition and subtraction, for both positive and negative numbers,
> without special-case hardware.

**Why:** With a plain "sign-magnitude" representation (one bit for sign,
the rest for magnitude), addition hardware needs extra logic to check
signs and decide whether to add or subtract magnitudes. Sign-magnitude
also has **two representations of zero** (`+0` and `-0`), which wastes a
bit pattern and complicates comparisons. Two's complement avoids both
problems: subtraction becomes "add the two's complement," so one adder
circuit does both jobs, and there is exactly one representation of zero.

**Q4. Convert -5 to 8-bit two's complement.**

> **Answer:** `11111011`

**Worked steps:**
1. Write 5 in 8-bit binary: `00000101`
2. Flip every bit (one's complement): `11111010`
3. Add 1: `11111010 + 1 = 11111011`

**Check it:** `11111011` interpreted as two's complement is
`-(2^7) + 2^6 + 2^5 + 2^4 + 2^3 + 2^1 + 2^0 = -128 + 64+32+16+8+2+1 = -5`. Correct.

*Related, not on the slide but worth knowing:* IEEE 754 floating point
uses a different scheme entirely (sign bit, exponent, mantissa) to
represent real (fractional) numbers, and can overflow to infinity or
underflow toward zero — review the format if you are unsure how a
fraction like 0.1 is stored.

---

## Week 4: ISA I

**Q5. Name three fields common to most instruction formats.**

> **Answer:** **Opcode** (what operation to do), **register fields**
> (which registers are the source/destination operands), and an
> **immediate or address/offset field** (a constant value, present in
> some formats and not others).

**Why:** Every instruction format starts with an opcode so the control
unit knows what circuit to activate. R-type (register-to-register)
formats spend the rest of their bits on register fields, since all
operands already live in registers. I-type (immediate) formats trade one
register field for an immediate constant, useful for `load`, small
arithmetic, and branch offsets. Knowing which fields a format has tells
you, at a glance, what kind of operand that instruction can use.

**Q6. What is an "addressing mode," in plain words?**

> **Answer:** A rule for how an instruction finds the data it operates
> on — for example, a value already sitting in a register, a constant
> written directly in the instruction, or an address computed from a
> register's value plus an offset.

**Why:** The same opcode (say, "load") can behave differently depending
on addressing mode: load from a fixed address, load from wherever a
register points, or load from a register plus a small offset (useful for
arrays and structs). Addressing modes are why an ISA can express many
different memory-access patterns using only a handful of instructions.

---

## Week 5: ISA II · Quiz 1

**Q7. Which instruction type lets a program repeat itself, i.e., create a loop?**

> **Answer:** A **conditional branch** instruction, which jumps back to
> an earlier instruction in the program when its condition is true.

**Why:** A loop is just "keep going back to the top while some condition
holds." A conditional branch (for example `beq`, "branch if equal")
compares two values and, if the condition holds, changes the program
counter to point somewhere else instead of the next instruction in
sequence. Placing the branch target *behind* the current instruction is
what produces a loop; placing it *ahead* produces an if/else skip.
Unconditional jumps move control flow too, but cannot by themselves
create a *repeating* loop — they need a conditional check to eventually
stop.

**Q8. What holds the return address during a procedure call?**

> **Answer:** The **stack** (in memory), or a dedicated return-address
> register for a single level of call, so the processor knows where to
> resume after the called procedure finishes.

**Why:** When a program calls a procedure, it must remember where to
continue once that procedure returns. Many ISAs put the return address
in a special register (e.g., a "link register") for a single call, but
because procedures can call other procedures (nested calls), that single
value must be *pushed onto the stack* before the next call overwrites
it, and *popped* back off when returning. The stack also holds local
variables and saved registers for each active call — together called a
"stack frame" or "activation record."

---

## Week 6: Single-Cycle

**Q9. In a single-cycle CPU, what sets the length of the clock period?**

> **Answer:** The **slowest instruction's** total delay through the
> datapath. Every instruction, even a fast one, must wait a full clock
> period, because all instructions share one fixed-length cycle.

**Why:** In a single-cycle design, one instruction completes in exactly
one clock cycle, so that cycle's length must be long enough for the
*worst-case* instruction to finish (typically `load word`, which touches
the register file, ALU, and memory in sequence). A simple instruction
like `add` finishes its real work much sooner but still has to "wait
out" the rest of the cycle doing nothing useful. This wasted time is
exactly the limitation Week 7's multi-cycle design fixes.

**Q10. Name the five stages an instruction passes through in the single-cycle datapath.**

> **Answer:** **Instruction fetch, decode/register read, execute (ALU),
> memory access, write-back.**

**Why:** These five stages describe the path *any* instruction takes
through the hardware in one cycle, though not every instruction uses
every stage's result: fetch reads the instruction from memory; decode
reads the source registers and figures out control signals; execute
computes an address or a result in the ALU; memory access reads or
writes data memory (skipped in effect by instructions like `add`); and
write-back stores a result into the register file (skipped by `store`
and branches). This same five-stage shape reappears in Week 9's
pipelined datapath — recognizing it now pays off later.

---

## Week 7: Multi-Cycle

**Q11. Why can a multi-cycle design finish a branch instruction faster than a single-cycle design does?**

> **Answer:** A multi-cycle design only spends as many (shorter) cycles
> as an instruction actually needs. A branch does not need a
> memory-access step, so it skips that cycle entirely. A single-cycle
> design cannot skip anything — every instruction pays for the full,
> fixed-length cycle regardless of what it needs.

**Why:** Multi-cycle breaks execution into several *shorter* clock
cycles (each sized for one simple sub-step, not the whole instruction),
and a finite-state-machine controller decides, instruction by
instruction, how many of those short cycles to use. `load word` might
take 5 cycles (it needs every stage); `beq` might take only 3 (it skips
write-back and, in many designs, the separate memory-access stage);
`add` might take 4. The *cycle time itself* also shrinks compared to
single-cycle, since each cycle only has to be as long as its one
sub-step, not the entire datapath's worst case.

**Q12. What component sequences the multiple cycles of one instruction?**

> **Answer:** A **finite-state-machine (FSM) controller**.

**Why:** Unlike single-cycle's simple combinational control (one set of
signals per instruction, valid for exactly one cycle), multi-cycle
control must remember *where it is* within an instruction's execution
and change the control signals every cycle. An FSM does this: each state
corresponds to one cycle of work (fetch, decode, execute, memory,
write-back, etc.), asserts the control signals appropriate for that
state, and transitions to the next state based on the instruction's
opcode and the current state — looping back to the fetch state once an
instruction finishes, ready for the next one.

**Trade-off to remember:** multi-cycle reduces wasted time per
instruction (Week 6's limitation) but still executes only **one**
instruction at a time, start to finish, before starting the next. That
remaining limitation is exactly what Week 9's pipelining addresses.

---

## Quick Self-Test

Before the exam, try covering the answers above and re-deriving each one
from scratch, especially Q2 (Amdahl's Law arithmetic), Q4 (two's
complement conversion), and Q9-Q10 (the single-cycle datapath trace).
Those three are the most common sources of lost points.
