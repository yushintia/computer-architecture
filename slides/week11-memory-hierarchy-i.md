---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 11: Memory Hierarchy I

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

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
<div class="wk now"><div class="n">Wk 11</div><div class="t">Memory Hierarchy I</div></div>
<div class="wk"><div class="n">Wk 12</div><div class="t">Memory Hierarchy II</div></div>
<div class="wk"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

---

<!-- SLOT 3: Recap + open wound -->

# Last Week, This Week

- **Last week delivered:** Pipelining II fixed hazards. A pipelined processor now gives correct answers every time, even while instructions overlap
- **Last week left broken:** Hazards are handled, but every pipeline still waits on a slow memory system

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **Memory:** where a running program's instructions and data are stored
- **Cache:** a small, very fast memory placed close to the processor
- **Cache hit:** the processor asks for data and finds it already in the cache
- **Cache miss:** the processor asks for data and it is not in the cache yet
- **Latency:** how long one single request takes to get an answer

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), zero jargon -->

# A Perfect Assembly Line, Still Waiting

<div class="pain">

SmartPick's repair team finally fixes the Studio laptop's assembly line
inside the chip. Every step now runs in the right order, every time. No
more wrong answers, ever.

A customer opens a huge photo album on the fixed laptop and scrolls
through her photos. The screen still freezes for a moment, again and
again. The assembly line inside the chip is not the problem this time.
Something else is making her wait.

</div>

<!--
notes: Do not say "memory" or "cache" yet. Let the class sit with the
confusion. Ask: "The pipeline is fixed. Why does it still freeze?" Take
a few guesses without confirming any of them.
-->

---

# The Chip Is Fast. Something Else Is Slow

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One step inside the chip</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 15%"></div></div>
  <div class="bar-value">a tiny fraction of a second</div>
</div>
<div class="bar-row">
  <div class="bar-label">One trip to fetch data from memory</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">roughly 100 times slower</div>
</div>
</div>

Every single step waits on this gap, even after the pipeline is fixed.

---

<!-- SLOT 5: Cost of not knowing -->

# What This Actually Costs

- A photo or video app freezes constantly, even on a chip that runs its steps perfectly
- A company buys an expensive new processor, but the program stays slow. Memory was the real bottleneck all along

<div class="why">
<strong>In industry:</strong> "why is this slow, even on fast hardware"
is a common debugging and interview question. Cloud providers charge
extra for machines with more cache and faster memory, because it
changes real speed directly.
</div>

---

# Waiting Adds Up, at Every Scale

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One frozen photo scroll</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 20%"></div></div>
  <div class="bar-value">a few seconds lost</div>
</div>
<div class="bar-row">
  <div class="bar-label">One slow database query</div>
  <div class="bar-track"><div class="bar-fill risk-med" style="width: 55%"></div></div>
  <div class="bar-value">users leave the page</div>
</div>
<div class="bar-row">
  <div class="bar-label">One datacenter, wrong memory design</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 92%"></div></div>
  <div class="bar-value">millions of dollars a year</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

The same gap, at three different sizes. Memory speed is not a small detail.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"How do we keep a fast processor fed with data, without paying for memory that is both huge and fast?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

1. Explain why memory speed limits real performance, even with a perfect pipeline
2. Describe the memory hierarchy and why it is built in layers
3. Explain how a cache decides between a hit and a miss
4. Compute a simple average memory access time (AMAT)

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Coming Up Next: Worksheet Part A

Next session, you will work in pairs on
**[Worksheet Part A](materials/week11/worksheet.html)**.

- You will see two cache sizes from SmartPick's laptops
- Your pair predicts which one causes fewer slow waits, and why
- We compare answers together at the start of 차시 3

