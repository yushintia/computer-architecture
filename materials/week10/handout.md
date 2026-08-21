# Week 10 Handout: Pipelining II — Hazards and Their Fixes

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **Pipeline (recap)** | A chip design that overlaps instructions, so a new one starts almost every clock cycle |
| **IF / ID / EX / MEM / WB (recap)** | The five pipeline stages: fetch, decode, execute, memory access, write back |
| **Hazard** | A situation where overlapping pipeline instructions could compute a wrong answer, unless something is done about it |
| **Data hazard** | One instruction needs a value that a previous instruction has not produced yet |
| **Control hazard** | The pipeline fetches instructions before it knows which way a branch will go |
| **Structural hazard** | Two instructions need the exact same piece of hardware in the same cycle, like one shared memory port |
| **Register file** | The small, fast storage inside the chip that holds a program's working values |
| **Forwarding (bypassing)** | Sending a freshly computed result straight to the instruction that needs it, before it is written to the register file |
| **Stall (bubble)** | A pause, one or more clock cycles, inserted to fix a hazard by waiting |
| **Load-use hazard** | A data hazard forwarding alone cannot fully fix, because a loaded value is not ready until one stage later than a normal computed result |
| **Hazard detection unit** | A circuit that watches every pair of nearby instructions and pauses the pipeline exactly when needed |
| **Branch prediction** | A guess about which way a branch will go, made before the real answer is known |
| **Flush** | Throwing away wrongly fetched instructions after a guessed branch turns out wrong |
| **Misprediction penalty** | The number of cycles lost when a branch guess turns out wrong |

---

## 2. The SmartPick Story, Worked Out Step by Step

This is the full version of the story from class. Read it slowly if the
in-class pace felt fast.

**The situation.** Last week, SmartPick's Studio laptop got faster by
overlapping instructions in a five-stage pipeline. This week, a
technician finds two bugs: sometimes a calculation gives an old, wrong
number, and sometimes a stock-check program takes the wrong next step.

**Bug 1: multiply, then use the answer right away.**

| Cycle | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Instr 1: multiply | IF | ID | EX (computes result) | MEM | WB (writes result) |
| Instr 2: use result | | IF | ID | EX (needs result now) | MEM |

**Step 1: find where the timing breaks.** Instruction 2 reaches EX in
cycle 4, needing the multiply's answer. Instruction 1 does not write
that answer into the register file until WB, in cycle 5. One cycle too
late. Without help, instruction 2 reads an old, wrong value sitting in
the register file.

**Step 2: apply the fix.** The chip adds a direct wire from instruction
1's EX output straight to instruction 2's EX input. This is
**forwarding**. Instruction 2 no longer waits for the register file at
all — it grabs the fresh value the moment instruction 1 computes it.

| Cycle | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Instr 1: multiply | IF | ID | EX (forwards result) | MEM | WB |
| Instr 2: use result | | IF | ID | EX (uses forwarded value) | MEM |

No cycle is wasted. Both instructions keep moving at full speed, and the
answer is always correct.

**Step 3: the one case forwarding cannot reach.** Now instruction 1 is a
**load** instead of a multiply. A loaded value is not ready until the
MEM stage finishes, one stage later than a computed result.

| Cycle | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Instr 1: load value | IF | ID | EX | MEM (value ready here) | WB |
| Instr 2: use value | | IF | ID | EX (needs it now) | MEM |

Instruction 2 needs the value in cycle 4. It does not exist until cycle
4's MEM stage finishes — the same cycle, too late to forward in time.
This is the **load-use hazard**. The **hazard detection unit** spots this
exact pattern and freezes instruction 2 for one cycle (a stall, or
bubble). After the pause, forwarding delivers the value normally.

**Bug 2: the stock-check branch.** A program checks "is this item in
stock?" and picks one of two next steps. The pipeline must fetch the
next instruction immediately, before the check's answer is ready —
otherwise it would stall on almost every branch. The chip makes a
**branch prediction**: a guess about which way the branch goes, and
keeps fetching down that guessed path.

- If the guess is right, no time is lost at all.
- If the guess is wrong, the chip **flushes** the wrongly fetched
  instructions before they finish, then restarts fetching on the
  correct path. The cycles lost are the **misprediction penalty**.

