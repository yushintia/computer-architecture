# Week 9 Worksheet: Timing the Overlap

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the professor can follow your thinking.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

A small program has 4 instructions, in this order: `lw`, `add`, `add`,
`beq`. The pipeline has five stages — Fetch, Decode, Execute, Memory,
Write Back — and every stage takes exactly one tick. **Do not look ahead
to Part B yet.**

**A1.** If these 4 instructions run **one at a time** (no overlap, each
instruction takes exactly 5 ticks, start to finish, before the next one
begins), how many total ticks does the whole program take?

`________________________________________________________________`

**A2.** If these 4 instructions run **overlapped** (a new instruction
starts every tick), predict the total ticks for the whole program.
Hint: total ticks = stages + (instructions − 1).

`________________________________________________________________`

**A3.** What is the difference between your A1 and A2 answers?

`________________________________________________________________`

**A4.** Prediction: as the program grows from 4 instructions to 100
instructions, will the overlapped version's advantage over one-at-a-time
grow bigger, grow smaller, or stay the same? Explain in one sentence.

`________________________________________________________________`

**A5.** In the overlapped version, does the very first instruction
finish faster than it would running alone? Circle one, then explain.

**Faster** &nbsp;&nbsp;&nbsp;&nbsp; **Same** &nbsp;&nbsp;&nbsp;&nbsp; **Slower**

`________________________________________________________________`

*Stop here. We compare predictions together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your professor will hand this out after the class discussion of Part A.
It starts with the real tick counts, then asks you to explain them.

**The real tick counts:** one at a time = 4 × 5 = **20 ticks**.
Overlapped = 5 + (4 − 1) = **8 ticks**.

**B1.** Was your Part A prediction (A2) correct?

`Yes  /  No  /  Partly`

**B2.** Using the tick counts above, compute the speedup for this
4-instruction program (one-at-a-time ticks ÷ overlapped ticks). Round to
one decimal place.

`________________________________________________________________`

**B3.** Now compute the same style of speedup for a bigger program: 200
instructions on the same five-stage pipeline. Show your ticks for both
the one-at-a-time version and the overlapped version, then the speedup.

`________________________________________________________________`
`________________________________________________________________`

**B4.** Compare your speedup from B2 (4 instructions) to B3 (200
instructions). Which one is closer to a "perfect" 5x speedup? Why?

`________________________________________________________________`

**B5.** A friend says: "a five-stage pipeline is always exactly 5 times
faster." Write one sentence explaining why this is not quite true.

`________________________________________________________________`

**B6 (stretch, optional).** Can pipelining ever produce a **wrong**
answer, not just a smaller-than-ideal speedup? Why or why not, based on
what you know so far?

`________________________________________________________________`
