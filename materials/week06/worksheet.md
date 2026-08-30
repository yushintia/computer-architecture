# Week 6 Worksheet: Tracing SmartPick's Datapath

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the professor can follow your thinking.

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

Your professor will hand this out after the class discussion of Part A.
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
