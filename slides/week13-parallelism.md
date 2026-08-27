---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 13: Parallelism · Quiz 2

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Welcome the class. Remind them Quiz 2 is today, near the end of
class, closed-book, covering Weeks 9-13. Keep the tone calm, not
stressful — the quiz is short and this is still a normal teaching day.
-->

---

<!-- SLOT 2: Where we are -->

# Where We Are

<div class="roadmap">
<div class="wk"><div class="n">Wk 1</div><div class="t">Introduction</div></div>
<div class="wk"><div class="n">Wk 2</div><div class="t">Performance &amp; Cost</div></div>
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
<div class="wk now"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

<!--
notes: Point at Week 13. Say: we have built one core's whole story —
instructions, a datapath, pipelining, caches, virtual memory. Today we
finally ask what happens when a chip has more than one core.
-->

---

<!-- SLOT 3: Recap + open wound -->

# Last Week, This Week

- **Last week delivered:** virtual memory, so every program gets its own large, private memory space, no matter the laptop's real RAM size
- **Last week left broken:** virtual memory solves capacity, but a single core is still the whole story

Today we open that story up: what happens once a chip has more than one core?

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **Core:** one independent processing unit inside a chip
- **Multicore:** a chip built with more than one core
- **Thread:** one stream of instructions a core can run
- **Parallelism:** doing more than one piece of work at the same time
- **Serial:** doing work one step after another, not at the same time

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), zero jargon -->

# Double the Cores, Not Double the Speed

<div class="pain">

The SmartPick customer from Week 1 is back. She loved her Studio laptop,
so she tells a friend about it. The friend finds a newer listing,
"Studio Pro," with 16 cores instead of Studio's 8. The seller says:
"twice the cores means twice the speed."

The friend buys it and times the same video export Week 1 used. Studio
took about 1 minute 25 seconds. She expects Studio Pro to take about 42
seconds, half that. Instead, it takes about 1 minute 10 seconds. Barely
faster. She calls SmartPick, confused: "You said double. Why is it
barely faster?"

</div>

<!--
notes: Let the confusion sit. Ask: "Any guesses why doubling the cores
did not halve the time?" Take a few guesses, do not confirm or deny any
of them yet.
-->

---

# The Extra Cores Barely Moved the Needle

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">Studio, 8 cores</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">~1 min 25 sec</div>
</div>
<div class="bar-row">
  <div class="bar-label">Studio Pro, 16 cores</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 83%"></div></div>
  <div class="bar-value">~1 min 10 sec</div>
</div>
</div>

Double the cores. Only about 17% faster, not 50% faster. Something in
this task refuses to split across cores.

<!-- notes: Let this gap sit for a moment before moving on. -->

---

<!-- SLOT 5: Cost of not knowing -->

# What Else This Actually Costs

- A shopper pays extra for more cores, expecting proportionally faster programs, and feels cheated when it barely helps
- A student writes a program meant to "use all the cores." It barely speeds up, and they do not know why
- A company rents a huge multi-core cloud server for a task that cannot be split up. Most of it sits unused

<div class="why">
<strong>In industry:</strong> "why doesn't this scale with more cores or
more machines" is a classic interview and real job question. Cloud
providers bill per core, so wasted cores are wasted money, every month.
</div>

---

# The Same Mistake, at Every Scale

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One student's laptop</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 20%"></div></div>
  <div class="bar-value">a slower program than expected</div>
</div>
<div class="bar-row">
  <div class="bar-label">One startup's cloud bill</div>
  <div class="bar-track"><div class="bar-fill risk-med" style="width: 55%"></div></div>
  <div class="bar-value">paying for cores that sit idle</div>
</div>
<div class="bar-row">
  <div class="bar-label">One company's data center</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 92%"></div></div>
  <div class="bar-value">huge wasted hardware budget</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

Not knowing where parallelism helps costs you, at whatever scale you work.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"How can one task actually use many cores at once — and what stops it from using all of them?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

<div class="cardlist">
<div class="card"><div class="h">Kinds of Parallelism</div><div class="d">Name the main kinds of parallelism used in real chips today</div></div>
<div class="card"><div class="h">Diminishing Returns</div><div class="d">Explain why adding more cores does not always mean proportionally faster</div></div>
<div class="card"><div class="h">Expected Speedup</div><div class="d">Compute a task's expected speedup from its serial and parallel parts</div></div>
<div class="card"><div class="h">Splittable Work</div><div class="d">Identify which parts of a real task can, and cannot, be split across workers</div></div>
</div>

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Coming Up Next: Worksheet Part A

Next session, you will work in pairs on
**[Worksheet Part A](materials/week13/worksheet.html)**.

- You will see a task split into a "must happen in order" part and a "can be split up" part
- Your pair predicts how much faster more cores actually make it
- Then we check your prediction against the real numbers together

