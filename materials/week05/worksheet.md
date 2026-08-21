# Week 5 Worksheet: Completing SmartPick's Search Program

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the instructor can follow your thinking.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

SmartPick keeps a shelf price list in memory, five laptops long:

| Position | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Price ($) | 640 | 710 | 525 | 890 | 705 |

A customer wants to know: is a laptop priced **$525** on the shelf
today? **Do not look ahead to Part B yet.**

**A1.** In plain words (not code), write the first step your program
must take before it can check anything.

`________________________________________________________________`

**A2.** In plain words, write the one question your program must ask
about each price, one at a time.

`________________________________________________________________`

**A3.** In plain words, write what your program should do if the
answer to A2 is "no, not yet."

`________________________________________________________________`

**A4.** In plain words, write what your program should do if the
answer to A2 is "yes, found it."

`________________________________________________________________`

**A5.** At most, how many times does your loop need to repeat its
question, for a 5-item list?

`________________________________________________________________`

*Stop here. We compare your plain-word steps together before you see
Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your instructor will hand this out after the class discussion of Part
A. It starts with the real answer, then asks you to encode two
instructions by hand.

**The real program:**

```
addi $t0, $zero, 525   # target price we're looking for
addi $t1, $a0, 0       # t1 = address of first price
addi $t2, $a0, 20      # t2 = address just past the list (5 items)

loop:
lw   $t3, 0($t1)       # t3 = this laptop's price
beq  $t3, $t0, found   # match! stop here
addi $t1, $t1, 4       # move to the next laptop
bne  $t1, $t2, loop    # if list not done, repeat

found:
```

**B1.** Was your Part A plan close to this? What is one thing you
would change now?

`________________________________________________________________`

**B2.** Using the words **branch** and **jump**, explain in 1-2
sentences why this loop needs both.

`________________________________________________________________`
`________________________________________________________________`

**Now, encode by hand.** Every instruction's bits start with an
**opcode**, the number that names its job. Here is a simplified
reference:

| Instruction | Opcode (decimal) |
|---|---|
| `addi` | 8 |
| `lw` | 35 |
| `sw` | 43 |
| `beq` | 4 |
| `bne` | 5 |

And a short register-number reference: `$zero` = 0, `$a0` = 4, `$t0` =
8, `$t1` = 9, `$t2` = 10, `$t3` = 11.

**B3.** Fill in the table below for the line `lw $t3, 0($t1)`.

| Field | Your answer |
|---|---|
| Opcode | `____` |
| Register holding the address | `____` |
| Register receiving the value | `____` |
| Offset number | `____` |

**B4.** Fill in the table below for the line `beq $t3, $t0, found`.

| Field | Your answer |
|---|---|
| Opcode | `____` |
| First register compared | `____` |
| Second register compared | `____` |

**B5 (stretch, optional).** A friend says a bigger instruction set,
with hundreds of opcodes, must always be better. Write one sentence of
pushback.

`________________________________________________________________`

---
---

# Instructor Answer Key — do not hand out this section

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
  instructor-led discussion, Part B ~15 min (reveal + encode)
- Do not let Part A run long — the value is reasoning about the loop's
  shape, not writing perfect mnemonics yet
- Quiz 1 follows shortly after Part B in the same session — keep the
  discussion tight so there is time
- If a pair finishes Part B early, point them to the handout's
  "Optional Reading" section
