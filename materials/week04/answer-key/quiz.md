# Answer Key

1. **B** — the ISA is the fixed agreement between hardware and software about which bit patterns exist as instructions and what each means
2. **C** — opcode ("what to do") and operand ("what to do it to") are the two parts of every instruction
3. **C** — `sub $t1, $t2, $t3` means `$t1 = $t2 - $t3`: dest first, then src1, then src2
4. **B** — `add` and `sub` are both R-type and actually share the same opcode; a separate hidden field, not covered until Week 6, is what tells them apart
5. **B** — dest is `$t0` (8), src1 is `$t1` (9), src2 is `$t2` (10), matching the instruction's own order
6. **C** — R-type instructions like `add` and `sub` only work on values already loaded into registers; reaching memory needs a different kind of instruction, not named yet
7. **B** — System/360 let machines of very different sizes and prices share one ISA, so a customer's software kept working after an upgrade
8. **Model answer:** "The opcode only names the general job (like `add`); the operand fields say which specific registers to use, and the same opcode with different operands does completely different work. An R-type instruction needs both parts to be a complete, meaningful instruction."
