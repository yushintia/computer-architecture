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

Your professor will walk through Part A's answers with the class
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
