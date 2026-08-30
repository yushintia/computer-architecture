# Week 4 Worksheet: Encoding SmartPick's Checkout Register

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the professor can follow your thinking.

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

Your professor will hand this out after the class discussion of Part A.
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
