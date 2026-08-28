# Week 10 Worksheet: Fixing Studio's Pipeline

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the professor can follow your thinking.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

Below are three short instruction pairs from Studio's pipeline. Each
table shows five cycles across the five stages: IF, ID, EX, MEM, WB.
**Do not look ahead to Part B yet.**

**Pair 1**

| Cycle | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| I1: `add` (computes a value) | IF | ID | EX | MEM | WB |
| I2: `sub` (needs that value) | | IF | ID | EX | MEM |

**Pair 2**

| Cycle | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| I1: `load` (reads memory) | IF | ID | EX | MEM | WB |
| I2: `add` (needs the loaded value) | | IF | ID | EX | MEM |

**Pair 3**

| Cycle | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| I1: `mul` (computes a value) | IF | ID | EX | MEM | WB |
| I2: `store` (does not need I1's value) | | IF | ID | EX | MEM |

**A1.** For each pair, circle the cycle where instruction 2 first needs
instruction 1's value (if it needs one at all).

`Pair 1: ______   Pair 2: ______   Pair 3: no value needed`

**A2.** For each pair, is this a **data hazard**, or **no hazard at
all**? Write your answer next to each pair number.

`Pair 1: ______________   Pair 2: ______________   Pair 3: ______________`

**A3.** For Pair 1, can plain forwarding (no stall) fix it? Why or why
not?

`________________________________________________________________`

**A4.** For Pair 2, can plain forwarding (no stall) fully fix it? Why or
why not?

`________________________________________________________________`
`________________________________________________________________`

**A5.** Draw an arrow (in words) showing where a forwarding wire would
go for Pair 1: from which stage, of which instruction, to which stage,
of which instruction?

`________________________________________________________________`

*Stop here. We compare answers together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your professor will hand this out after the class discussion of Part A.
It starts with the Part A answer key, then asks you to trace a branch.

### Part A answer key

- **A1:** Pair 1: cycle 4. Pair 2: cycle 4. Pair 3: no value needed
- **A2:** Pair 1: data hazard. Pair 2: data hazard (specifically, a
  **load-use hazard**). Pair 3: no hazard
- **A3:** Yes. Instruction 1's `add` result exists after its EX stage
  (cycle 3), which is before instruction 2 needs it (cycle 4).
  Forwarding sends it in time
- **A4:** No, not fully. Instruction 1's loaded value is not ready
  until its MEM stage finishes (cycle 4), the exact same cycle
  instruction 2 needs it in EX. One stall cycle is still needed before
  forwarding can deliver the value
- **A5:** From instruction 1's EX stage (cycle 3) to instruction 2's EX
  stage (cycle 4)

### B1: Trace a branch prediction

A branch instruction is predicted **taken**. The pipeline fetches two
instructions down the predicted path while the branch is still working
its way through the pipeline. The real outcome, known at the end of the
branch's EX stage, turns out to be **not taken** — the prediction was
wrong.

| Cycle | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Branch instruction | IF | ID | EX (outcome known here) | MEM | WB |
| Guessed instruction A | | IF | ID | EX | |
| Guessed instruction B | | | IF | ID | |

**B2.** How many instructions were fetched from the wrong (guessed)
path?

`________________________________________________________________`

**B3.** What must the pipeline do to those instructions, and at what
point (which cycle) does the pipeline know to do it?

`________________________________________________________________`
`________________________________________________________________`

**B4.** After the flush, where does the pipeline start fetching next?

`________________________________________________________________`

**B5.** A friend says: "A branch misprediction means the hardware made a
mistake." Write one sentence explaining why this is not quite right.

`________________________________________________________________`

**B6 (stretch, optional).** A much deeper pipeline (more stages) fetches
more wrongly guessed instructions before catching a misprediction. Why
does that make deep pipelines riskier, not just longer?

`________________________________________________________________`

---
---

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
