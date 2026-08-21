# Week 9 Handout: Pipelining I

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **Pipelining** | A hardware technique that splits an instruction's work into stages, so several instructions can be in different stages at the same time |
| **Stage** | One small, independent piece of an instruction's work, done by its own part of the chip |
| **Throughput** | How many instructions finish per unit of time, on average. Pipelining raises this |
| **Latency** | How long one single instruction takes, start to finish. Pipelining does not shrink this |
| **Overlap** | Starting a new instruction before the previous one fully finishes |
| **Fetch (IF)** | The stage that gets the next instruction from memory |
| **Decode (ID)** | The stage that figures out what the instruction means and reads its values |
| **Execute (EX)** | The stage that does the math or comparison |
| **Memory (MEM)** | The stage that reads or writes data, if the instruction needs it |
| **Write Back (WB)** | The stage that saves the result where it belongs, usually a register |
| **Pipeline register** | A small holding spot between two stages, so one instruction's result does not get mixed up with another's |
| **Fill time** | The first few ticks, while the pipeline is still filling up with instructions |
| **Drain time** | The last few ticks, while the pipeline empties out, after the last instruction enters |
| **Speedup** | How many times faster a pipelined program finishes, compared to running the same program one instruction at a time |
| **Hazard** | A situation where overlapping instructions could produce a wrong answer. Not yet solved — that is Week 10 |
| **Stall** | Pausing a stage for one or more ticks, to avoid a wrong answer. A tool Week 10 introduces |

---

## 2. The Studio Pipeline, Worked Out Step by Step

This is the full version of the story from class. Read it slowly if the
in-class pace felt fast.

**The situation.** Week 7 left SmartPick's engineers with a multi-cycle
Studio chip that gives each instruction only the steps it needs, but
still finishes one instruction completely before starting the next. On
the same test program as Week 7 — 1,000 `add` instructions and 100 `lw`
(load word) instructions — the chip still runs one thing at a time,
tick after tick, with most of the chip idle at every moment.

**Step 1: Split every instruction into the same five stages.** Instead
of skipping stages a given instruction does not need (Week 7's trick),
pipelining gives every instruction the exact same five stages, one tick
each: **Fetch (IF), Decode (ID), Execute (EX), Memory (MEM), Write Back
(WB)**. Even an `add` instruction, which never touches memory, still
passes through the MEM stage — it just does nothing useful there.

**Step 2: Overlap instructions, one stage apart.** As soon as
instruction 1 leaves Fetch and moves to Decode, instruction 2 enters
Fetch. A new instruction can now start almost every single tick, instead
of waiting for the previous one to finish all five stages first.

**Step 3: Add small "trays" between stages.** A **pipeline register**
sits between each pair of stages, holding one instruction's partial
result steady until the next tick. Without it, a faster-moving
instruction could overwrite an in-progress one's data by mistake.

**Step 4: Compute the real speedup.** Assume each pipeline stage takes
100 ns, the same length as one of Week 7's short steps.

- **One at a time (Week 7's actual multi-cycle result):** 1,000 `add` × 4 steps × 100 ns + 100 `lw` × 5 steps × 100 ns = 400,000 ns + 50,000 ns = **450,000 ns**
- **Pipelined:** total ticks = stages + (instructions − 1) = 5 + 1,099 = 1,104 ticks × 100 ns = **110,400 ns**
- **Speedup:** 450,000 ÷ 110,400 ≈ **4.1x**, close to but under the "ideal" 5x, because the pipeline still pays a small fill-time cost, and because Week 7's multi-cycle version already saved some time by skipping steps

**Step 5: State clearly what we can, and cannot, say yet.** We *can* say
pipelining makes a new instruction start almost every tick, which is a
huge throughput gain. We *cannot* yet say every answer stays correct
while doing this — two overlapped instructions can now interfere with
each other. That fix, hazards and forwarding, is Week 10's job.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations that were trimmed from the slides
to keep class time short. Read it if you are curious or want more
examples.

**Why pipelining does not skip stages, but multi-cycle did.** Week 7's
multi-cycle design let `add` skip the Memory step entirely, saving real
time for that one instruction. Pipelining cannot do this: every
instruction must move through the pipeline in lockstep, one stage per
tick, or the overlap breaks down. So a pipelined `add` still occupies
the MEM stage for one tick, doing nothing there — the loss on any single
instruction is tiny compared to the throughput gained across the whole
program.

**An everyday version of the same idea.** Picture a coffee shop with
four separate stations: take the order, grind the beans, pull the shot,
add milk. One barista doing all four steps for one customer, start to
finish, before starting the next customer, is slow. Four baristas, one
per station, passing each cup down the line, can serve a new customer
almost every few seconds — even though any single cup still takes the
same four steps to make.

**Where this shows up around you.**

- **Every modern CPU:** phones, laptops, and servers all pipeline instructions; some pipelines have far more than five stages
- **GPUs:** graphics chips pipeline the steps of turning 3D data into pixels on your screen
- **Manufacturing:** the moving assembly line this idea was borrowed from is still how most cars and electronics are built today
- **Web servers:** a request pipeline (receive, parse, process, respond) overlaps many users' requests the same way

**Who actually designs this, as a job.**

- **Computer architects** decide how many pipeline stages a chip should have, balancing speed against complexity
- **Digital design engineers** build the actual pipeline registers and stage circuits from logic gates
- **Verification engineers** test that overlapped instructions still produce correct results, catching the exact bugs Week 10 studies
- **Performance engineers** measure real speedup on real programs, since it is rarely the "perfect" stage-count number

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** List the five stages of a classic pipeline, in order,
with their abbreviations.
> **Answer:** Fetch (IF), Decode (ID), Execute (EX), Memory (MEM), Write
> Back (WB).

**Problem 2.** A five-stage pipeline runs 10 instructions, with no
stalls. How many total ticks does the program take?
> **Answer:** 5 + (10 − 1) = **14 ticks**.

**Problem 3.** The same 10 instructions, run one at a time (no overlap,
5 ticks each), take how many total ticks? What is the speedup compared
to Problem 2's pipelined version?
> **Answer:** 10 × 5 = 50 ticks, one at a time. Speedup = 50 ÷ 14 ≈
> **3.6x**.

**Problem 4.** True or false: pipelining makes one single instruction
finish faster than it would running alone. Explain your answer in one
sentence.
> **Answer:** False. One instruction still passes through all five
> stages, so its own latency stays the same — only throughput, how many
> instructions finish per tick, improves.

**Problem 5.** An `add` instruction never needs to read or write data
memory. Does a pipelined `add` skip the Memory (MEM) stage, the way it
did in Week 7's multi-cycle design? Why or why not?
> **Answer:** No. In a pipeline, every instruction passes through every
> stage, one tick each, even if it does nothing useful there — skipping
> a stage would break the lockstep overlap with other instructions.

**Problem 6.** A 1,000-instruction program runs on a five-stage
pipeline, 100 ns per stage. Compute the total pipelined time.
> **Answer:** Total ticks = 5 + 999 = 1,004 ticks. Time = 1,004 × 100 ns
> = **100,400 ns**.
