# Week 3 Worksheet: SmartPick's Register, Bit by Bit

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the instructor can follow your thinking.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

SmartPick's inventory system stores every quantity and stock code as
bits. Practice converting them, using the steps from class.

**A1.** SmartPick has 18 pairs of headphones in stock. Convert 18 to
binary. Show your steps.

`________________________________________________________________`

**A2.** A quantity is stored as the byte `00010111`. Convert it to
decimal.

`________________________________________________________________`

**A3.** A stock code is stored as the byte `10101100`. Convert it to
hexadecimal. Show both nibbles.

`________________________________________________________________`

**A4.** Prediction: can one single byte, like `11111011`, represent two
different decimal numbers, depending on how it is read? Circle one.

**Yes** &nbsp;&nbsp;&nbsp;&nbsp; **No** &nbsp;&nbsp;&nbsp;&nbsp; **Not sure**

**A5.** What is one thing about reading bytes correctly that you are
still not sure about?

`________________________________________________________________`

*Stop here. We compare answers together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your instructor will hand this out after the class discussion of Part A.
It starts with the real answer to A4, then asks you to explain it.

**The real answer to A4:** Yes. The byte `11111011` is 251 read as
unsigned, but -5 read as signed two's complement. The bits never say
which reading is correct on their own.

**B1.** Was your Part A prediction (A4) correct?

`Yes  /  No  /  Partly`

**B2.** Using the words **sign bit** and **two's complement**, explain
in 1-2 sentences why `11111011` does not obviously look like a negative
number just by looking at it.

`________________________________________________________________`
`________________________________________________________________`

**B3.** SmartPick's return counter uses an 8-bit **unsigned** field to
count today's returns. It is already at 255, the largest number 8 bits
can hold unsigned. What happens when the 256th return is processed?

`________________________________________________________________`

**B4.** SmartPick's receipt printer stamps the status code "OK" as two
ASCII bytes. Using `'O'` = 79 and `'K'` = 75, write each letter's byte
in 8-bit binary.

`'O'` = `________________`   &nbsp;&nbsp; `'K'` = `________________`

**B5 (stretch, optional).** A programmer accidentally stores a laptop
refund amount using an **unsigned** number type instead of **signed**.
What might go wrong when a refund needs to show a negative amount?

`________________________________________________________________`

---
---

# Instructor Answer Key — do not hand out this section

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

- Total time: Part A ~15 min (prediction only, no reveal), short instructor-led discussion, Part B ~15 min (reveal + explain)
- Do not let Part A run long — the value is in predicting under uncertainty, not in getting the "right" answer
- If a pair finishes Part B early, point them to the handout's "Optional Reading" section
