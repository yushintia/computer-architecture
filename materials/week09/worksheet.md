# Week 9 Worksheet: Timing the Overlap

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the instructor can follow your thinking.

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

Your instructor will hand this out after the class discussion of Part A.
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

---
---

# Instructor Answer Key — do not hand out this section

## Part A — what to listen for

There is no single "correct" prediction expected for A4/A5 reasoning —
the point is to surface reasoning, not to get it right yet.

- **A1:** 4 × 5 = **20 ticks**
- **A2:** 5 + (4 − 1) = **8 ticks**
- **A3:** 12 ticks saved
- **A4:** Accept any prediction with coherent reasoning; do **not**
  confirm the real answer yet. The advantage grows bigger — good answers
  mention that the fixed "extra" cost (fill/drain) becomes a smaller
  fraction of a longer program
- **A5:** **Same.** The first instruction (and every instruction) still
  passes through all five stages, one tick each — its own latency never
  shrinks. Only the *program's* total time improves

## Part B — model answers

- **B1:** Depends on their Part A guess; no wrong answer here, just self-checking
- **B2:** 20 ÷ 8 = **2.5x**
- **B3:** One at a time: 200 × 5 = 1,000 ticks. Overlapped: 5 + (200 − 1) = 204 ticks. Speedup = 1,000 ÷ 204 ≈ **4.9x**
- **B4:** The 200-instruction program is much closer to 5x, because the
  four extra fill/drain ticks are a tiny fraction of 204, but a large
  fraction of the 4-instruction program's 8 ticks
- **B5 (model answer):** "A five-stage pipeline only gets close to 5x on
  long programs — short programs and the fixed fill/drain time keep the
  real speedup below the ideal number."
- **B6 (model answer):** "Yes. Later this course (Week 10) shows that an
  overlapped instruction can sometimes need a value an earlier
  instruction has not produced yet, which can give a wrong answer, not
  just a smaller speedup. That is next week's problem to solve."

## Facilitation notes

- Total time: Part A ~15 min (tick-counting and prediction only, no
  reveal), short instructor-led discussion, Part B ~15 min (reveal +
  compute + explain)
- Do not let Part A run long — the value is in reasoning about overlap,
  not in getting the numbers perfectly right on the first try
- If a pair finishes Part B early, point them to the handout's "Optional
  Reading" section, and to Practice Problem 6 for extra computation
  practice