<div class="why">
Bring your notebook. No laptop or calculator needed yet.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: where did this idea come from?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **Memory hierarchy:** several layers of storage, from small and fast to huge and slow
- **Main memory (RAM):** the computer's main working storage, bigger than cache but slower
- **Locality:** the tendency of a program to reuse the same or nearby data soon
- **Hit rate:** the share of memory requests a cache can answer by itself

---

<!-- SLOT 8: Origin -->

# Where This Idea Came From

<div class="thread">You just felt the wait. Now: who noticed the gap first, and what did they build?</div>

- **1962:** Tom Kilburn's Atlas computer, in Manchester, introduces a "one-level store." It hides slow storage behind something faster, automatically
- **1965:** Maurice Wilkes proposes a small, fast "slave memory" that sits between the processor and main memory

<div class="why">
In 1968, IBM's System/360 Model 85 ships the first commercial cache,
and the name "cache" sticks. As processors kept getting faster than
memory, this extra layer became necessary in every computer.
</div>

---

# Sixty Years of the Same Gap

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1962</div><div class="d">Atlas computer<br>"one-level store" idea</div></div>
<div class="pt"><div class="dot"></div><div class="y">1965</div><div class="d">Wilkes proposes<br>"slave memory"</div></div>
<div class="pt"><div class="dot"></div><div class="y">1968</div><div class="d">IBM 360/85<br>first cache ships</div></div>
<div class="pt"><div class="dot"></div><div class="y">Today</div><div class="d">Multiple cache layers<br>in every chip</div></div>
</div>

The processor-memory gap never closed. Engineers just kept adding
smarter layers to hide it.

---

<!-- SLOT 9: Core concept -->

# Memory Hierarchy: Definition

<div class="thread">Sixty years of hiding the same gap point at one clear idea.</div>

> A **memory hierarchy** is a set of storage layers, from small and fast
> to huge and slow. Most requests are served by the fastest layer that
> can hold the data.

- **Cache:** the fastest layer, close to the processor, holding recently or often used data
- **Main memory (RAM):** larger and slower, holds the whole running program
- **Disk / SSD:** huge and slowest, holds data even when the power is off

---

<!-- Act 3 / BUILD -->

# The Gap the Pipeline Cannot Fix

<div class="thread">This is the number behind the whole week's story.</div>

| Storage | Typical wait | Roughly how many chip steps that wastes |
|---|---|---|
| Register (inside the chip) | under 1 chip step | 0 |
| Cache | about 1 chip step | ~1 |
| Main memory (RAM) | about 100 chip steps | ~100 |
| SSD | about 100,000 chip steps | ~100,000 |
| Hard disk | about 10,000,000 chip steps | ~10,000,000 |

Even a perfectly working pipeline stalls on every one of these waits.

---

# Layers, Not One Giant Memory

<div class="thread">One gap, solved by stacking storage instead of picking just one.</div>

<div class="stack">
<div class="layer view"><span class="h">Cache</span> <span class="s">small, very fast, sits right next to the processor</span></div>
<div class="layer logical"><span class="h">Main Memory (RAM)</span> <span class="s">bigger, slower, holds the whole running program</span></div>
<div class="layer physical"><span class="h">Disk / SSD</span> <span class="s">huge, slowest, keeps data even when powered off</span></div>
</div>

No single memory is both huge and fast enough. Layering gets close to both.

---

# Why Not Just Build One Big, Fast Memory?

<div class="thread">The driving question, answered directly.</div>

- Fast memory, like cache, needs more parts for every bit it stores, so it costs far more per byte
- Fast memory also uses more power and chip space, so a chip cannot make it huge
- Slow memory, like RAM or disk, is cheap and huge, but too slow to keep the processor busy alone

<div class="why">
This is a genuine trade-off, not a design mistake. Cost, space, and
speed cannot all be maximized at the same time.
</div>

---

# Real Chips Have Several Cache Levels

<div class="thread">"Cache" is not one single layer. Modern chips stack several.</div>