<div class="why">
Bring your notebook and a calculator (or your phone's calculator). No
laptop needed.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: where did the idea of parallelism come from?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **SIMD:** one instruction applied to many pieces of data at once
- **GPU:** a chip built from thousands of small cores, suited to SIMD-style work
- **Data-level parallelism:** repeating the same operation on many data items at once
- **Task-level parallelism:** different workers doing different jobs at once
- **Distributed computing:** many separate computers cooperating over a network on one job

---

<!-- SLOT 8: Origin -->

# This Problem Is Not New

<div class="thread">You just felt the pain. Now: who else felt it, and what did the field do?</div>

<div class="cardlist">
<div class="card"><div class="h">1966</div><div class="d">Michael Flynn sorts computer designs by how many instruction and data streams they handle at once</div></div>
<div class="card"><div class="h">~2004</div><div class="d">chip speed hits the power wall (Week 1). Chipmakers stop chasing one faster core and start shipping two, four, then many cores per chip</div></div>
<div class="card"><div class="h">2004</div><div class="d">Google publishes MapReduce, showing thousands of ordinary machines can cooperate on one huge job</div></div>
<div class="card"><div class="h">2007</div><div class="d">NVIDIA opens GPUs, built for repetitive graphics math, to general-purpose programs</div></div>
</div>

<div class="why">
Four different moments, one shared answer: if one worker cannot go
faster, use more workers instead.
</div>

---

# Four Answers to the Same Wall

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1966</div><div class="d">Flynn's Taxonomy<br>a map of parallel designs</div></div>
<div class="pt"><div class="dot"></div><div class="y">2004</div><div class="d">MapReduce<br>many machines, one job</div></div>
<div class="pt"><div class="dot"></div><div class="y">~2004-05</div><div class="d">Multicore chips<br>more cores, not more GHz</div></div>
<div class="pt"><div class="dot"></div><div class="y">2007</div><div class="d">GPUs go general-purpose<br>thousands of small cores</div></div>
</div>

Every era asked: if one worker is maxed out, how do we add more workers
correctly?

---

<!-- SLOT 9: Core concept -->

# Parallelism: Definition

<div class="thread">Four historical answers point at one clear idea. Here it is.</div>

> **Parallelism** means splitting one piece of work into pieces that run
> at the same time, on more than one worker, instead of one after
> another.

- **Task-level parallelism:** different workers do different jobs at once (one core plays audio, another decodes video)
- **Data-level parallelism:** every worker repeats the same operation on a different piece of data (brightening every pixel in a photo)

Studio Pro's 16 cores are workers. The question is how much of the video
export they can actually share.

---

<!-- Act 3 / BUILD -->

# Where Parallelism Lives in a Real Machine

<div class="thread">One definition, three places engineers actually put it to work.</div>

<div class="appgrid">
<div class="app"><div class="name">Multicore</div><div class="desc">Several full cores on one chip. The OS splits a program into threads and hands one to each core</div></div>
<div class="app"><div class="name">SIMD / GPU</div><div class="desc">One instruction repeated across thousands of small cores, for data-level work like graphics or AI</div></div>
<div class="app"><div class="name">Distributed</div><div class="desc">Many separate machines, connected by network, splitting one very large job</div></div>
</div>

Studio Pro uses the first one: multicore.

---

# Multicore & Threads

- A program's work is split into **threads**: independent streams of instructions
- The operating system hands each thread to a free core to run
- More threads run truly at once only if the program has enough independent pieces of work to hand out

If a program has only one thread, extra cores simply sit idle, no matter
how many the chip has.

---

# Data-Level Parallelism: SIMD & GPUs

- **SIMD** means: one instruction, applied to many data items, in one step
- A **GPU** is built from thousands of small, simple cores, each good at one repeated operation
- This fits work like brightening every pixel of a photo, or updating millions of numbers in an AI model

GPUs are fast at this exact pattern, and much slower at tasks that need
one careful step after another.

---

# Distributed Computing: Many Whole Machines

- When one chip is not enough, split the job across many separate computers connected by a network
- Each machine works on its own piece, then the pieces are combined
- Used for training large AI models, web-scale search, and huge scientific simulations

The idea is the same as multicore, just at building scale instead of
chip scale.

---

# The Catch: Not Every Task Splits Evenly

<div class="thread">Three ways to add workers. Now: why did Studio Pro barely help?</div>

Some steps in a task **must** happen in order, no matter how many workers
you have. Combining every worker's piece into one final file only starts
once every worker is done.

That "must happen in order" part is called the **serial** part of a task.
The rest, which can be split across workers, is the **parallel** part.

---

# Speedup: A Formula for the Catch

<div class="thread">Serial and parallel parts, turned into one usable number.</div>

For a task with serial fraction **S** and parallel fraction **P**
(S + P = 1), running on **N** workers:

> **Speedup = 1 / (S + P / N)**

- More workers (bigger N) only shrink the parallel part's time
- The serial part's time never shrinks, no matter how big N gets
- That serial part is what caps how much extra cores can ever help

---

<!-- SLOT N-2: Worked example -->

# Case Study: Studio Pro's 16 Cores, Explained

<div class="thread">Same running example, now with the formula from the last slide.</div>

Studio's video export is about **20% serial** (S = 0.2) and **80%
parallel** (P = 0.8):

| Cores (N) | Speedup = 1 / (S + P/N) | Export time |
|---|---|---|
| 1 | 1.0x | ~4 min 43 sec |
| 8 | ~3.3x | ~1 min 25 sec |
| 16 | 4.0x | ~1 min 10 sec |

Doubling cores from 8 to 16 barely changed the time: the 20% serial part
takes the same 57 seconds either way, and it dominates.

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week13/worksheet.html">Worksheet Part A</a></strong>. You will get a new task's
serial and parallel fractions and predict its speedup on different core
counts. About 15 minutes.
</div>

- Use the formula: Speedup = 1 / (S + P/N)
- It is OK to be unsure of the arithmetic, write down your reasoning too
- We check your numbers together at the start of 차시 3

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work through the formula. Do not confirm final answers yet, the reveal
happens next session with Part B.
-->

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: your Worksheet Part A answers, then Quiz 2.</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **Speedup:** how many times faster a task runs with more workers, versus one worker
- **Synchronization:** workers pausing to wait for each other or share results
- **Coordination overhead:** the extra time workers spend communicating instead of working
- **Scalability:** how well a task keeps speeding up as workers are added

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week13/worksheet.html">Worksheet Part B</a></strong>. Check your Part A
prediction against the real answer, then answer two new questions. About
15 minutes.
</div>

- The answer key shows the full formula worked out, step by step
- Notice how little extra speed the last few cores actually buy

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). Let pairs self-check. After ~15 minutes, cold-call 1-2 pairs
to share their reasoning before moving on to common mistakes.
-->

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"More cores always means faster":** ignores the serial part. The formula shows it caps total speedup
- **"Splitting work is free":** real workers must communicate and share results, which costs real time
- **"GPUs are always the answer":** they excel at data-level work, but gain little on tasks that need one careful step after another

