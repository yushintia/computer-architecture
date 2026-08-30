# Professor Answer Key — do not hand out this section

## Part A — what to listen for

There is no single "correct" prediction expected in Part A — the point
is to surface reasoning, not to get it right yet. Common good answers:

- **A1 (add's path):** Instruction Memory, Register File, ALU, Register File again
- **A2 (crossed out for add):** Data Memory — add has no reason to touch it
- **A3/A4:** Accept any prediction if the reasoning is coherent. Many pairs will correctly guess "No," reasoning that add only needs values already in registers
- **A5:** The correct answer is "Yes" — load's whole purpose is to bring a value in from Data Memory. Some pairs may still guess "No" by analogy with add; that is a fine, expected mistake to surface now

## Part B — model answers

- **B1:** Depends on their Part A guess; there is no wrong answer here, just self-checking
- **B2:** 200 + 100 + 200 + 100 = **600 ps**
- **B3:** 200 + 100 + 200 + 200 + 100 = **800 ps**
- **B4:** 800 - 600 = **200 ps wasted every cycle**
- **B5 (model answer):** "Every part of the datapath shares one single clock signal, so the chip cannot give one instruction a shorter tick and another a longer one within the same design."
- **B6:** 800 - 500 = **300 ps wasted every cycle**

## Facilitation notes

- Total time: Part A ~15 min (prediction only, no reveal), short professor-led discussion, Part B ~15 min (reveal + compute)
- Do not let Part A run long — the value is in predicting under uncertainty, not in getting the "right" answer
- If a pair finishes Part B early, point them to the handout's "Optional Reading" section, especially "why two adders, not one"
