# Professor Answer Key — do not hand out this section

## Part A — what to listen for

- **A1:** Serial = saving the final combined file (must happen last, one
  step at a time). Parallel = filtering each of the 200 photos
  (independent, splittable across cores)
- **A2:** Speedup(4) = 1 / (0.10 + 0.90/4) = 1 / (0.10 + 0.225) =
  1 / 0.325 ≈ **3.08x**. Accept small rounding differences
- **A3/A4:** Accept any prediction if the reasoning is coherent. Many
  pairs will guess "roughly double" by intuition (2x workers -> 2x
  speedup); a few may already suspect diminishing returns from class.
  Do **not** confirm or deny yet — that is the point of the prediction
- **A5:** Good answers mention: communication between workers, waiting
  for the slowest worker, combining results, keeping shared data
  consistent (cache coherence, Weeks 11-12). Any answer naming a real
  coordination cost is a success

## Part B — model answers

- **B1:** Should match ≈3.08x from A2, within rounding
- **B2:** No — speedup only went from ~3.1x to ~4.7x, about 1.5x more,
  not 2x more, even though the worker count doubled
- **B3 (model answer):** "The 10% serial part takes the same fixed time
  no matter how many workers help with the other 90%. As workers grow,
  that fixed serial time becomes a bigger and bigger share of the total,
  so each doubling of workers buys a smaller and smaller speedup gain."
- **B4 (model answer):** "More cores help less and less once the task's
  serial part starts to dominate — check the serial fraction before
  assuming more cores means proportionally faster."
- **B5 (model answer):** "The formula assumes perfectly free splitting
  and combining. Real machines pay a coordination cost: workers must
  communicate, wait for the slowest one, and merge partial results,
  which eats into the theoretical speedup, especially as worker count
  grows."

## Facilitation notes

- Total time: Part A ~15 min (prediction + first computation, no full
  reveal), short professor-led discussion, Part B ~15 min (reveal +
  explain)
- Encourage pairs to actually do the A2 arithmetic; walking around to
  check for the 0.325 denominator catches most calculation slips early
- If a pair finishes Part B early, point them to the handout's "Optional
  Reading" section
