# Professor Answer Key — do not hand out this section

## Part A — what to listen for

There is no single "correct" prediction expected in Part A — the point
is to surface reasoning, not to get it right yet. Common good answers:

- **A1:** the processor asks for data and finds it already in the cache, so the answer is fast
- **A2:** the processor asks for data and it is not in the cache, so the answer is slow
- **A3/A4:** Accept any prediction if the reasoning is coherent. Many pairs will correctly guess "Studio," reasoning from the bigger cache size seen in Week 1. Some may say "cannot tell" without a hit-rate number yet — that is a reasonable, honest answer at this stage
- **A5:** the processor fetches the data from main memory (RAM), and that fetch is much slower than a cache hit

## Part B — model answers

- **B1:** Value miss rate = 20%, AMAT = 1 + (0.20 × 100) = **21 ns**. Studio miss rate = 5%, AMAT = 1 + (0.05 × 100) = **6 ns**
- **B2:** roughly **3.5 times faster** (21 / 6 ≈ 3.5)
- **B3 (model answer):** "Studio's bigger cache reaches a higher hit rate, so it needs far fewer slow trips to main memory. That lowers its AMAT, and a lower AMAT means less waiting on every single memory request, which adds up across a whole video export."
- **B4:** first-time file read = **compulsory**; data no longer fits = **capacity**
- **B5 (model answer):** "A bigger cache usually helps, but past a point it barely raises the hit rate while still costing more money and chip space — so check the actual hit rate or benchmark, not just the cache size number."

## Facilitation notes

- Total time: Part A ~15 min (prediction only, no reveal), short professor-led discussion, Part B ~15 min (real numbers + explain)
- Do not let Part A run long — the value is in reasoning from Week 1's story, not in getting the "right" number
- If a pair finishes Part B early, point them to the handout's "Optional Reading" section
