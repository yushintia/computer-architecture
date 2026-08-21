# Week 9 Self-Check Quiz (Ungraded)

Computer Architecture (503872-004). This quiz is **ungraded** — it is
only to help you check what stuck. About 10 minutes. Do not look back at
the slides while you answer.

---

**1.** What does "pipelining" mean?

A. Running instructions in a random order
B. Splitting an instruction's work into stages that overlap across several instructions
C. Making the clock run at a higher frequency
D. Skipping instructions the program does not need

**2.** In the classic five-stage pipeline, which stage comes right after
Decode (ID)?

A. Fetch (IF)
B. Execute (EX)
C. Memory (MEM)
D. Write Back (WB)

**3.** "Throughput" measures:

A. How long one single instruction takes, start to finish
B. How many instructions finish per unit of time, on average
C. The chip's clock speed in GHz
D. How large the chip's cache is

**4.** A five-stage pipeline runs 20 instructions, with no stalls. Using
total ticks = stages + (instructions − 1), how many total ticks does the
program take?

A. 20
B. 24
C. 25
D. 100

**5.** What causes "fill time" in a pipeline?

A. The pipeline emptying out after the last instruction
B. The first few ticks, before the pipeline is full of instructions
C. A wrong branch guess
D. A broken pipeline register

**6.** Put the five pipeline stages in order, using their abbreviations.

`_____________________________________________________________`

**7.** True or false: pipelining makes any single instruction finish
faster than it would running alone.

`_____________________________________________________________`

**8. (Short answer)** In 1-2 sentences, explain why a five-stage
pipeline's real speedup on a program is usually a little less than 5x.
Use at least one key word from this week (fill time, drain time, stall).

`_____________________________________________________________`
`_____________________________________________________________`

---
---

# Answer Key

1. **B** — pipelining splits an instruction's work into stages, and overlaps those stages across several instructions
2. **B** — Execute (EX) comes right after Decode (ID): Fetch, Decode, Execute, Memory, Write Back
3. **B** — throughput is how many instructions finish per unit of time; latency is one instruction's own time
4. **B** — 5 + (20 − 1) = 24 ticks
5. **B** — fill time is the first few ticks, while the pipeline is still filling up with instructions
6. **IF, ID, EX, MEM, WB** (Fetch, Decode, Execute, Memory, Write Back)
7. **False** — one instruction still passes through all five stages, so its own latency stays the same; only throughput improves
8. **Model answer:** "Every program pays a one-time fill time at the start and a drain time at the end, and those extra ticks never disappear. On top of that, real programs sometimes need a stall, which pauses a stage for a tick or more, so the real speedup lands a little under the ideal stage count."