**Step 4: state clearly what we can, and cannot, say yet.** We *can* now
say Studio's pipeline is both fast and correct: forwarding, a
single-cycle stall for load-use, and predict-then-flush for branches. We
*cannot* yet say the pipeline is as fast as it could be — every one of
these instructions still has to reach out to memory, and if memory is
slow, hazard handling alone does not help. That is Week 11's job.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations that were trimmed from the slides
to keep class time short. Read it if you are curious or want more
examples.

**There are three hazard families, not just two.** This week focused on
data hazards and control hazards, the two that show up constantly.
Textbooks also name a **structural hazard**: two instructions need the
same piece of hardware (like one memory port) in the same cycle. Modern
chips avoid most structural hazards with extra hardware copies, so they
come up far less often in practice than data or control hazards.

**Forwarding has a formal name: Tomasulo's idea, generalized.** Robert
Tomasulo built his forwarding-like scheme in 1967 for one specific,
expensive IBM machine's floating-point unit. The RISC pipelines of the
1980s (MIPS at Stanford, RISC-I at Berkeley) turned a similar idea into
simple, standard, built-in hardware for every instruction, not just a
rare special case. That simpler, always-on version is what modern chips
use today.

**Branch prediction gets much smarter than "always guess the same way."**
Real chips keep a short history of how a specific branch behaved
recently and predict based on that pattern — this is called **dynamic**
branch prediction, versus a fixed guess called **static** prediction. A
deeply pipelined chip (many stages) pays a much bigger misprediction
penalty than a shallow one, because more wrongly fetched instructions
must be flushed. This is one reason very deep pipelines can be a risky
design choice, not an automatic win.

**Software also helps avoid hazards.** A compiler can reorder
instructions so that a load and its first use are not right next to each
other, hiding the load-use stall without changing the program's result.
This is called **instruction scheduling**, and it is one reason
compiler design connects directly to processor design.

**Where this shows up around you.**

- **Every modern CPU (phone, laptop, server):** forwarding and branch prediction are standard, not optional, hardware
- **Compilers:** instruction scheduling passes exist specifically to reduce stalls
- **CPU verification engineers:** spend real career time proving a pipeline's hazard logic never produces a wrong answer
- **Game and simulation code:** branch-heavy code (lots of `if` statements) is more sensitive to misprediction cost than straight-line code

**Who actually designs this, as a job.**

- **Microarchitects** decide how forwarding paths and the hazard detection unit are wired
- **Verification / validation engineers** write tests that try to catch any hazard the hardware misses
- **Compiler engineers** write instruction schedulers that avoid stalls before the hardware even sees the code
- **Performance engineers** measure how often branch mispredictions actually slow down a real program

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** Instruction 1 computes a value in EX at cycle 3.
Instruction 2, right behind it, needs that value in its own EX at cycle
4. Without forwarding, what would instruction 2 read, and why is it
wrong?

> **Answer:** It would read whatever old value is sitting in the
> register file, because instruction 1 has not written its result there
> yet (that happens in WB, cycle 5). The read comes one cycle too early.

**Problem 2.** Name the hazard in Problem 1, and name the fix that
solves it with zero lost cycles.

> **Answer:** A data hazard. Forwarding fixes it: the chip wires
> instruction 1's EX result straight into instruction 2's EX input.

**Problem 3.** Instruction 1 is a `load`. Instruction 2, right behind
it, needs the loaded value. Why does forwarding alone not fully solve
this case?

> **Answer:** A loaded value is not ready until the MEM stage finishes,
> one stage later than a normal computed value. By the time instruction
> 2 reaches EX, the value does not exist yet, so there is nothing to
> forward.

**Problem 4.** What is the standard fix for the case in Problem 3, and
how many cycles does it typically cost?

> **Answer:** A one-cycle stall (bubble), inserted by the hazard
> detection unit. After that single pause, forwarding delivers the value
> normally.

**Problem 5.** A branch is predicted "taken," and the pipeline fetches
three instructions down that path before the branch's real outcome is
known. The prediction turns out wrong. What must happen to those three
instructions?

> **Answer:** They must be flushed — thrown away before they reach WB —
> so they never change any stored value. The pipeline then restarts
> fetching on the correct path.

**Problem 6.** A classmate says: "To be completely safe, the pipeline
should just stall on every single branch until the outcome is known."
Give one reason this is a bad design choice, even though it is correct.

> **Answer:** It wastes a cycle on almost every branch, since branches
> are common in real programs. This gives up most of the speed
> pipelining was built to provide, even though the answers would still
> be correct.
