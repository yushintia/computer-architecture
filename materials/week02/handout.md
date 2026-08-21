# Week 2 Handout: Performance & Cost

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **CPU time** | The actual time a processor spends running one program |
| **Clock rate** | How many clock ticks happen per second, measured in GHz |
| **Clock cycle time** | How long one clock tick takes, in seconds. Equals 1 / clock rate |
| **Instruction count** | How many instructions a program actually runs, for one task, on one machine |
| **CPI (cycles per instruction)** | The average number of clock cycles each instruction takes to finish |
| **Speedup** | How many times faster one machine or version is, compared to another |
| **Amdahl's Law** | A rule that caps the overall speedup you can get when only part of a task gets faster |
| **Fraction improvable (F)** | The share of the original time spent in the part you can actually speed up |
| **Bottleneck** | The part of a task that limits how fast the whole task can go |
| **Cost-performance** | How much performance a machine gives you for each dollar spent |
| **Price ratio** | How many times more expensive one machine is than another |
| **MIPS** | Millions of instructions per second — an old speed measure that can mislead |
| **Benchmark suite (SPEC)** | A shared, standard set of test programs used to measure real performance fairly |
| **Local speedup vs. overall speedup** | How much faster one part got, versus how much faster the whole task got |
| **Cost-effective** | Giving good value for the money spent, not just being cheap |

---

## 2. The SmartPick Story, Worked Out Step by Step

This is the full version of the worked example from class. Read it
slowly if the in-class pace felt fast.

**Where we left off.** Last week, the SmartPick clerk had only a
stopwatch: Value finished a video export in about 3 minutes 50 seconds,
Studio in about 1 minute 25 seconds. He knew the two laptops shared an
ISA but had different microarchitectures. He could not explain the gap
with a number.

**Step 1: Attach the formula.** CPU time = Instruction Count × CPI ×
Clock Cycle Time. This week's numbers for the export task, kept simple
for teaching:

| | Value laptop | Studio laptop |
|---|---|---|
| Clock rate | 3.0 GHz | 3.0 GHz |
| Instruction count (export task) | 2 billion | 2 billion |
| CPI | 3 | 1 |
| Clock cycle time | 1 / 3.0 GHz ≈ 0.33 ns | 1 / 3.0 GHz ≈ 0.33 ns |
| **CPU time** | 2 billion × 3 × 0.33 ns ≈ **2.0 sec** | 2 billion × 1 × 0.33 ns ≈ **0.67 sec** |

**Step 2: Read what stayed the same, and what changed.** Clock rate and
instruction count are identical — same ISA, same task, same clock speed.
Only CPI changed: 3 for Value, 1 for Studio. That single number carries
the entire gap.

