---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 2: Performance & Cost

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Welcome back. Remind students: last week ended with a mystery we
could not solve with numbers. Today we solve it with numbers.
-->

---

<!-- SLOT 2: Where we are -->

# Where We Are

<div class="roadmap">
<div class="wk"><div class="n">Wk 1</div><div class="t">Introduction</div></div>
<div class="wk now"><div class="n">Wk 2</div><div class="t">Performance &amp; Cost</div></div>
<div class="wk"><div class="n">Wk 3</div><div class="t">Data Representation</div></div>
<div class="wk"><div class="n">Wk 4</div><div class="t">ISA I</div></div>
<div class="wk"><div class="n">Wk 5</div><div class="t">ISA II · Quiz 1</div></div>
<div class="wk"><div class="n">Wk 6</div><div class="t">Single-Cycle</div></div>
<div class="wk"><div class="n">Wk 7</div><div class="t">Multi-Cycle</div></div>
<div class="wk review"><div class="n">Wk 8</div><div class="t">Midterm Exam</div></div>
<div class="wk"><div class="n">Wk 9</div><div class="t">Pipelining I</div></div>
<div class="wk"><div class="n">Wk 10</div><div class="t">Pipelining II</div></div>
<div class="wk"><div class="n">Wk 11</div><div class="t">Memory Hierarchy I</div></div>
<div class="wk"><div class="n">Wk 12</div><div class="t">Memory Hierarchy II</div></div>
<div class="wk"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

<!--
notes: Point at Week 2. Say: last week gave us the map. This week gives
us a ruler.
-->

---

<!-- SLOT 3: Recap + open wound -->

# Last Week, This Week

- **Last week delivered:** the course contract, and the SmartPick mystery — two laptops, same spec sheet, one clearly slower in real use
- **Last week left broken:** we still do not know why the spec sheet did not tell the whole story

Today we build that number, step by step.

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **CPU time:** the actual time a processor spends running one program
- **Clock rate:** how many clock ticks happen per second, in GHz
- **Clock cycle time:** how long one clock tick takes, in seconds
- **Instruction count:** how many instructions a program actually runs
- **CPI (cycles per instruction):** the average number of clock cycles each instruction takes

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE) -->

# Still No Number

<div class="pain">

Week 1 left us with the SmartPick mystery: two laptops, same spec
sheet, one clearly slower in real use. But we still cannot put a
number on which machine is faster, or by how much. Knowing the mystery
exists is not the same as measuring it.

The SmartPick clerk still only has a stopwatch. Value: about 3 minutes
50 seconds. Studio: about 1 minute 25 seconds. He can repeat this test,
but he cannot explain the gap in numbers. He also cannot predict it for
a laptop he has never tested.

</div>

<!--
notes: Ask: "Could the clerk use this stopwatch method to help the NEXT
customer, with two different laptops?" Let students realize a stopwatch
alone does not generalize.
-->

---

<!-- SLOT 5: Cost of not knowing -->

# What This Actually Costs

- A shopper picks the wrong laptop because "faster" was only a guess, not a number
- An engineer cannot tell a manager how much an upgrade will really help
- A team buys cloud servers priced by the hour, with no way to compare real value for money
- A resume claim like "I made the system faster" means nothing without a measured number attached

<div class="why">
<strong>In industry:</strong> "how much faster, exactly, and is it worth
the price" is a daily engineering question. Companies that cannot answer
it waste real budget on hardware.
</div>

---

# Guessing Is Expensive, At Any Scale

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One shopper, wrong laptop</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 20%"></div></div>
  <div class="bar-value">a few hundred dollars, wasted</div>
</div>
<div class="bar-row">
  <div class="bar-label">One team, wrong cloud plan</div>
  <div class="bar-track"><div class="bar-fill risk-med" style="width: 55%"></div></div>
  <div class="bar-value">real monthly budget, wasted</div>
</div>
<div class="bar-row">
  <div class="bar-label">One company, wrong chip at scale</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 92%"></div></div>
  <div class="bar-value">millions of dollars a year</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

