# Week 7 Self-Check Quiz (Ungraded)

Computer Architecture (503872-004). This quiz is **ungraded** — it is
only to help you check what stuck. About 10 minutes. Do not look back at
the slides while you answer.

---

**1.** What is the main problem with last week's single-cycle chip that
multi-cycle design fixes?

A. It cannot run all instruction types
B. Every instruction waits for one fixed tick, sized for the slowest instruction
C. It uses too many transistors
D. It cannot read from memory

**2.** In a multi-cycle chip, what does one clock tick now equal?

A. One whole instruction, no matter what
B. One single step of an instruction, such as Fetch or Decode
C. One entire program
D. Ten instructions running together

**3.** Which instruction uses all five possible steps (Fetch, Decode,
Execute, Memory, Write Back)?

A. `add`
B. `beq`
C. `lw` (load word)
D. `sw` (store word)

**4.** Why does a multi-cycle chip need temporary registers, like the
instruction register, that single-cycle did not need?

A. To make the chip use more power
B. Because work is now spread across several ticks, so values must be held steady between them
C. Because multi-cycle chips do not have an ALU
D. To store the whole program at once

**5.** What did Maurice Wilkes propose in 1951, and why?

A. A faster clock, to make chips run hotter
B. Microprogramming: storing control steps as data instead of hardwiring them, to make control logic easier to build and fix
C. The first single-cycle datapath
D. A new instruction set for EDSAC

**6.** If one multi-cycle step takes 100 ns, how long does a 3-step
`beq` instruction take?

A. 100 ns
B. 200 ns
C. 300 ns
D. 500 ns

**7.** True or false: multi-cycle design lets the chip start a new
instruction before the current one finishes.

`_____________________________________________________________`

**8. (Short answer)** In 1-2 sentences, explain why more clock ticks per
instruction does not always mean a chip is slower. Use at least one key
word from this week (step, tick, control unit).

`_____________________________________________________________`
`_____________________________________________________________`

---
---

# Answer Key

1. **B** — every instruction had to wait for one fixed tick sized for the slowest instruction, even fast ones
2. **B** — one tick now equals one short step, not a whole instruction
3. **C** — `lw` needs all five steps: it fetches, decodes, computes an address, reads memory, and writes the result back
4. **B** — spreading one instruction's work across several ticks means some values must be held steady from one tick to the next
5. **B** — Wilkes proposed microprogramming so control steps could be stored as data and changed easily, instead of rewiring a fixed circuit
6. **C** — 3 steps × 100 ns = 300 ns
7. **False** — multi-cycle still finishes one instruction completely, step by step, before starting the next one; overlapping instructions is Week 9's topic
8. **Model answer:** "Each tick is now much shorter than a single-cycle tick, so even an instruction that needs several short ticks can finish faster overall than waiting for one long, fixed tick. The control unit only turns on the steps each instruction actually needs."
