# Professor Answer Key — do not hand out this section

## Part A — what to listen for

- **A1:** Fetch, Decode, Execute, Write Back. Skips **Memory** (never reads or writes data memory)
- **A2:** Fetch, Decode, Execute, Memory, Write Back. Uses **all five** steps, skips none
- **A3:** Fetch, Decode, Execute, Memory. Skips **Write Back** (never saves a result into a register)
- **A4:** Fetch, Decode, Execute. Skips **two** steps: Memory and Write Back
- **A5:** Accept any ranking with coherent reasoning at this stage; do **not** confirm the real answer yet. Most pairs will correctly guess `beq` uses the fewest steps and `lw` the most, since Parts A1-A4 walk them there directly

## Part B — model answers

- **B1:** Depends on their Part A guess; no wrong answer here, just self-checking
- **B2:** `add` = 4 × 100 ns = 400 ns. `lw` = 5 × 100 ns = 500 ns
- **B3:** 200 × 400 ns + 50 × 500 ns = 80,000 ns + 25,000 ns = **105,000 ns**
- **B4:** Single-cycle: 250 × 500 ns = 125,000 ns. Multi-cycle: 105,000 ns (from B3). Multi-cycle is faster, by **20,000 ns** (about 16% less time)
- **B5 (model answer):** "Multi-cycle uses more ticks per instruction sometimes, but each tick is much shorter, so the total real time is usually still less, not more."
- **B6 (model answer):** "No. Multi-cycle only changes how long one instruction takes; the chip still fully finishes one instruction, step by step, before it starts the next one. Running two instructions at once is a different idea, called overlap, which Week 9 (Pipelining) introduces, after the Week 8 midterm review."

## Facilitation notes

- Total time: Part A ~15 min (step-tracing and prediction only, no reveal), short professor-led discussion, Part B ~15 min (reveal + compute + explain)
- Do not let Part A run long — the value is in reasoning about which steps each instruction needs, not in getting the ranking perfectly right
- If a pair finishes Part B early, point them to the handout's "Optional Reading" section, and to Practice Problem 5 for extra computation practice