A number turns a guess into a decision you can defend.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"How do we turn 'faster' into an exact number we can compute, compare, and predict?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

1. Compute CPU time from instruction count, CPI, and clock rate
2. Explain why the same clock rate does not guarantee the same speed
3. Apply Amdahl's Law to predict the limit of a speedup
4. Compare two machines by performance per dollar, not price alone

---

<!-- SLOT 8: Origin -->

# This Problem Is Not New

<div class="thread">You just felt the pain. Now: who else felt it, and what did the field do?</div>

- **1964:** IBM launches the System/360 family — several different machines, one shared instruction set. Same idea as SmartPick's two laptops, sixty years earlier
- **1967:** Gene Amdahl, an IBM engineer, publishes a short paper. It proves a hard limit: speeding up only part of a machine can only help so much
- **1970s-80s:** makers advertise "MIPS" (millions of instructions per second). Different machines need different numbers of instructions for the same job, so MIPS could mislead

<div class="why">
Engineers nicknamed misleading MIPS numbers "Meaningless Indicator of
Processor Speed." The field needed a fair, agreed-on way to measure real
performance.
</div>

---

# Sixty Years of Chasing a Fair Number

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1964</div><div class="d">System/360<br>one ISA, many machines</div></div>
<div class="pt"><div class="dot"></div><div class="y">1967</div><div class="d">Amdahl's Law<br>a hard limit on partial speedups</div></div>
<div class="pt"><div class="dot"></div><div class="y">1988</div><div class="d">SPEC benchmarks founded<br>a fair, shared test suite</div></div>
<div class="pt"><div class="dot"></div><div class="y">Today</div><div class="d">CPU time, CPI, Amdahl's Law<br>still the core tools</div></div>
</div>

Every era needed the same thing: a number both sides could trust.

---

<!-- SLOT 9: Core concept -->

# CPU Time: Definition

<div class="thread">Sixty years of measuring point at one core formula. Here it is.</div>

> **CPU time** is the actual time a processor spends running one
> program: Instruction Count × CPI × Clock Cycle Time.

- **Instruction count:** how many instructions the program actually runs
- **CPI:** the average clock cycles each instruction takes
- **Clock cycle time:** how long one clock tick takes, in seconds

Three numbers, multiplied together, replace one stopwatch guess.

---

<!-- Act 3 / BUILD -->

# Clock Rate & Clock Cycle Time

<div class="thread">First factor: how fast the clock itself ticks.</div>

- **Clock rate**, in GHz, counts ticks per second. 3.0 GHz means 3 billion ticks every second
- **Clock cycle time** is the reverse: how long one tick takes. At 3.0 GHz, one tick takes about 0.33 nanoseconds
- For any one chip: clock cycle time = 1 / clock rate
- Clock rate is usually the biggest number on a spec sheet, which is exactly why shoppers trust it too much

A higher clock rate means a shorter cycle time, always. It says nothing about the other two factors yet.

---

# Instruction Count & CPI

<div class="thread">The other two factors: how much work, and how hard each step is.</div>

- **Instruction count:** how many instructions the program runs, for this task, on this machine
- **CPI:** on average, how many clock cycles each instruction takes to finish
- CPI is not fixed. A slower memory system makes the processor wait, so CPI goes up
- Same software, same ISA, can still produce a different CPI on a different microarchitecture

---

# Putting It Together: A Quick Example

<div class="thread">Same formula, small numbers, before we touch SmartPick.</div>

A small program runs **100 million instructions**. Average CPI is **2**.
Clock rate is **1 GHz**.

| Step | Value |
|---|---|
| Instruction count | 100,000,000 |
| CPI | 2 |
| Clock cycle time | 1 / 1 GHz = 1 nanosecond |
| **CPU time** | 100,000,000 × 2 × 1 ns = **0.2 seconds** |

Same three numbers, every time: count, CPI, cycle time.

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Coming Up Next: Worksheet Part A

