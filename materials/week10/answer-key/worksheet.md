# Professor Answer Key — do not hand out this section

## Part A — what to listen for

- **A1:** Pair 1: cycle 4. Pair 2: cycle 4. Pair 3: no value needed
  (already given in the worksheet, but confirm students find it
  themselves before checking)
- **A2:** Pair 1: data hazard. Pair 2: data hazard, specifically a
  load-use hazard. Pair 3: no hazard — `store` in this example does not
  read `mul`'s result
- **A3:** Yes, plain forwarding fixes Pair 1. The value is ready one
  cycle before it is needed (EX at cycle 3, needed at cycle 4), so a
  direct wire delivers it in time with zero stall
- **A4:** No. The loaded value and the need for it land in the exact
  same cycle (cycle 4), so there is nothing yet to forward at the moment
  instruction 2 reaches EX. One stall cycle is required first
- **A5:** Instruction 1's EX output (cycle 3) forwards to instruction
  2's EX input (cycle 4). Accept any answer naming the same two points,
  worded differently

## Part B — model answers

- **B2:** Two instructions (Guessed instruction A and B)
- **B3 (model answer):** "Both guessed instructions must be flushed
  (thrown away) before they reach WB. The pipeline knows to do this at
  the end of the branch's EX stage, cycle 3, when the real outcome
  becomes known."
- **B4:** The pipeline restarts fetching from the correct, not-taken
  path, the cycle right after the misprediction is detected
- **B5 (model answer):** "It is not a hardware mistake — predicting is a
  deliberate strategy that trades some wrong guesses for a lot of saved
  time on correct guesses. Flushing is the planned, working fix for
  those wrong guesses, not a bug."
- **B6 (model answer):** "A deeper pipeline fetches more instructions
  before a branch's outcome is known, so a wrong guess means flushing
  more work and losing more cycles. The best-case speed goes up with
  more stages, but so does the worst-case misprediction cost."

## Facilitation notes

- Total time: Part A ~15 min (trace and predict, no reveal), short
  professor-led discussion, Part B ~15 min (reveal + branch trace)
- Do not let Part A run long — the goal is spotting the hazard pattern,
  not perfect wording
- If a pair finishes Part B early, point them to the handout's "Optional
  Reading" section on dynamic branch prediction and instruction
  scheduling
