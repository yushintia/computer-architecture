# Week 6 Worksheet: Tracing SmartPick's Datapath

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the instructor can follow your thinking.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

Below is a plain list of every part in SmartPick's single-cycle
datapath. **Do not look ahead to Part B yet.**

**The parts:** Program Counter (PC), Instruction Memory, Register File,
ALU, Data Memory, Control Unit.

The instruction is: `add $t0, $t1, $t2` — it adds two register values
and stores the result in a third register.

**A1.** List every part you think this add instruction actually passes
through, in order.

`________________________________________________________________`

**A2.** Cross out, from the full parts list above, any part you think
add does **not** need at all.

`________________________________________________________________`

**A3.** Prediction: does add ever read or write Data Memory? Circle one.

**Yes** &nbsp;&nbsp;&nbsp;&nbsp; **No** &nbsp;&nbsp;&nbsp;&nbsp; **Not sure**

**A4.** In 1-2 sentences, explain your reasoning for A3.

`________________________________________________________________`
`________________________________________________________________`

**A5.** Now do the same for a load instruction (`lw $t0, 0($t1)`, "load
the value at this address into $t0"). Does it use Data Memory? Circle
one.

**Yes** &nbsp;&nbsp;&nbsp;&nbsp; **No** &nbsp;&nbsp;&nbsp;&nbsp; **Not sure**

*Stop here. We compare predictions together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your instructor will hand this out after the class discussion of Part A.
It starts with the real answer, then asks you to compute real timing
numbers.

**The real path.** `add $t0, $t1, $t2` uses: Instruction Memory (fetch),
Register File (decode, read `$t1` and `$t2`), ALU (execute, adds them),
and Register File again (write back, store into `$t0`). It never touches
Data Memory.

`lw $t0, 0($t1)` uses all of those, **plus** Data Memory, to actually
read the value at the computed address.

**B1.** Was your Part A prediction (A3) correct?

`Yes  /  No  /  Partly`

**Timing table** (use these for B2-B4): fetch = 200 ps, register read =
100 ps, ALU = 200 ps, data memory = 200 ps, register write = 100 ps.

**B2.** Compute the real time needed by `add`.

`________________________________________________________________`

**B3.** Compute the real time needed by `lw` (load word).

`________________________________________________________________`

**B4.** If the datapath's clock cycle must fit the slower of the two,
how much time does `add` waste every single cycle?

`________________________________________________________________`

**B5.** A friend says: "Since add finishes early, it should just use a
shorter clock cycle than load." Write one sentence explaining why a
single-cycle datapath cannot actually do this.

`________________________________________________________________`

**B6 (stretch, optional).** A branch instruction (fetch, decode, execute
only, no memory or write back) needs 500 ps. How much time does it waste
every cycle, using the same clock cycle length as B4?

`________________________________________________________________`

---
---

# Instructor Answer Key — do not hand out this section

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

- Total time: Part A ~15 min (prediction only, no reveal), short instructor-led discussion, Part B ~15 min (reveal + compute)
- Do not let Part A run long — the value is in predicting under uncertainty, not in getting the "right" answer
- If a pair finishes Part B early, point them to the handout's "Optional Reading" section, especially "why two adders, not one"
