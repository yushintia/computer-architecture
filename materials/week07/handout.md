# Week 7 Handout: Multi-Cycle Datapath

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **Single-cycle datapath** | Last week's chip design: every instruction runs in exactly one clock tick, sized for the slowest instruction |
| **Multi-cycle design** | A chip design that gives each instruction only as many short clock ticks as it actually needs |
| **Step (stage)** | One small piece of work a chip does while running an instruction, such as "read a register" or "access memory" |
| **Clock cycle (tick)** | One "beat" of the chip's clock. In multi-cycle design, one tick equals one step, not one whole instruction |
| **Cycle count** | How many clock ticks one instruction actually takes to finish. Different instructions can have different cycle counts |
| **Reuse (shared hardware)** | Using the same piece of hardware, like the ALU, more than once for different jobs inside one instruction |
| **Temporary register** | A small storage spot that holds one value between ticks, so it is not lost while work continues over several ticks |
| **Instruction register (IR)** | A temporary register that holds the current instruction so the chip can still read it in later steps |
| **Memory data register (MDR)** | A temporary register that holds a value just read from memory, until it can be saved into a normal register |
| **Control unit** | The part of a chip that decides what happens on each clock tick: which wires turn on, and what step runs next |
| **Finite state machine** | A small circuit that moves through a fixed set of steps ("states"), one tick at a time, based on what happened before |
| **Microprogramming** | Storing the list of control steps as data in a small memory, instead of wiring one giant fixed circuit. Invented by Maurice Wilkes, 1951 |
| **Idle** | Doing no useful work while waiting. Multi-cycle chips are idle between finishing one instruction and starting the next |
| **Overlap** | Starting a new piece of work before the current one is fully finished. Multi-cycle chips do not do this yet — that is next week's topic |

---

## 2. The Timing Fix, Worked Out Step by Step

This is the full version of the story from class. Read it slowly if the
in-class pace felt fast.

**The situation.** An engineer studies last week's single-cycle chip.
She runs a small program: 1,000 `add` instructions and 100 `lw` (load
word) instructions. She expects the adds to finish quickly. They do not.

**Step 1: Why did every instruction wait the same time?** Last week's
chip used one fixed clock tick, long enough for the slowest instruction,
`lw`. `lw` needs five actions: fetch the instruction, read a register,
compute a memory address, read memory, and save the result. `add` only
needs four of the five steps `lw` needs (skipping memory access, but
using different total work), yet both instructions had to wait for the
exact same fixed tick either way.

**Step 2: Split the work into short steps.** Multi-cycle design breaks
execution into five possible short steps: Fetch, Decode, Execute,
Memory, Write Back. Each step becomes its own, much shorter, clock tick.

**Step 3: Let each instruction skip steps it does not need.**

| Instruction | Steps used | Steps skipped | Total ticks |
|---|---|---|---|
| `add` (R-type) | Fetch, Decode, Execute, Write Back | Memory | 4 |
| `lw` (load word) | Fetch, Decode, Execute, Memory, Write Back | none | 5 |
| `sw` (store word) | Fetch, Decode, Execute, Memory | Write Back | 4 |
| `beq` (branch) | Fetch, Decode, Execute | Memory, Write Back | 3 |

**Step 4: Compute the real time saved.** Assume the old single-cycle
tick was 500 ns (nanoseconds), and each new short step takes 100 ns.

- **Single-cycle total:** 1,000 adds × 500 ns + 100 loads × 500 ns = 500,000 ns + 50,000 ns = **550,000 ns**
- **Multi-cycle total:** 1,000 adds × 400 ns (4 steps) + 100 loads × 500 ns (5 steps) = 400,000 ns + 50,000 ns = **450,000 ns**
- **Savings:** 100,000 ns, about **18% less total time**, on the exact same program