| Level | Typical size | Speed |
|---|---|---|
| L1 cache | ~32-64 KB | fastest, closest to each core |
| L2 cache | ~256 KB - 1 MB | fast, still close to the core |
| L3 cache | several MB, up to tens of MB | slower, shared by all cores |

SmartPick's "24 MB cache" spec usually means the L3 cache. It is the
layer the processor reaches only after L1 and L2 both miss.

---

# Where Cache Size Matters in Real Products

<div class="thread">The same layered idea, everywhere you look.</div>

<div class="appgrid">
<div class="app"><div class="name">Smartphones</div><div class="desc">small, battery-limited caches balance speed against heat and power</div></div>
<div class="app"><div class="name">Gaming consoles</div><div class="desc">large caches keep game textures close to the processor</div></div>
<div class="app"><div class="name">Cloud servers</div><div class="desc">more cache per rented core often costs more, for real reasons</div></div>
<div class="app"><div class="name">Databases</div><div class="desc">a "hot" table that fits in cache answers queries far faster</div></div>
<div class="app"><div class="name">Web browsers</div><div class="desc">cache recently visited pages so a "back" click feels instant</div></div>
<div class="app"><div class="name">AI training chips</div><div class="desc">huge on-chip caches keep costly data movement to a minimum</div></div>
</div>

---

# Why Caching Actually Works

<div class="thread">Layers only help if we can predict what the processor needs next. We can.</div>

<div class="two-col">
<div>

**Temporal locality**

If data was used once, it is often used again soon.

Example: replaying the same song.

</div>
<div>

**Spatial locality**

If one piece of data was used, nearby data is often used next.

Example: reading a book page by page.

</div>
</div>

Caches bet on both patterns, and the bet usually pays off.

---

# Cache Hit: The Common, Fast Case

<div class="thread">Locality is the bet. Hit and miss are the two possible outcomes.</div>

<div class="pipeline">
<div class="stage"><div class="h">CPU asks</div><div class="s">"give me this data"</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Cache has it</div><div class="s">found right away</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Fast answer</div><div class="s">about 1 chip step</div></div>
</div>

A **cache hit** is the case the whole hierarchy is betting on, and the case that happens most often.

---

# Cache Miss: The Slower Case

<div class="thread">Sometimes the bet does not pay off. The processor still needs an answer.</div>

<div class="pipeline">
<div class="stage"><div class="h">CPU asks</div><div class="s">"give me this data"</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Cache does not have it</div><div class="s">must ask main memory</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Fetch from RAM</div><div class="s">about 100 chip steps</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Slow answer</div><div class="s">also saved in cache, for next time</div></div>
</div>

A **cache miss** costs far more time, so a good cache keeps misses rare.

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week11/worksheet.html">Worksheet Part A</a></strong>. You will compare
SmartPick's two cache sizes and predict which laptop has fewer slow
waits, and why. About 15 minutes.
</div>

- Write down your prediction and your reason
- It is OK to be unsure — write down what you do not know too
- We compare answers together at the start of 차시 3

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work. Do not confirm any answers yet, the real numbers come in 차시 3.
-->

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: how do we put a number on this?</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **Miss rate:** the share of memory requests a cache cannot answer by itself
- **Miss penalty:** the extra time a miss costs, on top of a normal hit
- **AMAT:** average memory access time — the average time one memory request takes
- **Working set:** the data a program is actively using right now

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week11/worksheet.html">Worksheet Part B</a></strong>. Check your Part A
prediction against the real numbers, then answer two new questions.
About 15 minutes.
</div>

- The answer key shows how to turn "bigger cache" into an actual number
- That number is exactly what the rest of today's session builds toward

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). Let pairs self-check before the AMAT slides that follow.
-->

---

# Measuring a Cache: Hit Rate and Miss Rate

<div class="thread">Now we turn "usually fast" into a real number.</div>

Example: out of 100 memory requests, a cache answers 90 by itself.

- **Hit rate** = 90 / 100 = **90%**
- **Miss rate** = 10 / 100 = **10%**

