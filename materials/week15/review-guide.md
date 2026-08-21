# Week 15 Review Guide: Final Exam (Weeks 1-14)

Computer Architecture (503872-004) — for students to study from before
the final. Same 15 questions as the "Check Yourself" section of the
Week 15 slides, with fuller worked explanations than fit on a slide.
Organized by theme and week, weighted toward Weeks 9-14 since Weeks 1-7
were already covered in depth in the [Week 8 review guide](../week08/review-guide.md).

Final exam facts, from Week 1's Course Logistics grading table: the
final is worth **30%** of your grade, the same weight as the midterm,
and it is **cumulative** — it covers Weeks 1-14, not just the material
since the midterm.

---

## Theme 1: Measuring and Describing a Machine (Weeks 1-5)

### Week 2: Performance & Cost

**Q1. Value's video export runs 2 billion instructions at CPI 3, at 3.0 GHz. Find the CPU time.**

> **Answer:** **2.0 seconds.**

**Worked steps:**

```
CPU time = (Instruction Count x CPI) / Clock Rate
         = (2,000,000,000 x 3) / 3,000,000,000
         = 6,000,000,000 / 3,000,000,000
         = 2.0 s
```

These are the exact numbers from Week 2's SmartPick case study: Value
runs 2 billion instructions at CPI 3, Studio runs the same 2 billion
instructions at CPI 1, giving Studio a CPU time of 0.67 s — three times
faster, thanks to Studio's bigger cache lowering its CPI. If a question
gives you instructions, CPI, and clock rate, this formula is always the
starting point.

### Week 3: Data Representation

**Q2. Write -9 as an 8-bit two's complement binary number.**

> **Answer:** `11110111`

**Worked steps:**
1. Write 9 in 8-bit binary: `00001001`
2. Flip every bit (one's complement): `11110110`
3. Add 1: `11110110 + 1 = 11110111`

**Check it:** `11110111` = `-(2^7) + 2^6+2^5+2^4+2^3+2^2+2^1+2^0` minus
the flipped 2^3 bit... more simply: `-128 + 64+32+16+4+2+1 = -128+119 =
-9`. Correct.

Two's complement is used instead of a plain sign bit because it lets one
adder circuit handle both addition and subtraction, for positive and
negative numbers alike, and it has only one representation of zero.

### Weeks 4-5: ISA I and II

**Q3. Which instruction format computes using only registers, and which one adds an offset to reach memory?**

> **Answer:** **R-type** computes using only registers (e.g. `add`,
> `sub`). **I-type** adds a register's value to a small built-in offset
> to compute a memory address, used by `lw` (load) and `sw` (store).

**Why:** The instruction set this course teaches has three formats:
R-type (register-to-register compute), I-type (register plus a small
constant — loads, stores, and branches like `beq`/`bne` all use this
shape), and J-type (an unconditional jump to a new address, `j`/`jal`).
Knowing the format tells you, at a glance, what kind of operand an
instruction can use. A conditional branch (`beq`, `bne`) is what lets a
program repeat itself into a loop; the return address for a procedure
call lives on the stack (or a link register for one call level deep).

---

## Theme 2: Building and Speeding Up a Datapath (Weeks 6-10)

### Week 6: Single-Cycle

**Q4. A single-cycle CPU gives every instruction one full clock cycle. What's the main downside of fixing the cycle length this way?**

> **Answer:** The clock period must be long enough for the **slowest**
> instruction (`lw`, which touches the register file, ALU, and memory in
> sequence). Every other instruction, even a fast one like `add`, still
> has to wait out that same full cycle length, doing nothing useful for
> the rest of it.

An instruction passes through five stages in this datapath: instruction
fetch, decode/register read, execute (ALU), memory access, write-back —
though not every instruction uses every stage's result (e.g. `add`
doesn't need the memory-access stage's result, but still pays for its
time).

### Week 7: Multi-Cycle

**Q5. Give one reason a multi-cycle `beq` finishes in fewer cycles than a multi-cycle `lw`.**

