# Week 4 Worksheet: Encoding SmartPick's Checkout Register

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the instructor can follow your thinking.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

SmartPick's checkout program uses a handful of registers to total up a
customer's cart. Three instructions from that program are shown below.
**Do not look ahead to Part B yet — the register-number table is not
revealed until then.**

- **(1)** `add $t0, $t1, $t2`
- **(2)** `sub $t3, $t4, $t5`
- **(3)** `add $t6, $t0, $t3`

**A1.** For each instruction above, identify its four fields: opcode,
dest, src1, src2. It is OK to write "shared, not sure yet" for the
opcode value — we have not revealed the exact bits yet.

| Instr | Opcode | Dest | Src1 | Src2 |
|---|---|---|---|---|
| (1) | | | | |
| (2) | | | | |
| (3) | | | | |

**A2.** In plain words, what does instruction (1) compute? What does
instruction (2) compute?

`________________________________________________________________`
`________________________________________________________________`

**A3.** Instruction (3) uses `$t0` and `$t3` as its sources. Where did
the values in `$t0` and `$t3` most likely come from? (Hint: look at
instructions (1) and (2) again.)

`________________________________________________________________`

**A4.** Prediction: do `add` and `sub` use the same opcode, or different
opcodes? Circle one, and write one sentence of reasoning.

**Same** &nbsp;&nbsp;&nbsp;&nbsp; **Different** &nbsp;&nbsp;&nbsp;&nbsp; **Not sure**

`________________________________________________________________`

*Stop here. We compare answers together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your instructor will hand this out after the class discussion of Part A.
It starts with the Part A answer key, then reveals the register-number
table and asks you to encode and decode two new instructions.

**Register numbers:** `$t0`=8, `$t1`=9, `$t2`=10, `$t3`=11, `$t4`=12,
`$t5`=13, `$t6`=14.

**B1.** Using the table above, fill in the numeric dest/src1/src2 values
for all three Part A instructions.

| Instr | Dest # | Src1 # | Src2 # |
|---|---|---|---|
| (1) `add $t0, $t1, $t2` | | | |
| (2) `sub $t3, $t4, $t5` | | | |
| (3) `add $t6, $t0, $t3` | | | |

**B2.** Was your Part A4 prediction (same opcode vs. different opcode)
correct? If not, in one sentence, what actually tells `add` and `sub`
apart?

`________________________________________________________________`

**B3.** Encode this new instruction into its fields: `sub $t1, $t6, $t2`

| Opcode | Dest # | Src1 # | Src2 # |
|---|---|---|---|
| | | | |

**B4.** Decode this instruction, and write its meaning in words:
dest register number 9, src1 register number 11, src2 register number
14, R-type opcode.

`________________________________________________________________`

**B5 (stretch, optional).** SmartPick wants to check whether the
customer's total (in `$t0`) is over a $50 discount threshold, stored
somewhere in memory. Can `add` and `sub` alone do this check? Why or why
not?

`________________________________________________________________`

---
---

# Instructor Answer Key — do not hand out this section

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
  reveal), short instructor-led discussion, Part B ~15 min (register
  numbers revealed + encode/decode practice).
- Do not reveal the register-number table during Part A — the value is
  in labeling fields correctly under uncertainty about the opcode, not
  in getting exact numbers early.
- If a pair finishes Part B early, point them to the handout's "Optional
  Reading" section, or have them try writing their own three-instruction
  chain like SmartPick's checkout example.