**Step 5: State clearly what we can, and cannot, say yet.** We *can* say
multi-cycle saves real time by not forcing short instructions to wait
for the longest one. We *cannot* yet say the chip works on more than one
instruction at once — it still finishes one fully before starting the
next. That overlap is Week 9's job (after the Week 8 midterm review).

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations that were trimmed from the slides
to keep class time short. Read it if you are curious or want more
examples.

**Why "notepads" (temporary registers) are new this week.** Last week's
chip finished each instruction inside one tick, so nothing needed to be
remembered between ticks — the whole instruction happened and vanished
in one beat. This week, one instruction's work is spread across several
ticks, so the chip needs small storage spots (the instruction register,
the memory data register, and a few others) to hold values steady from
one tick to the next, until a later step needs them.

**Two ways to build the control unit.** Maurice Wilkes's 1951 idea,
microprogramming, stores the control steps as data: a small memory holds
a "recipe," and the control unit reads one line per tick. The
alternative is a hardwired finite state machine: a fixed circuit built
directly out of logic gates, with no separate memory for the recipe.
Real chips have used both approaches at different times, and modern
chips often mix them — a hardwired core for common instructions, plus
microcode for rare, complex ones.

**A everyday version of the same idea.** Think of a coffee shop that
makes every drink, simple or complex, using one fixed 5-minute slot,
because that is how long the most complicated drink takes. A
multi-cycle shop instead breaks drink-making into short steps (grind,
pour, steam milk, add syrup) and skips steps a simple drink does not
need. A plain coffee finishes in two steps; a specialty latte still uses
all four. Same staff, same equipment, much less wasted time overall.

**Where this shows up around you.**

- **Older CPUs (1970s-80s):** many real processors, including early x86 chips, used multi-cycle and microprogrammed control directly
- **Modern CPUs:** still use microcode internally for rare, complex instructions, even though the main pipeline (Week 9) is far more advanced
- **Embedded chips:** simple, low-cost microcontrollers still often use multi-cycle designs, since chip area and cost matter more than raw speed
- **Digital logic courses:** finite state machines, taught as a general tool, are the exact circuit type a control unit uses here

**Who actually designs this, as a job.**

- **Digital design engineers** build the actual datapath and control unit circuits from logic gates
- **Verification engineers** test that the control unit picks the correct next step for every instruction type, including rare edge cases
- **Computer architects** decide how many steps each instruction type should take, balancing speed against circuit complexity
- **Firmware / microcode engineers** write and update the stored "recipe" for chips that still use microprogrammed control

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** In one sentence, explain why last week's single-cycle
chip wastes time on a fast instruction like `add`.
> **Answer:** Because every instruction must wait for one fixed clock
> tick, sized for the slowest instruction, even if `add` finishes its
> own work sooner.

**Problem 2.** List the five possible steps of a multi-cycle
instruction, in order.
> **Answer:** Fetch, Decode, Execute, Memory, Write Back.

**Problem 3.** `beq` (branch) uses only 3 of the 5 steps. Which two
steps does it skip, and why might it not need them?
> **Answer:** It skips Memory and Write Back. A branch only compares two
> register values and decides where to go next — it never reads or
> writes data memory, and it does not save a result into a register.

**Problem 4.** Assume one short multi-cycle step takes 100 ns. How long
does one `lw` instruction take in total? How long does one `sw`
instruction take?
> **Answer:** `lw` uses 5 steps: 5 × 100 ns = 500 ns. `sw` uses 4 steps:
> 4 × 100 ns = 400 ns.

**Problem 5.** A program has 500 `add` instructions and 200 `lw`
instructions. Using the 100 ns-per-step assumption above, compute the
total multi-cycle time.
> **Answer:** 500 × 400 ns (4 steps) + 200 × 500 ns (5 steps) =
> 200,000 ns + 100,000 ns = **300,000 ns**.

**Problem 6.** True or false: multi-cycle design lets two different
instructions run at the same time. Explain your answer in one sentence.
> **Answer:** False. Multi-cycle still finishes one instruction
> completely, step by step, before starting the next one — that overlap
> is Week 9's topic (Pipelining), not this week's.
