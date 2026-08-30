# Week 7 Worksheet: Timing the Multi-Cycle Fix

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the professor can follow your thinking.

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

Your professor will hand this out after the class discussion of Part A.
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
