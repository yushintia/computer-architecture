# Week 5 Self-Check Quiz (Ungraded)

Computer Architecture (503872-004). This quiz is **ungraded** — it is
only to help you check what stuck. About 10 minutes. Do not look back at
the slides while you answer. This is separate from today's Quiz 1.

---

**1.** Which instruction copies a value **from memory into a
register**?

A. `add`
B. `lw`
C. `sw`
D. `beq`

**2.** Which instruction format uses a register plus a small built-in
number, like `addi`, `lw`, and `beq`?

A. R-type
B. I-type
C. J-type
D. None of these

**3.** What does a branch instruction do on its own, without a jump?

A. It always repeats the program from the start
B. It only decides whether to jump; it cannot repeat steps by itself
C. It writes a value into memory
D. It changes the clock speed of the processor

**4.** What is the RISC "load-store" rule?

A. Every instruction may read or write memory directly
B. Only load and store instructions may touch memory; all others use registers only
C. Loops must always use the `jal` instruction
D. Registers may only hold whole numbers, never addresses

**5.** Which historical event is correctly matched to its year?

A. 1945 — RISC project begins at Berkeley
B. 1949 — EDSAC includes a conditional jump instruction
C. 1980s — von Neumann designs the first stored-program computer
D. Today — CISC replaces RISC in most modern chips

**6.** Put these steps in order for a search loop: `check for a match`,
`load the next price`, `move to the next item`, `jump back if not
found`.

`_____________________________________________________________`

**7.** True or false: an I-type instruction can compute using only two
registers, with no constant number involved.

`_____________________________________________________________`

**8. (Short answer)** In 1-2 sentences, explain why last week's
instruction set (add and subtract only) could not write a program that
searches a list in memory. Use at least one key word from this week
(load, branch, jump, or loop).

`_____________________________________________________________`
`_____________________________________________________________`

---
---

# Answer Key

1. **B** — `lw` (load word) copies a value from memory into a register; `sw` goes the opposite direction
2. **B** — I-type instructions use a register plus a small built-in number
3. **B** — a branch only decides whether to jump; it needs a jump back to actually repeat
4. **B** — only load and store touch memory; every other instruction works on registers only
5. **B** — EDSAC (1949) built in a conditional jump from day one; the RISC project was 1980s, not 1945
6. **load the next price -> check for a match -> move to the next item -> jump back if not found**
7. **False** — that describes R-type; I-type instructions always involve a small built-in constant
8. **Model answer:** "Add and subtract only work on values already sitting in registers, so they cannot load a list from memory or repeat a check with a loop. Searching a list needs load, branch, and jump together."