Next session, you will work in pairs on
**[Worksheet Part A](materials/week02/worksheet.html)**.

- You will compute CPU time yourself, for two small fictional machines
- Same formula as this slide, different numbers
- We check your answers together at the start of 차시 3

<div class="why">
Bring a calculator or your phone's calculator. No laptop needed.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: is price the same as value?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **Cost-performance:** how much performance a machine gives you per dollar spent
- **Speedup:** how many times faster one machine or version is than another
- **Amdahl's Law:** a rule for the limit on speedup when only part of a task gets faster
- **Fraction improvable:** the share of the original time spent in the part you can actually speed up
- **Bottleneck:** the part of a task that limits how fast the whole task can go

---

# Cost-Performance: Price vs Performance

<div class="thread">Speed is only half the story. Price is the other half.</div>

- Price alone does not tell you if a purchase is a good deal
- **Cost-performance** compares how much performance you get for each dollar spent
- A machine that costs more can still be the better deal, if it is proportionally faster
- Compare a **price ratio** to a **speed ratio** between two machines to check
- Example: a machine costing 20% more but running 50% faster is the better deal, even though it costs more upfront

A cheaper machine is not automatically the smarter buy.

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week02/worksheet.html">Worksheet Part A</a></strong>. Compute CPU time for two
small machines, then compare their cost-performance. About 15 minutes.
</div>

- Show your steps: instruction count, CPI, clock cycle time
- Then compute performance per dollar for each machine
- We compare answers together next, in Part B

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work. Do not confirm final answers yet, the key is in Part B.
-->

---

# Amdahl's Law: Why One Fast Part Isn't Enough

<div class="thread">A natural question: why not just speed up the slow part and stop worrying?</div>

- Every task has parts. Some parts can be sped up. Some cannot
- Speeding up only the improvable part still leaves the other part exactly as slow
- The part you cannot speed up becomes the new **bottleneck** — it limits the total speedup
- This is true even if the improvable part becomes infinitely fast, which feels surprising the first time you see it

Making one part faster and faster still hits a ceiling.

---

# Amdahl's Law: The Formula

<div class="thread">The 1967 paper's limit, written as one formula.</div>

> **Amdahl's Law:** Overall speedup = 1 / ((1 − F) + F / S)

- **F:** the fraction of the original time spent in the part you speed up
- **S:** how many times faster that part becomes
- **(1 − F):** the rest of the task, which never gets faster

The untouched part, `1 − F`, is what caps how much you can gain.

---

# Amdahl's Law: Diminishing Returns

<div class="thread">What happens if S keeps growing, without limit?</div>

Half a task (F = 0.5) gets faster and faster. The other half never changes.

| Speedup of that half (S) | Overall speedup |
|---|---|
| 2x | 1.33x |
| 4x | 1.6x |
| 10x | 1.82x |
| infinitely fast | **2x, and no more** |

Even an infinitely fast upgrade to half a task only doubles it overall.

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: what does this mean for SmartPick's two laptops?</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **MIPS:** an old, often misleading speed number, millions of instructions per second
- **Benchmark suite (SPEC):** a shared, standard set of test programs used to measure real performance fairly
- **Local speedup vs. overall speedup:** how much faster one part got, versus how much faster the whole task got
- **Cost-effective:** giving good value for the money spent, not just being cheap

---

# Why MIPS Could Mislead

<div class="thread">A concrete reason the field dropped raw MIPS as the main measure.</div>

Machine X needs **5 instructions** to add two numbers. Machine Y needs
only **2 instructions** for the same job, a simpler, more direct ISA.

If both run **1,000 million instructions per second**, their MIPS number
looks identical. But Machine Y finishes the real addition task faster.
It needed fewer instructions to begin with.

<div class="why">
MIPS counts instructions, not work done. CPU time counts actual seconds,
which is what a shopper or a company really cares about.
</div>

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week02/worksheet.html">Worksheet Part B</a></strong>. Check your Part A
answers against the key, then apply Amdahl's Law to a new task. About 15
minutes.
</div>

