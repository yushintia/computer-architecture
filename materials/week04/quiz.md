# Week 4 Self-Check Quiz (Ungraded)

Computer Architecture (503872-004). This quiz is **ungraded** — it is
only to help you check what stuck. About 10 minutes. Do not look back at
the slides while you answer.

---

**1.** Which of these best describes an ISA (Instruction Set
Architecture)?

A. One specific way a chip is physically wired
B. The fixed agreement between hardware and software about which bit patterns exist as instructions, and what each one means
C. The speed at which a processor's clock ticks
D. A programming language like Python or C

**2.** An instruction has two parts. Which pair correctly names them?

A. Register and memory
B. Encode and decode
C. Opcode and operand
D. Source and destination only

**3.** What does the instruction `sub $t1, $t2, $t3` compute?

A. `$t1 = $t2 + $t3`
B. `$t2 = $t1 - $t3`
C. `$t1 = $t2 - $t3`
D. `$t3 = $t1 - $t2`

**4.** True or false: `add` and `sub` use different opcodes to tell them
apart.

A. True — each instruction always needs its own unique opcode
B. False — they share the same opcode; a separate hidden field (revealed in Week 6) tells them apart
C. True — but only in some ISAs, not MIPS
D. False — they have no opcode at all

**5.** Register numbers this week: `$t0`=8, `$t1`=9, `$t2`=10. Encode
`add $t0, $t1, $t2` into its dest/src1/src2 register numbers.

A. Dest 9, Src1 8, Src2 10
B. Dest 8, Src1 9, Src2 10
C. Dest 10, Src1 9, Src2 8
D. Dest 8, Src1 10, Src2 9

**6.** Why can this week's `add` and `sub` instructions not read a value
stored in memory?

A. They are broken and need to be fixed in a future ISA version
B. Memory does not exist yet in this course
C. `add` and `sub` are R-type instructions, which only work on values already sitting in registers
D. Registers and memory always hold the exact same values, so it does not matter

**7.** In 1964, IBM System/360 mattered because it:

A. Was the first computer ever built
B. Let one shared ISA span a whole family of machines, so customer software kept working when they upgraded
C. Introduced the first microarchitecture
D. Replaced assembly language with binary

**8. (Short answer)** In 1-2 sentences, explain why "the opcode alone is
the whole instruction" is a mistake. Use at least one key word from this
week (opcode, operand, R-type).

`_____________________________________________________________`
`_____________________________________________________________`

---
---

# Answer Key

1. **B** — the ISA is the fixed agreement between hardware and software about which bit patterns exist as instructions and what each means
2. **C** — opcode ("what to do") and operand ("what to do it to") are the two parts of every instruction
3. **C** — `sub $t1, $t2, $t3` means `$t1 = $t2 - $t3`: dest first, then src1, then src2
4. **B** — `add` and `sub` are both R-type and actually share the same opcode; a separate hidden field, not covered until Week 6, is what tells them apart
5. **B** — dest is `$t0` (8), src1 is `$t1` (9), src2 is `$t2` (10), matching the instruction's own order
6. **C** — R-type instructions like `add` and `sub` only work on values already loaded into registers; reaching memory needs a different kind of instruction, not named yet
7. **B** — System/360 let machines of very different sizes and prices share one ISA, so a customer's software kept working after an upgrade
8. **Model answer:** "The opcode only names the general job (like `add`); the operand fields say which specific registers to use, and the same opcode with different operands does completely different work. An R-type instruction needs both parts to be a complete, meaningful instruction."
