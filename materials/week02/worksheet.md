# Week 2 Worksheet: Measuring SmartPick, With Numbers

Computer Architecture (503872-004). Work with your pair. Show your
steps — write the numbers you multiply or divide, not just a final
answer.

**Pair names:** ___________________________ / ___________________________

**Formula reminder:** CPU time = Instruction Count × CPI × Clock Cycle
Time, where Clock Cycle Time = 1 / Clock Rate.

**Amdahl's Law reminder:** Overall speedup = 1 / ((1 − F) + F / S),
where F is the fraction of time you can speed up, and S is how much
faster that fraction becomes.

---

## Part A (do this in 차시 2, about 15 minutes)

Two fictional machines run the exact same task. Compute CPU time for
each, then compare them.

| Spec line | Machine P | Machine Q |
|---|---|---|
| Clock rate | 2.5 GHz | 2.5 GHz |
| Instruction count | 800 million | 800 million |
| CPI | 4 | 2 |
| Price | $500 | $650 |

**A1.** What is the clock cycle time for both machines? (They share a
clock rate.)

`________________________________________________________________`

**A2.** Compute CPU time for Machine P. Show your steps.

`________________________________________________________________`
`________________________________________________________________`

**A3.** Compute CPU time for Machine Q. Show your steps.

`________________________________________________________________`
`________________________________________________________________`

**A4.** What is the speedup of Machine Q over Machine P?

`________________________________________________________________`

**A5.** Compute the price ratio (Q / P) and the performance-per-dollar
ratio. Is Machine Q worth its higher price?

`________________________________________________________________`
`________________________________________________________________`

*Stop here. We compare answers together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your instructor will walk through Part A's answers with the class
first. Then continue below.

**B1.** Did your Part A answers match the class discussion? Fix any
mistakes here before continuing.

`Yes  /  No, fixed above`

**B2.** A software update on Machine P speeds up a part of a task —
70% of the total run time — by 3x. The remaining 30% cannot get faster.
Using Amdahl's Law, what is the overall speedup?

`________________________________________________________________`
`________________________________________________________________`

**B3.** What is the maximum possible speedup for the same task, even if
that 70% became infinitely fast?

`________________________________________________________________`

**B4.** Now try SmartPick's real numbers yourself, before the class
sees the reveal. Both laptops run the same video-export task.

| Spec line | Value | Studio |
|---|---|---|
| Clock rate | 3.0 GHz | 3.0 GHz |
| Instruction count | 2 billion | 2 billion |
| CPI | 3 | 1 |
| Price | $600 | $950 |

Compute: CPU time for Value, CPU time for Studio, the speedup, and the
performance-per-dollar ratio.

`________________________________________________________________`
`________________________________________________________________`
`________________________________________________________________`
`________________________________________________________________`

**B5 (stretch, optional).** Value's team speeds up encoding — 80% of the
export's run time — by 4x with a better codec. Using Amdahl's Law, what
is the overall speedup? What is the maximum possible, even with an
infinitely fast encoder?

`________________________________________________________________`
`________________________________________________________________`

---
---

# Instructor Answer Key — do not hand out this section

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
  instructor-led walkthrough, Part B ~15 min (verify + new problems +
  SmartPick attempt)
- Encourage pairs to write every intermediate number (cycle time,
  instruction count, CPI) — the goal is fluency with the formula, not
  just a final number
- For B4, let pairs attempt it fully before showing the deck's own
  worked-example slide; comparing their numbers to the slide is the
  payoff moment
- If a pair finishes early, point them to B5 or the handout's practice
  problems
