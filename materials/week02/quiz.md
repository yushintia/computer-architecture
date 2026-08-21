# Week 2 Self-Check Quiz (Ungraded)

Computer Architecture (503872-004). This quiz is **ungraded** — it is
only to help you check what stuck. About 10 minutes. Do not look back at
the slides while you answer.

---

**1.** What is CPU time?

A. The price of a processor
B. The actual time a processor spends running one program
C. The number of cores a processor has
D. The clock rate printed on a spec sheet

**2.** A program runs 400 million instructions, average CPI 2, clock
rate 2.0 GHz. What is its CPU time?

A. 0.1 seconds
B. 0.2 seconds
C. 0.4 seconds
D. 2.0 seconds

**3.** Two machines have the exact same clock rate. What does this tell
you about their CPU time on the same task?

A. They will always finish in exactly the same time
B. Nothing on its own — CPI and instruction count also matter
C. The one with more cores always wins
D. Clock rate is the only thing that decides CPU time

**4.** What does Amdahl's Law describe?

A. How much faster a processor gets as its clock rate rises
B. The limit on overall speedup when only part of a task gets faster
C. The exact price of a fast processor
D. How many instructions a program needs

**5.** A task's improvable part is 50% of total time. That part becomes
infinitely fast. What is the maximum overall speedup?

A. Infinite
B. 4x
C. 2x
D. 1x, no change

**6.** Why could an old "MIPS" number mislead a buyer?

A. It only measured price, not speed
B. It counted instructions per second, not how many instructions a task actually needed
C. It only worked for laptops, not desktops
D. It measured clock rate instead of CPI

**7.** Laptop E costs $800 and is twice as fast as Laptop F, which costs
$500. Which has better performance per dollar?

A. Laptop E
B. Laptop F
C. They are exactly equal
D. Cannot be determined

**8. (Short answer)** In 1-2 sentences, explain why speeding up one part
of a task by 10x does not always make the whole task 10x faster. Use at
least one key word from this week (Amdahl's Law, bottleneck, fraction
improvable).

`_____________________________________________________________`
`_____________________________________________________________`

---
---

# Answer Key

1. **B** — CPU time is the actual time a processor spends running one program, computed from instruction count, CPI, and clock cycle time
2. **C** — CPU time = 400,000,000 × 2 × (1 / 2,000,000,000) = 0.4 seconds
3. **B** — same clock rate guarantees nothing on its own; CPI and instruction count can still differ and change the result
4. **B** — Amdahl's Law caps the overall speedup you can get when only part of a task is sped up
5. **C** — maximum speedup = 1 / (1 − 0.5) = 2x, even with an infinitely fast improvement
6. **B** — MIPS counts instructions per second, not how many instructions the actual task needs, so it can mislead when comparing different designs
7. **A** — price ratio (E/F) = 800/500 = 1.6, speed ratio (E/F) = 2, performance-per-dollar ratio = 2/1.6 = 1.25, so Laptop E gives about 1.25x more performance per dollar, even though it costs more upfront
8. **Model answer:** "The part you did not speed up still takes its full original time, and becomes the bottleneck. Amdahl's Law shows the fraction improvable, F, limits how much the overall task can speed up, no matter how fast that part gets."
