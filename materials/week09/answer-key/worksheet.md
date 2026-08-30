# Professor Answer Key — do not hand out this section

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
  reveal), short professor-led discussion, Part B ~15 min (reveal +
  compute + explain)
- Do not let Part A run long — the value is in reasoning about overlap,
  not in getting the numbers perfectly right on the first try
- If a pair finishes Part B early, point them to the handout's "Optional
  Reading" section, and to Practice Problem 6 for extra computation
  practice