- The answer key shows the full computation, step by step
- Part B also asks you to compute SmartPick's own numbers, before we reveal them

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). Let pairs self-check first. After ~15 minutes, cold-call 2-3
pairs before moving to the case study reveal.
-->

---

<!-- SLOT N-2: Worked example -->

# Case Study: SmartPick, Now With Real Numbers

<div class="thread">Same laptops as Week 1. This time, with the formula attached.</div>

| | Value | Studio |
|---|---|---|
| Clock rate | 3.0 GHz | 3.0 GHz |
| Instructions (export task) | 2 billion | 2 billion |
| CPI | 3 | 1 |
| **CPU time** | **2.0 sec** | **0.67 sec** |
| Price | $600 | $950 |

Same ISA, same clock rate, same instruction count. Studio's smaller CPI
— thanks to its bigger cache from last week — makes it **3x faster**.
Studio costs 58% more, but delivers about **1.9x more performance per
dollar** spent.

---

# Case Study: What If We Speed Up Just the Encoder?

<div class="thread">Amdahl's Law, applied to Value's own upgrade plan.</div>

Value's engineers speed up encoding, 80% of the run time, by **4x** with
a better codec. The remaining 20%, saving the file, cannot get faster.

**F = 0.8, S = 4.** Overall speedup = 1 / ((1 − 0.8) + 0.8 / 4) = 1 / 0.4
= **2.5x**, not 4x.

<div class="why">
Even an infinitely fast encoder caps the total speedup at 1 / (1 − 0.8) =
<strong>5x</strong>. The 20% you cannot touch always limits the result.
</div>

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"A 4x faster part means a 4x faster task":** wrong — the untouched part still takes its full time
- **"The cheaper machine is always the better deal":** compare performance per dollar, not price alone
- **"Same clock rate means same speed":** CPI and instruction count matter just as much as clock rate

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. A program runs 500 million instructions, average CPI 4, clock rate 2 GHz. What is its CPU time?
2. A task's slow part is 60% of the total time. You speed that part up 3x. What is the overall speedup?
3. Laptop A costs $500 and is half as fast as Laptop B, which costs $700. Which has better performance per dollar?

<div class="why">
After this, take the short <a href="materials/week02/quiz.html">self-check quiz</a> for more
practice. It is ungraded.
</div>

---

# Answers

1. CPU time = 500,000,000 × 4 × (1 / 2,000,000,000) = **1 second**
2. Speedup = 1 / ((1 − 0.6) + 0.6 / 3) = 1 / 0.6 ≈ **1.67x**
3. **Laptop B.** It is 2x the speed for 1.4x the price, so about **1.43x** more performance per dollar

---

<!-- SLOT N+1: Limits (Act 4 / CLOSE), becomes Week 3 slot 4 -->

# What This Week's Tools Cannot Do Yet

<div class="limits">
We can measure speed precisely, but not yet how a number becomes a bit
pattern the ALU can act on.
</div>

---

<!-- SLOT N+2: Bridge -->

# Next Week

Week 2 leaves **how a number becomes a bit pattern** unsolved. **Week 3,
Data Representation**, addresses it. It shows exactly how numbers and
letters become 0s and 1s a processor can act on.

---

<!-- SLOT N+3: Summary -->

# Summary

- CPU time = Instruction Count × CPI × Clock Cycle Time — this week's core formula
- Same clock rate does not guarantee the same speed; CPI and instruction count matter too
- Amdahl's Law: speeding up part of a task caps the overall speedup; the untouched part becomes the bottleneck
- Compare machines by performance per dollar, not price alone
- **You did today:** Worksheet Parts A and B, self-check quiz
- **Reading:** Hennessy & Patterson, 6th ed., Chapter 1, Performance and Amdahl's Law sections
- **Handout:** [materials/week02/handout.md](materials/week02/handout.html), glossary and the full worked example
- **Prepare:** bring one number from a real spec sheet you want to compute performance for

---

<!-- SLOT N+4: Thank You -->
<!-- _class: end -->

# Thank You
