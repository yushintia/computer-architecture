# Professor Answer Key — do not hand out this section

## Part A — what to listen for

There is no single "correct" wording expected in Part A — the point is
to surface the loop's logic in plain words before seeing real
mnemonics. Common good answers:

- **A1:** get the first price (or: point to the start of the list)
- **A2:** does this price equal $525? (accept "is this the target
  price" or similar)
- **A3:** move to the next price and ask again (repeat)
- **A4:** stop; report that it was found
- **A5:** 5 times (once per item on the list); accept "up to 5"

## Part B — model answers

- **B1:** Any honest comparison is fine; look for whether their plan
  had both a repeat step and a stop condition
- **B2 (model answer):** "The branch checks whether the current price
  matches, but only a jump actually sends the program back to check the
  next one. Without the jump, the loop would run once and stop."
- **B3:** Opcode `35`; address register `$t1` (9); receiving register
  `$t3` (11); offset `0`
- **B4:** Opcode `4`; first register `$t3` (11); second register `$t0`
  (8)
- **B5 (model answer):** "A small instruction set can still compute
  anything a large one can; RISC keeps it small on purpose, because
  fewer, simpler instructions are easier to build fast."

## Facilitation notes

- Total time: Part A ~15 min (plan only, no reveal), short
  professor-led discussion, Part B ~15 min (reveal + encode)
- Do not let Part A run long — the value is reasoning about the loop's
  shape, not writing perfect mnemonics yet
- Quiz 1 follows shortly after Part B in the same session — keep the
  discussion tight so there is time
- If a pair finishes Part B early, point them to the handout's
  "Optional Reading" section
