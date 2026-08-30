# Professor Answer Key — do not hand out this section

## Part A — what to listen for

There is no single "correct" prediction expected for A4 — the point is
to surface reasoning, not to get it right yet. Common good answers:

- **A1:**

  | Instr | Opcode | Dest | Src1 | Src2 |
  |---|---|---|---|---|
  | (1) | shared / not sure yet | `$t0` | `$t1` | `$t2` |
  | (2) | shared / not sure yet | `$t3` | `$t4` | `$t5` |
  | (3) | shared / not sure yet | `$t6` | `$t0` | `$t3` |

- **A2:** (1) computes `$t0 = $t1 + $t2`. (2) computes `$t3 = $t4 - $t5`.
- **A3:** `$t0` was just written by instruction (1), and `$t3` was just
  written by instruction (2). Instruction (3) reuses both results as its
  own inputs — this is a good moment to note that registers hold
  whatever was last written into them, not a fixed value.
- **A4:** Accept any answer with coherent reasoning. Many pairs will
  guess "different, because they do different jobs" — that is a
  reasonable, common wrong guess. Do **not** confirm or deny yet; that is
  the point of the "not sure yet" moment.

## Part B — model answers

- **B1:**

  | Instr | Dest # | Src1 # | Src2 # |
  |---|---|---|---|
  | (1) `add $t0, $t1, $t2` | 8 | 9 | 10 |
  | (2) `sub $t3, $t4, $t5` | 11 | 12 | 13 |
  | (3) `add $t6, $t0, $t3` | 14 | 8 | 11 |

- **B2 (model answer):** "My prediction was [same/different] — the
  actual answer is that `add` and `sub` share the same opcode. A
  separate, hidden field (not covered until Week 6) is what actually
  tells them apart, not the opcode."
- **B3:** Opcode: shared R-type opcode. Dest: `$t1` (9). Src1: `$t6`
  (14). Src2: `$t2` (10). Full instruction: `sub $t1, $t6, $t2`.
- **B4:** Dest register 9 is `$t1`, src1 register 11 is `$t3`, src2
  register 14 is `$t6`. Since fields alone don't say add vs. sub, either
  reading is a fair answer as long as the fields are labeled correctly;
  point out that this is exactly the ambiguity Week 6 resolves. If
  written as `add`, meaning is `$t1 = $t3 + $t6`; if `sub`, meaning is
  `$t1 = $t3 - $t6`.
- **B5 (model answer):** "No. `add` and `sub` only work on values
  already sitting in registers. Checking a threshold stored in memory
  needs an instruction that can reach into memory, and comparing against
  it needs an instruction that can make a decision — neither exists yet
  in this week's instruction set. That gap is exactly what Week 5
  covers."

## Facilitation notes

- Total time: Part A ~15 min (fields + prediction, no opcode-bits
  reveal), short professor-led discussion, Part B ~15 min (register
  numbers revealed + encode/decode practice).
- Do not reveal the register-number table during Part A — the value is
  in labeling fields correctly under uncertainty about the opcode, not
  in getting exact numbers early.
- If a pair finishes Part B early, point them to the handout's "Optional
  Reading" section, or have them try writing their own three-instruction
  chain like SmartPick's checkout example.
