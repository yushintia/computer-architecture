# Week 7 Worksheet: Timing the Multi-Cycle Fix

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the instructor can follow your thinking.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

Here are the five possible steps a multi-cycle instruction can use, in
order: **Fetch, Decode, Execute, Memory, Write Back**. Not every
instruction uses every step. **Do not look ahead to Part B yet.**

**A1.** `add` (an R-type instruction) reads two registers, adds them,
and saves the result into a register — it never touches memory. Which
steps does `add` use? Which one does it skip?

`________________________________________________________________`

**A2.** `lw` (load word) reads a register to compute an address, reads a
value from memory at that address, and saves that value into a
register. Which steps does `lw` use? Does it skip any?

`________________________________________________________________`

**A3.** `sw` (store word) reads two registers, computes an address, and
writes a value into memory — it never saves anything back into a
register. Which steps does `sw` use? Which one does it skip?

`________________________________________________________________`

**A4.** `beq` (branch) reads two registers and compares them, then
decides where to go next — it never touches memory or writes to a
register. Which steps does `beq` use? How many does it skip?

`________________________________________________________________`

**A5.** Prediction: rank all four instructions from **fewest** total
steps to **most** total steps.

`________________________________________________________________`

*Stop here. We compare predictions together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your instructor will hand this out after the class discussion of Part A.
It starts with the real step counts, then asks you to explain them.

**The real step counts:** `add` = 4 steps, `sw` = 4 steps, `beq` = 3
steps, `lw` = 5 steps.

**B1.** Was your Part A ranking (A5) correct?

`Yes  /  No  /  Partly`

**B2.** Assume each short step takes 100 ns. Using the step counts
above, compute the total time for **one** `add` and **one** `lw`.

`________________________________________________________________`

**B3.** A program runs 200 `add` instructions and 50 `lw` instructions.
Using 100 ns per step, compute the **total** multi-cycle time for this
program. Show your work.

`________________________________________________________________`
`________________________________________________________________`

**B4.** If the old single-cycle chip used one fixed 500 ns tick for
every instruction, was that same 250-instruction program faster or
slower on single-cycle than on multi-cycle? By how much?

`________________________________________________________________`

**B5.** A friend says: "multi-cycle instructions take more clock ticks,
so multi-cycle must be slower overall." Write one sentence explaining
why this is wrong.

`________________________________________________________________`

**B6 (stretch, optional).** Multi-cycle now finishes `add` faster than
`lw`. Does that mean two instructions can now run on the chip at the
same time? Why or why not?

`________________________________________________________________`

---
---

# Instructor Answer Key — do not hand out this section

## Part A — what to listen for

- **A1:** Fetch, Decode, Execute, Write Back. Skips **Memory** (never reads or writes data memory)
- **A2:** Fetch, Decode, Execute, Memory, Write Back. Uses **all five** steps, skips none
- **A3:** Fetch, Decode, Execute, Memory. Skips **Write Back** (never saves a result into a register)
- **A4:** Fetch, Decode, Execute. Skips **two** steps: Memory and Write Back
- **A5:** Accept any ranking with coherent reasoning at this stage; do **not** confirm the real answer yet. Most pairs will correctly guess `beq` uses the fewest steps and `lw` the most, since Parts A1-A4 walk them there directly

## Part B — model answers

- **B1:** Depends on their Part A guess; no wrong answer here, just self-checking
- **B2:** `add` = 4 × 100 ns = 400 ns. `lw` = 5 × 100 ns = 500 ns
- **B3:** 200 × 400 ns + 50 × 500 ns = 80,000 ns + 25,000 ns = **105,000 ns**
- **B4:** Single-cycle: 250 × 500 ns = 125,000 ns. Multi-cycle: 105,000 ns (from B3). Multi-cycle is faster, by **20,000 ns** (about 16% less time)
- **B5 (model answer):** "Multi-cycle uses more ticks per instruction sometimes, but each tick is much shorter, so the total real time is usually still less, not more."
- **B6 (model answer):** "No. Multi-cycle only changes how long one instruction takes; the chip still fully finishes one instruction, step by step, before it starts the next one. Running two instructions at once is a different idea, called overlap, which Week 9 (Pipelining) introduces, after the Week 8 midterm review."

## Facilitation notes

- Total time: Part A ~15 min (step-tracing and prediction only, no reveal), short instructor-led discussion, Part B ~15 min (reveal + compute + explain)
- Do not let Part A run long — the value is in reasoning about which steps each instruction needs, not in getting the ranking perfectly right
- If a pair finishes Part B early, point them to the handout's "Optional Reading" section, and to Practice Problem 5 for extra computation practice
