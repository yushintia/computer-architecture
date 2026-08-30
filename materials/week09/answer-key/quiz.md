# Answer Key

1. **B** — pipelining splits an instruction's work into stages, and overlaps those stages across several instructions
2. **B** — Execute (EX) comes right after Decode (ID): Fetch, Decode, Execute, Memory, Write Back
3. **B** — throughput is how many instructions finish per unit of time; latency is one instruction's own time
4. **B** — 5 + (20 − 1) = 24 ticks
5. **B** — fill time is the first few ticks, while the pipeline is still filling up with instructions
6. **IF, ID, EX, MEM, WB** (Fetch, Decode, Execute, Memory, Write Back)
7. **False** — one instruction still passes through all five stages, so its own latency stays the same; only throughput improves
8. **Model answer:** "Every program pays a one-time fill time at the start and a drain time at the end, and those extra ticks never disappear. On top of that, real programs sometimes need a stall, which pauses a stage for a tick or more, so the real speedup lands a little under the ideal stage count."
