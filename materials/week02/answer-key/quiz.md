# Answer Key

1. **B** — CPU time is the actual time a processor spends running one program, computed from instruction count, CPI, and clock cycle time
2. **C** — CPU time = 400,000,000 × 2 × (1 / 2,000,000,000) = 0.4 seconds
3. **B** — same clock rate guarantees nothing on its own; CPI and instruction count can still differ and change the result
4. **B** — Amdahl's Law caps the overall speedup you can get when only part of a task is sped up
5. **C** — maximum speedup = 1 / (1 − 0.5) = 2x, even with an infinitely fast improvement
6. **B** — MIPS counts instructions per second, not how many instructions the actual task needs, so it can mislead when comparing different designs
7. **A** — price ratio (E/F) = 800/500 = 1.6, speed ratio (E/F) = 2, performance-per-dollar ratio = 2/1.6 = 1.25, so Laptop E gives about 1.25x more performance per dollar, even though it costs more upfront
8. **Model answer:** "The part you did not speed up still takes its full original time, and becomes the bottleneck. Amdahl's Law shows the fraction improvable, F, limits how much the overall task can speed up, no matter how fast that part gets."
