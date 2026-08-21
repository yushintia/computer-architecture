# Week 10 Self-Check Quiz (Ungraded)

Computer Architecture (503872-004). This quiz is **ungraded** — it is
only to help you check what stuck. About 10 minutes. Do not look back at
the slides while you answer.

---

**1.** What is a "hazard" in a pipeline?

A. A broken instruction that must be deleted
B. A situation where overlapping instructions could compute a wrong answer
C. A type of memory chip
D. A slower version of a pipeline

**2.** An instruction needs a value that the instruction right before it
has not produced yet. What is this called?

A. A control hazard
B. A structural hazard
C. A data hazard
D. A misprediction

**3.** What does "forwarding" (bypassing) do?

A. Deletes an instruction from the pipeline
B. Sends a freshly computed result straight to the instruction that needs it, before it is written back
C. Guesses which way a branch will go
D. Slows the clock down for one instruction

**4.** Why can forwarding alone not fully fix a load-use hazard?

A. Loaded values are always wrong
B. The loaded value is not ready until one stage later than a normal computed value
C. Forwarding only works for `add` instructions
D. Load instructions do not use the pipeline

**5.** What is the standard fix for a load-use hazard?

A. Always predict the load will fail
B. Flush the entire pipeline
C. A one-cycle stall (bubble), then forwarding delivers the value
D. Skip the instruction that needs the value

**6.** A branch is predicted "taken," but the real outcome turns out to
be "not taken." What must the pipeline do with the wrongly fetched
instructions?

A. Keep them and let them finish anyway
B. Flush them, then restart fetching on the correct path
C. Convert them into stalls
D. Nothing, they fix themselves

**7.** A classmate says: "The safest design is to always stall every
branch until its outcome is known." Give one reason this wastes
performance.

`_____________________________________________________________`

**8. (Short answer)** In 1-2 sentences, explain the difference between a
data hazard and a control hazard. Use at least one key word from this
week (forwarding, stall, branch prediction, flush).

`_____________________________________________________________`
`_____________________________________________________________`

---
---

# Answer Key

1. **B** — a hazard is a situation where overlapping instructions could compute a wrong answer, unless something is done about it
2. **C** — a data hazard: one instruction needs a value a previous instruction has not produced yet
3. **B** — forwarding sends a freshly computed result straight to the instruction that needs it, skipping the wait for the register file
4. **B** — a loaded value is not ready until the MEM stage finishes, one stage later than a normal computed value, so there is nothing yet to forward
5. **C** — a one-cycle stall (bubble) from the hazard detection unit, after which forwarding delivers the value normally
6. **B** — flush the wrongly fetched instructions so they never affect a stored value, then restart fetching on the correct path
7. **Model answer:** "Branches are common in real programs, so stalling on every one wastes a cycle almost constantly, giving up most of the speed pipelining was built to provide."
8. **Model answer:** "A data hazard is when an instruction needs a value a previous instruction has not produced yet, usually fixed with forwarding or a stall. A control hazard is when the pipeline fetches instructions before knowing which way a branch goes, fixed with branch prediction and a flush if the guess is wrong."
