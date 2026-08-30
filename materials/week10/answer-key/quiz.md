# Answer Key

1. **B** — a hazard is a situation where overlapping instructions could compute a wrong answer, unless something is done about it
2. **C** — a data hazard: one instruction needs a value a previous instruction has not produced yet
3. **B** — forwarding sends a freshly computed result straight to the instruction that needs it, skipping the wait for the register file
4. **B** — a loaded value is not ready until the MEM stage finishes, one stage later than a normal computed value, so there is nothing yet to forward
5. **C** — a one-cycle stall (bubble) from the hazard detection unit, after which forwarding delivers the value normally
6. **B** — flush the wrongly fetched instructions so they never affect a stored value, then restart fetching on the correct path
7. **Model answer:** "Branches are common in real programs, so stalling on every one wastes a cycle almost constantly, giving up most of the speed pipelining was built to provide."
8. **Model answer:** "A data hazard is when an instruction needs a value a previous instruction has not produced yet, usually fixed with forwarding or a stall. A control hazard is when the pipeline fetches instructions before knowing which way a branch goes, fixed with branch prediction and a flush if the guess is wrong."
