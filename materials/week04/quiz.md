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