> **Answer:** Multi-cycle only spends as many (shorter) cycles as an
> instruction actually needs. `beq` does not need a memory-access step,
> so it skips that cycle. `lw` needs every step — fetch, register read,
> address compute, memory access, write-back — so it uses more cycles.

A finite-state-machine (FSM) controller sequences these cycles: each
state asserts the control signals for one cycle of work, then moves to
the next state based on the instruction's opcode, looping back to fetch
once an instruction finishes. Multi-cycle fixes single-cycle's wasted
time, but still executes only one instruction at a time, start to
finish — the limitation pipelining fixes next.

### Week 9: Pipelining I

**Q6. Name the three types of pipeline hazards, one line each.**

> **Answer:**
> - **Structural:** two instructions need the same piece of hardware in
>   the same cycle (e.g. one memory port). Modern chips avoid most of
>   these with extra hardware copies.
> - **Data:** an instruction needs a value a previous, still-in-flight
>   instruction has not produced yet.
> - **Control:** the pipeline fetches instructions before it knows which
>   way a branch will go.

Data and control hazards are the two that show up constantly and get
the most attention; structural hazards are the textbook's third family,
worth knowing but far less common in practice on modern chips.

### Week 10: Pipelining II

**Q7. Forwarding fixes most data hazards right away. Why can't it fully fix a load-use hazard?**

> **Answer:** A value loaded from memory is not ready until the pipeline's
> MEM stage finishes — one stage later than an ALU result, which is
> ready at EX. The very next instruction needs that value one cycle
> before it exists, so forwarding cannot deliver something that hasn't
> been produced yet. At least one stall cycle ("bubble") is still needed.

```
Cycle:                1    2    3    4          5
Instr 1: load value   IF   ID   EX   MEM(ready)  WB
Instr 2: use value         IF   ID   EX(needs it) MEM
```

The hazard detection unit spots exactly this pattern and freezes
instruction 2 for one cycle; after the pause, forwarding delivers the
value normally.

**Q8. A branch is mispredicted 20% of the time, with a 4-cycle penalty. What is the expected extra cycles per branch?**

> **Answer:** `0.20 x 4 = 0.8 extra cycles per branch`, on average.

Branch prediction guesses which way a branch goes before the outcome is
known, so the pipeline can keep fetching instead of stalling. When the
guess is wrong, the wrongly fetched instructions are **flushed**
(thrown away) and the pipeline restarts from the correct target — that
restart is the misprediction penalty. Multiplying the miss rate by the
penalty gives the *expected* extra cost per branch, the same style of
calculation as a cache miss's contribution to AMAT (Week 11) or a
serial fraction's cap on speedup (Weeks 2 and 13).

---

## Theme 3: Memory and Parallel Scale (Weeks 11-14)

### Week 11: Memory Hierarchy I (Cache)

**Q9. A program touches a new array for the very first time, and it isn't in the cache yet. Which type of miss is this?**

> **Answer:** A **compulsory miss** — the data was never in the cache
> before, so no cache design or size could have prevented this one.

The other two miss types: a **capacity miss** happens when the cache is
too small to hold everything the program is currently using, and a
**conflict miss** happens when the data could fit, but the cache's rules
sent it to a slot another piece of data already occupies.

**Q10. Hit time is 1 ns, miss rate is 8%, miss penalty is 90 ns. Compute AMAT.**

> **Answer:** **8.2 ns.**

```
AMAT = hit time + (miss rate x miss penalty)
     = 1 + (0.08 x 90)
     = 1 + 7.2
     = 8.2 ns
```

AMAT (Average Memory Access Time) turns "usually fast, sometimes slow"
into one number you can compare across designs. A bigger cache
generally raises the hit rate (lowers the miss rate), which lowers
AMAT — this is exactly why Studio's larger cache made it faster than
Value on the same task, back in Week 1's opening mystery.

### Week 12: Memory Hierarchy II (Virtual Memory)

**Q11. What does a TLB store, and why does that make address translation fast?**

