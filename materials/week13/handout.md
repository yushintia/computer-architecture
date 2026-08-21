# Week 13 Handout: Parallelism

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester, and again in Week 14's presentations.

| Term | Plain definition |
|---|---|
| **Core** | One independent processing unit inside a chip |
| **Multicore** | A chip built with more than one core |
| **Thread** | One independent stream of instructions a core can run |
| **Parallelism** | Doing more than one piece of work at the same time, instead of one after another |
| **Serial** | Doing work one step after another; the opposite of parallel |
| **Task-level parallelism** | Different workers doing different jobs at the same time |
| **Data-level parallelism** | Every worker repeating the same operation on a different piece of data |
| **SIMD** | "Single Instruction, Multiple Data" — one instruction applied to many data items in one step |
| **GPU** | A chip built from thousands of small, simple cores, well suited to SIMD-style work |
| **Distributed computing** | Many separate computers, connected by a network, cooperating on one job |
| **Speedup** | How many times faster a task runs with more workers, compared to one worker |
| **Serial fraction (S)** | The share of a task that must happen one step at a time, no matter how many workers are used |
| **Parallel fraction (P)** | The share of a task that can be split across workers. S + P = 1 for one task |
| **Synchronization** | Workers pausing to wait for each other, or to share results, before continuing |
| **Coordination overhead** | Extra time workers spend communicating or waiting, instead of computing |
| **Scalability** | How well a task keeps speeding up as more workers are added |
| **Flynn's Taxonomy** | A 1966 way of sorting computer designs by how many instruction and data streams they handle at once |

---

## 2. The Studio Pro Story, Worked Out Step by Step

This is the full version of the story from class. Read it slowly if the
in-class pace felt fast.

**The situation.** The SmartPick customer from Week 1 loved her Studio
laptop. A friend finds a newer listing, "Studio Pro," advertised with 16
cores instead of Studio's 8. The seller claims "twice the cores, twice
the speed." The friend buys it, expecting the same video export task to
take about half as long: roughly 42 seconds, down from Studio's 1 minute
25 seconds.

**The real result.** Studio Pro finishes the export in about **1 minute
10 seconds**. Faster, yes — but nowhere near half the time.

**Step 1: Split the task into two parts.** Every task like this has a
**serial** part (must happen one step at a time, such as writing the
final combined video file) and a **parallel** part (can be split across
many cores at once, such as encoding each frame's video data).

**Step 2: Estimate the split for this task.** For Studio's video export,
about **20% is serial** (S = 0.2) and **80% is parallel** (P = 0.8).

**Step 3: Apply the speedup formula.**

> **Speedup(N) = 1 / (S + P / N)**

| Cores (N) | S + P/N | Speedup | Export time |
|---|---|---|---|
| 1 | 0.2 + 0.8 = 1.0 | 1.0x | ~4 min 43 sec |
| 8 | 0.2 + 0.1 = 0.3 | ~3.3x | ~1 min 25 sec |
| 16 | 0.2 + 0.05 = 0.25 | 4.0x | ~1 min 10 sec |

**Step 4: Read what the table says.** Going from 1 core to 8 cores buys
a large jump: 3.3x faster. Going from 8 cores to 16 cores only buys
another 0.7x: the 20% serial part takes the same 57 seconds either way,
and it does not get any smaller no matter how many cores help with the
other 80%. That fixed 57 seconds is why doubling the cores did not come
close to halving the time.

**Step 5: State clearly what we can, and cannot, say yet.** We *can* now
say, correctly: Studio Pro is faster because it has more cores for the
80% parallel part, but its speedup is capped by the fixed 20% serial
part. We *cannot* yet point at Studio Pro's actual circuit and show
exactly how its 16 cores coordinate — that concrete, real-design view is
what Week 14's presentations bring.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations that were trimmed from the slides
to keep class time short. Read it if you are curious or want more
examples.

**Why the formula assumes "perfect" splitting, and reality does not.**
The speedup formula (Speedup = 1 / (S + P/N)) assumes the parallel part
splits perfectly evenly across N workers, with no extra cost. Real
machines pay a coordination cost too: workers must occasionally
communicate, wait for the slowest worker, or keep shared data in sync
(recall caches from Weeks 11-12: two cores sharing data must stay
consistent). That is why real speedup is often a little lower than the
formula predicts, especially as N grows large.

**A second, everyday version of the same idea.** Imagine 16 painters
tasked with painting one long fence and then signing it together at the
end. Adding more painters speeds up the painting part a lot. But only
one signature can go on the fence at a time, and everyone must wait for
each other to finish painting before signing starts. No matter how many
painters you hire, the signing step takes the same fixed time. The
painting is the parallel part; the single, orderly signature is the
serial part.

**Where this shows up around you.**

- **Smartphone chips:** a handful of cores, tuned for both single-thread speed and battery-friendly parallel work
- **Gaming GPUs:** thousands of simple cores, built from the ground up for data-level parallelism
- **AI training clusters:** thousands of GPUs across many machines, using both multicore and distributed computing together
- **Cloud servers:** rented by the core, so companies pay directly for how well their software actually uses parallelism
- **Video game engines:** split physics, rendering, and audio across different cores as task-level parallelism

**Who actually designs this, as a job.**

- **Computer architects** decide how many cores a chip should have and how they share memory — this course's core focus
- **Parallel / systems programmers** write software that actually splits work correctly across cores or machines
- **GPU / AI infrastructure engineers** design and tune hardware and software for data-level, SIMD-style work at scale
- **Site reliability / cloud engineers** decide how many machines a distributed job actually needs, balancing speed against cost

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** A task is 100% parallel (S = 0, P = 1). What is its
speedup on 4 workers, using the formula?
> **Answer:** Speedup = 1 / (0 + 1/4) = 1 / 0.25 = **4x**, a perfect,
> proportional speedup.

**Problem 2.** A task is 100% serial (S = 1, P = 0). What is its
speedup on 8 workers?
> **Answer:** Speedup = 1 / (1 + 0) = **1x**. Extra workers do not help
> at all if nothing can be split up.

**Problem 3.** A task is 10% serial and 90% parallel. What is its
speedup on 4 workers?
> **Answer:** Speedup = 1 / (0.1 + 0.9/4) = 1 / 0.325 ≈ **3.1x**.

**Problem 4.** Using the same task as Problem 3 (S = 0.1, P = 0.9), what
is its speedup on 16 workers? Compare it to your answer for 4 workers.
> **Answer:** Speedup = 1 / (0.1 + 0.9/16) = 1 / 0.15625 ≈ **6.4x**.
> Going from 4 to 16 workers (4x more workers) only doubles the speedup,
> because the 10% serial part increasingly dominates.

**Problem 5.** Name one task that fits data-level parallelism well, and
explain why in one sentence.
> **Answer (example):** Brightening every pixel in a photo, because the
> exact same operation repeats on many independent pieces of data.

**Problem 6.** A friend says: "I bought a 32-core server, so my program
should run 32 times faster than on 1 core." What is missing from their
reasoning?
> **Answer:** They ignored the task's serial fraction. Unless the task is
> 100% parallel, the serial part caps the speedup below 32x, no matter
> how many cores are added.