---

# The Hidden Cost: Coordination

Workers do not just compute, they also **synchronize**: pausing to wait
for each other or to share partial results.

- Combining 16 workers' pieces takes longer to coordinate than combining 8 workers' pieces
- Two cores sharing the same cache line (Week 11-12) must stay in sync, which also costs time
- Past a point, adding more workers can add more coordination cost than it saves in compute time

---

<!-- NEW: Quiz 2 logistics, near end of 차시 3, before self-check hand-off -->

# Quiz 2 Today

Right after this section: Quiz 2, closed-book, covering Weeks 9-13,
about 15 minutes.

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. A task is 25% serial and 75% parallel. About how much faster is it on 4 workers than on 1?
2. Name one task that benefits from a GPU's data-level parallelism, and one that does not
3. True or false: doubling the number of cores always doubles a program's speed

<div class="why">
After Quiz 2, take the short <a href="materials/week13/quiz.html">self-check quiz</a> for more
practice. It is ungraded.
</div>

---

# Answers

1. Speedup = 1 / (0.25 + 0.75/4) = 1 / 0.4375 ≈ **2.3x faster**, not 4x
2. Brightening every pixel of a photo benefits; deciding step-by-step game logic that depends on the last step does not
3. **False** — the serial part limits how much extra cores can help (the speedup formula)

---

<!-- SLOT 14: Limits (Act 4 / CLOSE), becomes Week 14 slot 4 -->

# What Today's Techniques Cannot Do Yet

<div class="limits">
We can now name parallel techniques, but not yet see them working in a
real, current design. Knowing multicore, SIMD, and distributed computing
by name is not the same as watching one real chip use them.
</div>

---

<!-- SLOT 15: Bridge -->

# Next Week

Week 13 leaves **seeing these techniques inside one real, current
processor design** unsolved. **Week 14, Presentation**, addresses it:
you present a real design and connect it to everything from this
semester.

---

<!-- SLOT 16: Summary -->

# Summary

- Parallelism splits work across multiple workers: cores, GPUs, or distributed machines
- Speedup is capped by a task's serial fraction, so more workers help less and less
- Coordination between workers has a real cost, not only a benefit
- **You did today:** Worksheet Parts A and B, Quiz 2, self-check quiz
- **Reading:** Hennessy & Patterson, 6th ed., Chapter 5, Thread-Level Parallelism
- **Handout:** [materials/week13/handout.md](materials/week13/handout.html), glossary and the full Studio Pro walkthrough
- **Prepare:** find one real device's core count (phone, laptop, or console). Bring it for Week 14

---

<!-- SLOT 17: Thank You -->
<!-- _class: end -->

# Thank You
