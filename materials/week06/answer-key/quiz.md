# Answer Key

1. **B** — a datapath is the wiring inside a chip that moves data between its parts
2. **C** — the clock cycle must be long enough for the slowest instruction the design supports
3. **D** — add never reads or writes data memory; only load and store do
4. **B** — the control unit reads the opcode and switches on only the wires that instruction needs
5. **D** — 200 + 100 + 200 + 200 + 100 = 800 ps
6. **B** — every part of the datapath shares one clock signal, so all instructions get the same fixed cycle length
7. **Fetch -> Decode -> Execute -> Memory -> Write Back**
8. **Model answer:** "The clock cycle is fixed to the slowest instruction the datapath supports, so a faster instruction like add still must wait out that same full clock cycle before the next one can start."
