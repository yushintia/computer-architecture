# Week 6 Self-Check Quiz (Ungraded)

Computer Architecture (503872-004). This quiz is **ungraded** — it is
only to help you check what stuck. About 10 minutes. Do not look back at
the slides while you answer.

---

**1.** Which of these best describes a "datapath"?

A. The list of commands a processor understands
B. The wiring inside a chip that moves data from one part to another
C. The brand name printed on the chip
D. The operating system installed on a laptop

**2.** In a single-cycle design, what decides the length of the clock
cycle?

A. The fastest instruction the design supports
B. The average time across all instruction types
C. The slowest instruction the design supports
D. Whichever instruction runs most often

**3.** Which datapath part does an `add` instruction never use?

A. Register File
B. ALU
C. Instruction Memory
D. Data Memory

**4.** What does the control unit read to decide which wires to switch
on?

A. The clock cycle length
B. The opcode, the short code naming the operation
C. The size of the register file
D. The brand of ALU used

**5.** Using this week's stage timings (fetch 200 ps, register read 100
ps, ALU 200 ps, data memory 200 ps, register write 100 ps), how much
real time does a load instruction need?

A. 500 ps
B. 600 ps
C. 700 ps
D. 800 ps

**6.** Why can a single-cycle datapath not give a fast instruction a
shorter clock cycle than a slow one?

A. Fast instructions are actually rare, so it does not matter
B. Every instruction shares one single clock signal
C. The control unit forbids it by rule
D. The ALU is too slow to allow it

**7.** Put these in the correct order, from first to last, for a load
instruction: `Memory`, `Fetch`, `Write Back`, `Decode`, `Execute`.

`_____________________________________________________________`

**8. (Short answer)** In 1-2 sentences, explain why an `add` instruction
still takes a full clock cycle, even though it never touches data
memory. Use at least one key word from this week (datapath, control
unit, clock cycle).

`_____________________________________________________________`
`_____________________________________________________________`
