# Answer Key

1. **B** — every instruction had to wait for one fixed tick sized for the slowest instruction, even fast ones
2. **B** — one tick now equals one short step, not a whole instruction
3. **C** — `lw` needs all five steps: it fetches, decodes, computes an address, reads memory, and writes the result back
4. **B** — spreading one instruction's work across several ticks means some values must be held steady from one tick to the next
5. **B** — Wilkes proposed microprogramming so control steps could be stored as data and changed easily, instead of rewiring a fixed circuit
6. **C** — 3 steps × 100 ns = 300 ns
7. **False** — multi-cycle still finishes one instruction completely, step by step, before starting the next one; overlapping instructions is Week 9's topic
8. **Model answer:** "Each tick is now much shorter than a single-cycle tick, so even an instruction that needs several short ticks can finish faster overall than waiting for one long, fixed tick. The control unit only turns on the steps each instruction actually needs."
