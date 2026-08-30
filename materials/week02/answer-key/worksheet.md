# Professor Answer Key — do not hand out this section

## Part A — model answers

- **A1:** Clock cycle time = 1 / 2.5 GHz = **0.4 nanoseconds**, same for
  both machines
- **A2:** CPU time (P) = 800,000,000 × 4 × 0.4 ns = 1,280,000,000 ns =
  **1.28 seconds**
- **A3:** CPU time (Q) = 800,000,000 × 2 × 0.4 ns = 640,000,000 ns =
  **0.64 seconds**
- **A4:** Speedup = 1.28 / 0.64 = **2x** — Machine Q is twice as fast
- **A5:** Price ratio (Q/P) = 650 / 500 = 1.3. Performance-per-dollar
  ratio = speed ratio / price ratio = 2 / 1.3 ≈ **1.54**. Machine Q gives
  about 1.54x more performance per dollar, so yes, it is worth the
  higher price here

## Part B — model answers

- **B1:** Self-check, no wrong answer, just correction
- **B2:** F = 0.7, S = 3. Speedup = 1 / ((1 − 0.7) + 0.7/3) = 1 / (0.3 +
  0.233) = 1 / 0.533 ≈ **1.88x**
- **B3:** Maximum speedup = 1 / (1 − 0.7) = 1 / 0.3 ≈ **3.33x**, the cap
  even with an infinitely fast update
- **B4 (model computation):**
  - CPU time (Value) = 2,000,000,000 × 3 × (1/3,000,000,000) = **2.0
    seconds**
  - CPU time (Studio) = 2,000,000,000 × 1 × (1/3,000,000,000) ≈ **0.67
    seconds**
  - Speedup = 2.0 / 0.67 ≈ **3x**
  - Price ratio (Studio/Value) = 950 / 600 ≈ 1.58. Performance-per-dollar
    ratio = 3 / 1.58 ≈ **1.9x** — Studio gives more performance per
    dollar despite the higher price
- **B5:** F = 0.8, S = 4. Speedup = 1 / ((1 − 0.8) + 0.8/4) = 1 / (0.2 +
  0.2) = 1 / 0.4 = **2.5x**. Maximum possible = 1 / (1 − 0.8) = **5x**,
  never more, no matter how fast the encoder gets

## Facilitation notes

- Total time: Part A ~15 min (compute, no reveal yet), short
  professor-led walkthrough, Part B ~15 min (verify + new problems +
  SmartPick attempt)
- Encourage pairs to write every intermediate number (cycle time,
  instruction count, CPI) — the goal is fluency with the formula, not
  just a final number
- For B4, let pairs attempt it fully before showing the deck's own
  worked-example slide; comparing their numbers to the slide is the
  payoff moment
- If a pair finishes early, point them to B5 or the handout's practice
  problems