**Step 3: Connect CPI back to last week's cache observation.** Studio's
24 MB cache (versus Value's 8 MB) means fewer slow trips to main memory.
Fewer stalls means a lower average CPI. This is *why* Studio's CPI is
lower, not just a coincidence.

**Step 4: Compute the speedup.** Speedup = CPU time of Value / CPU time
of Studio = 2.0 / 0.67 ≈ **3x**. Studio finishes the export about three
times faster.

**Step 5: Check the price against the speed — cost-performance.** Studio
costs $950, Value costs $600. Price ratio = 950 / 600 ≈ 1.58 (58% more
expensive). Speed ratio = 3.0 (3x faster). Performance per dollar ratio =
speed ratio / price ratio = 3.0 / 1.58 ≈ **1.9**. Studio gives about 1.9x
more performance per dollar, even though it costs more upfront.

**Step 6: Apply Amdahl's Law to a real upgrade question.** Suppose
Value's engineers install a better codec that speeds up encoding — 80%
of the export's run time — by 4x. Saving the file, the other 20%, cannot
get faster.

- F = 0.8 (the improvable fraction)
- S = 4 (how much faster that fraction becomes)
- Overall speedup = 1 / ((1 − F) + F / S) = 1 / (0.2 + 0.2) = 1 / 0.4 = **2.5x**

Even a 4x faster encoder only makes the whole export 2.5x faster, not
4x. The untouched 20% is the bottleneck. Even an infinitely fast encoder
could only reach 1 / (1 − 0.8) = **5x**, never more.

**Step 7: State clearly what we can, and cannot, say yet.** We *can* now
say exactly how much faster Studio is (3x), why (lower CPI, from a
bigger cache), and whether it is the better deal (yes, about 1.9x more
performance per dollar). We *cannot* yet say what bit pattern the
processor actually works on when it runs one instruction. That is
Week 3's job.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations trimmed from the slides to keep
class time short. Read it if you are curious or want more examples.

**Why CPI can be less than 1.** Modern processors can start more than
one instruction in the same clock cycle. When that happens, average CPI
can drop below 1 — sometimes called IPC (instructions per cycle) instead.
This course keeps CPI ≥ 1 in examples to stay simple, but real chips
often push CPI below 1.

**Amdahl's Law shows up everywhere, not just in CPUs.** A delivery
company that makes its trucks 4x faster, but whose warehouse loading
still takes the same fixed time, will not see 4x faster deliveries
overall. The fixed step becomes the new bottleneck. Anywhere a process
has a part that cannot shrink, Amdahl's Law applies.

**A second reason MIPS could mislead.** Two machines can also disagree
on how "complex" one instruction is. A single instruction on one ISA
might do the work of three instructions on another. Comparing MIPS
directly, without checking instruction count, hides this difference
completely.

**Where this shows up around you.**

- **Cloud computing:** providers publish "instance types" priced by
  performance and cost together, exactly like Studio vs. Value
- **Game consoles:** marketing often quotes teraflops (a raw speed
  number), but real game performance depends on the whole system, not
  one number
- **Mobile chips:** battery life adds a third axis besides speed and
  price, but the same cost-performance thinking still applies
- **Data center procurement:** buyers run standard benchmarks (like
  SPEC) before choosing a chip, precisely to avoid a MIPS-style mistake

**Who actually uses this, as a job.**

- **Performance engineers** measure CPU time and CPI on real workloads to
  find bottlenecks
- **Procurement / infrastructure engineers** use cost-performance
  analysis to choose hardware at scale
- **Compiler engineers** try to lower instruction count and CPI together,
  for the same ISA
- **Computer architects** design microarchitectures aiming for lower CPI
  at a given clock rate and cost

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** A program runs 300 million instructions. Average CPI is
2. Clock rate is 1.5 GHz. What is its CPU time?
> **Answer:** CPU time = 300,000,000 × 2 × (1 / 1,500,000,000) = **0.4
> seconds**.

**Problem 2.** Machine A has a clock rate of 4.0 GHz and CPI of 2 for a
task. Machine B has a clock rate of 2.0 GHz and CPI of 0.5 for the same
task, with the same instruction count. Which machine has the lower CPU
time?
> **Answer:** Machine A's cycle time is 1/4 GHz, effective time factor =
> 2 × (1/4) = 0.5. Machine B's factor = 0.5 × (1/2) = 0.25. **Machine B**
> has the lower CPU time, despite the lower clock rate.

**Problem 3.** A task is 40% a part you can speed up. You make that part
5x faster. What is the overall speedup, using Amdahl's Law?
> **Answer:** Speedup = 1 / ((1 − 0.4) + 0.4/5) = 1 / (0.6 + 0.08) = 1 /
> 0.68 ≈ **1.47x**.

**Problem 4.** Using the same task as Problem 3, what is the maximum
possible speedup, even with an infinitely fast improvement to that 40%?
> **Answer:** Maximum speedup = 1 / (1 − 0.4) = 1 / 0.6 ≈ **1.67x**.

**Problem 5.** Laptop C costs $400 and is one-third as fast as Laptop D,
which costs $650. Which laptop has better performance per dollar?
> **Answer:** Price ratio (D/C) = 650/400 = 1.625. Speed ratio (D/C) = 3.
> Performance-per-dollar ratio = 3 / 1.625 ≈ 1.85. **Laptop D** gives
> about 1.85x more performance per dollar, despite costing more.

**Problem 6.** Explain in one sentence why two machines with the exact
same MIPS number can still finish the same real task in different
amounts of time.
> **Answer (example):** MIPS only counts instructions per second, not
> how many instructions the task actually needs, so a machine that needs
> fewer instructions for the same job can still finish faster.