> **Answer:** A **TLB (Translation Lookaside Buffer)** stores recently
> used virtual-to-physical page translations. Checking the full page
> table on every single memory access would be too slow, so the TLB acts
> as a small, fast cache of recent translations — most of the time the
> answer is already there, so translation is nearly free. It's last
> week's caching idea, reused for addresses instead of data.

**Q12. What happens, step by step, on a page fault?**

> **Answer:** A page fault happens when the page table says the needed
> page sits only on disk, not in RAM.
> 1. The processor pauses.
> 2. The operating system finds a free physical frame.
> 3. The OS loads the page from disk into that frame.
> 4. The OS updates the page table with the new mapping.
> 5. The program continues, re-running the instruction that faulted.

A page fault costs far more than a cache miss: RAM answers in
nanoseconds, but a disk trip can take milliseconds — thousands of times
slower. This is also how two programs can both use the same virtual
address (like 4,200) without colliding: each program has its own
private page table mapping that address to a different physical frame,
which is also why one crashing program usually doesn't crash the whole
machine.

### Week 13: Parallelism

**Q13. A program is 80% parallelizable. What is the max speedup on 4 cores, by Amdahl's Law?**

> **Answer:** **2.5x.**

```
Speedup = 1 / (S + P/N)
        = 1 / (0.2 + 0.8/4)
        = 1 / (0.2 + 0.2)
        = 1 / 0.4
        = 2.5
```

This is the *same arithmetic* as Week 2's Amdahl's Law example (speeding
up 80% of a task by 4x also gave 2.5x) — here the "speedup of the
improved part" is supplied by cores instead of a faster component. The
serial fraction (S = 0.2, the part that cannot be split across cores)
never shrinks no matter how many cores you add, which is exactly why
doubling cores from 8 to 16 barely moved SmartPick Studio Pro's export
time in Week 13's case study: the fixed serial part dominates once N is
large.

**Q14. Two cores each cache the same address, and one writes to it. What problem can occur, and what prevents it?**

> **Answer:** The other core's cached copy becomes **stale** (out of
> date) — it still holds the old value after the write. A **coherence
> protocol** prevents this by invalidating or updating the other cores'
> copies so every core sees the new value. This synchronization is part
> of why sharing data across cores costs time, on top of the raw
> computation.

### Week 14: Presentation (real designs, every layer at once)

**Q15. A laptop chip and a phone chip can share the same ARM ISA. Name two microarchitecture differences that could still make one faster.**

> **Answer (any two):** pipeline depth, cache size, core count, in-order
> vs. out-of-order execution, clock speed vs. power budget.

This is Week 1's opening mystery, generalized: sharing an ISA only
guarantees the *same software* runs on both chips, it says nothing
about *how fast*. A laptop chip usually has a much larger power and
cooling budget than a phone chip, so it can afford a deeper pipeline,
more aggressive out-of-order execution, a bigger cache, and a higher
clock speed — all microarchitecture choices, all invisible to the ISA.
Week 14's presentations applied exactly this kind of layer-by-layer
reasoning to one real, current chip or system.

---

## What to Focus On Next

Weeks 1-7 were already reviewed in depth for the midterm (see the
[Week 8 review guide](../week08/review-guide.md)) — spend less time
re-deriving those. Put your remaining study time on:

- **Pipelining hazards (Weeks 9-10):** the load-use hazard timing
  diagram (Q7) and misprediction-penalty arithmetic (Q8)
- **Memory hierarchy (Weeks 11-12):** AMAT arithmetic (Q10) and tracing
  the page-fault sequence from memory, step by step (Q12)
- **Parallelism (Week 13):** Amdahl's Law with N cores (Q13), and being
  able to explain *why* the serial fraction caps the speedup, not just
  compute the number

Before the exam, cover the answers above and re-derive each one from
scratch, especially Q1 (CPU time), Q8 and Q10 (expected-value style
arithmetic), Q12 (page fault sequence), and Q13 (Amdahl's Law with
cores). Those are the most common sources of lost points on a
cumulative final.
