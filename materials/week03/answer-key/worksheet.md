# Professor Answer Key — do not hand out this section

## Part A — what to listen for

- **A1:** `18 = 16 + 2`, so `00010010`
- **A2:** `00010111 = 16 + 4 + 2 + 1 = 23`
- **A3:** `1010` = `A`, `1100` = `C`, so hex `AC`
- **A4/A5:** Accept any prediction if reasoning is coherent. Many pairs will guess "No, a byte only has one meaning" — that is the expected wrong guess, and the whole point of the "not sure yet" moment. Do **not** confirm or deny the answer yet
- **A5:** Good answers mention: not knowing which reading rule to use, confusion about negative numbers, or uncertainty about hex. Any honest gap is a success

## Part B — model answers

- **B1:** Depends on their A4 guess; there is no wrong answer here, just self-checking
- **B2 (model answer):** "Two's complement does not use a simple sign bit the way sign-magnitude does. It stores negative numbers by inverting the bits and adding 1, so a negative number's pattern looks like a large positive number unless you know to apply the signed reading rule."
- **B3 (model answer):** "The counter overflows. It cannot hold 256 in 8 bits, so it silently wraps around back to 0, showing the wrong count instead of an error."
- **B4:** `'O'` = `01001111`, `'K'` = `01001011`
- **B5 (model answer):** "The refund amount cannot be shown as a normal negative number. It would either wrap around to a huge, wrong positive number (overflow) or the software would need extra, error-prone workarounds to show a return as negative at all."

## Facilitation notes

- Total time: Part A ~15 min (prediction only, no reveal), short professor-led discussion, Part B ~15 min (reveal + explain)
- Do not let Part A run long — the value is in predicting under uncertainty, not in getting the "right" answer
- If a pair finishes Part B early, point them to the handout's "Optional Reading" section
