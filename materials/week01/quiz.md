# Week 1 Self-Check Quiz (Ungraded)

Computer Architecture (503872-004). This quiz is **ungraded** — it is
only to help you check what stuck. About 10 minutes. Do not look back at
the slides while you answer.

---

**1.** Which of these best describes an ISA (Instruction Set
Architecture)?

A. The physical wires and transistors on a chip
B. The fixed list of commands a processor understands
C. The brand name printed on the box
D. The operating system installed on a laptop

**2.** Two laptops have the exact same clock speed (GHz). What does this
tell you about their real-world performance?

A. They will always run at exactly the same speed
B. Nothing on its own — performance also depends on the microarchitecture
C. The more expensive one is always faster
D. Clock speed is the only thing that matters for performance

**3.** What is a "microarchitecture"?

A. A very small building design
B. One specific way of building a processor that carries out an ISA's commands
C. Another name for an operating system
D. The brand of transistor used in a chip

**4.** Convert the decimal number **11** to binary.

A. `1011`
B. `1101`
C. `1110`
D. `0111`

**5.** What caused chipmakers to shift from raising clock speed to
adding more cores, around 2004?

A. Software stopped needing faster processors
B. Higher clock speeds made chips too hot to cool affordably (the "power wall")
C. Transistors stopped getting smaller
D. Customers stopped buying fast laptops

**6.** A bigger cache generally helps performance because it:

A. Makes the ISA simpler
B. Increases the advertised clock speed
C. Reduces how often the processor needs a slow trip to main memory
D. Adds more cores to the chip

**7.** Put these in the correct order, from the code you write to the
physical chip: `ISA`, `Transistors`, `Application`, `Microarchitecture`,
`Logic Gates`.

`_____________________________________________________________`

**8. (Short answer)** In 1-2 sentences, explain why two laptops with the
same advertised clock speed can finish the same task in very different
amounts of time. Use at least one key word from this week (ISA,
microarchitecture, cache).

`_____________________________________________________________`
`_____________________________________________________________`

---
---

# Answer Key

1. **B** — the ISA is the fixed list of commands a processor understands, the contract between software and hardware
2. **B** — same clock speed guarantees nothing about real speed on its own; the microarchitecture underneath can differ
3. **B** — microarchitecture is one specific way of implementing an ISA in circuits
4. **A** — `1011` (8 + 0 + 2 + 1 = 11)
5. **B** — the "power wall": pushing clock speed higher made chips too hot to cool affordably, so the industry moved to multicore instead
6. **C** — a bigger cache keeps more data close to the processor, so it needs main memory less often, on average
7. **Application -> ISA -> Microarchitecture -> Logic Gates -> Transistors**
8. **Model answer:** "They can share the same ISA, so the same software runs on both, but have different microarchitectures. A design with a better microarchitecture (or bigger cache) needs fewer steps to finish the same work, so it is faster even at the same GHz."
