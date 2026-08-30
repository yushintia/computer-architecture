# Answer Key

1. **B** — `lw` (load word) copies a value from memory into a register; `sw` goes the opposite direction
2. **B** — I-type instructions use a register plus a small built-in number
3. **B** — a branch only decides whether to jump; it needs a jump back to actually repeat
4. **B** — only load and store touch memory; every other instruction works on registers only
5. **B** — EDSAC (1949) built in a conditional jump from day one; the RISC project was 1980s, not 1945
6. **load the next price -> check for a match -> move to the next item -> jump back if not found**
7. **False** — that describes R-type; I-type instructions always involve a small built-in constant
8. **Model answer:** "Add and subtract only work on values already sitting in registers, so they cannot load a list from memory or repeat a check with a loop. Searching a list needs load, branch, and jump together."