A bigger cache usually raises the hit rate, because more data fits close to the processor.

---

# Putting a Number on the Wait: AMAT

<div class="thread">Hit rate alone is not enough. We must also weigh how much a miss costs.</div>

> **AMAT** (average memory access time) = hit time + (miss rate × miss penalty)

Example: hit time = 1 ns, miss rate = 10%, miss penalty = 100 ns extra.

AMAT = 1 + (0.10 × 100) = **11 ns**

A lower AMAT means the processor spends less time waiting, on average.

---

# When a Miss Happens, and Why

<div class="thread">Not all misses share the same cause. Knowing why helps you know what to fix.</div>

- **Compulsory miss:** the very first time data is asked for — it was never in the cache yet
- **Capacity miss:** the cache is too small to hold everything the program is using right now
- **Conflict miss:** the data could fit, but the cache's rules sent it to a slot another piece of data already uses

<div class="why">
Capacity misses are exactly why next week matters. Some programs and
datasets simply do not fit, no matter how the cache is designed.
</div>

---

<!-- SLOT N-2: Worked example -->

# Case Study: Why Studio Really Was Faster

<div class="thread">Week 1 could not fully explain this gap. Today, we finally can.</div>

| | Value laptop (8 MB cache) | Studio laptop (24 MB cache) |
|---|---|---|
| Hit rate | 80% | 95% |
| Hit time | 1 ns | 1 ns |
| Miss penalty | 100 ns | 100 ns |
| **AMAT** | 1 + 0.20×100 = **21 ns** | 1 + 0.05×100 = **6 ns** |

Same story as Week 1, now with real numbers. Studio's bigger cache
raises the hit rate, which cuts AMAT to about a third of Value's.

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"Bigger cache always means faster":** past a point, extra cache barely raises hit rate, but still costs money and chip space
- **"Cache and RAM are the same thing":** cache is small and fast. RAM is bigger and slower, and holds the whole running program
- **"A cache miss means something is broken":** misses are normal and expected. No cache is big enough to hold everything

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. In plain words, explain the difference between a cache hit and a cache miss
2. A cache has a 95% hit rate, 2 ns hit time, and a 120 ns miss penalty. Compute AMAT

<div class="why">
After this, take the short <a href="materials/week11/quiz.html">self-check quiz</a> for more
practice. It is ungraded.
</div>

---

# Answers

1. A **hit** means the cache already has the data. A **miss** means it does not, so the processor must wait for main memory
2. AMAT = 2 + (0.05 × 120) = 2 + 6 = **8 ns**

---

<!-- SLOT N+1: Limits (Act 4 / CLOSE), becomes Week 12 slot 4 -->

# What Caching Cannot Do

<div class="limits">
Caching speeds up memory, but only for programs and datasets that fit.
A cache only holds a small slice of all the data a computer owns. If a
program's data is too big, or jumps around unpredictably, caching stops
helping.
</div>

---

<!-- SLOT N+2: Bridge -->

# Next Week

Week 11 leaves **what happens when a program or dataset does not fit in
memory at all** unsolved. **Week 12, Memory Hierarchy II**, addresses
it: virtual memory.

---

<!-- SLOT N+3: Summary -->

# Summary

- Memory is far slower than the processor, so even a perfect pipeline still waits
- A memory hierarchy hides this gap with layers: cache, RAM, disk
- Caching works because programs reuse the same and nearby data (locality)
- AMAT turns hit rate and miss penalty into one real number for comparing designs
- **Reading:** Hennessy & Patterson, 6th ed., Chapter 2
- **Handout:** [materials/week11/handout.md](materials/week11/handout.html), glossary and the full AMAT walkthrough
- **Prepare:** think of one program you use that feels slow to "load." Bring one guess why

---

<!-- SLOT N+4: Thank You -->
<!-- _class: end -->

# Thank You
