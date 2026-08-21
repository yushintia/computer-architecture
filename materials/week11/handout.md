# Week 11 Handout: Memory Hierarchy I

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **Memory** | Where a running program's instructions and data are stored |
| **Memory hierarchy** | A set of storage layers, from small and fast to huge and slow, built so most requests are served by the fastest layer that can hold the data |
| **Cache** | A small, very fast memory placed close to the processor, holding data used recently or often |
| **Main memory (RAM)** | The computer's main working storage. Bigger than cache, but slower |
| **Disk / SSD** | Huge, slowest storage. Keeps data even when the power is off |
| **Cache hit** | The processor asks for data and finds it already in the cache |
| **Cache miss** | The processor asks for data and it is not in the cache yet |
| **Latency** | How long one single request takes to get an answer |
| **Locality** | The tendency of a program to reuse the same or nearby data soon |
| **Temporal locality** | If data was used once, it is often used again soon |
| **Spatial locality** | If one piece of data was used, nearby data is often used next |
| **Hit rate** | The share of memory requests a cache can answer by itself |
| **Miss rate** | The share of memory requests a cache cannot answer by itself |
| **Miss penalty** | The extra time a miss costs, on top of a normal hit |
| **AMAT** | Average memory access time — the average time one memory request takes, counting both hits and misses |
| **Compulsory miss** | A miss caused by asking for data for the very first time |
| **Capacity miss** | A miss caused because the cache is too small to hold everything the program is using |
| **Conflict miss** | A miss caused because the cache's own rules sent data to a slot another piece of data already uses |
| **Working set** | The data a program is actively using right now |
| **L1 / L2 / L3 cache** | The usual names for a chip's cache layers, from smallest-and-fastest (L1) to largest-and-slowest (L3) |

---

## 2. The SmartPick Story, Continued: The Real Numbers

This is the full version of the AMAT walkthrough from class. Read it
slowly if the in-class pace felt fast.

**Where we left off.** In Week 1, SmartPick's two laptops, Value and
Studio, had the same clock speed (3.0 GHz) and the same core count (8),
but Studio finished the same video export more than twice as fast. The
only real hardware difference on the spec sheet was cache size: Value
had 8 MB, Studio had 24 MB. Week 1 could say *that* cache size mattered,
but not *how much*, or *why*, exactly.

**Step 1: Turn cache size into a hit rate.** A bigger cache can hold
more of the data a program is actively using (its **working set**), so
it answers more requests by itself. Assume Value's smaller cache reaches
an **80% hit rate**, while Studio's bigger cache reaches **95%**.

**Step 2: Turn hit rate into AMAT.** Assume both laptops have the same
hit time (1 ns) and the same miss penalty (100 ns, the cost of a trip to
main memory). Apply the formula:

> AMAT = hit time + (miss rate × miss penalty)

| | Value laptop | Studio laptop |
|---|---|---|
| Hit rate | 80% | 95% |
| Miss rate | 20% | 5% |
| Hit time | 1 ns | 1 ns |
| Miss penalty | 100 ns | 100 ns |
| **AMAT** | 1 + (0.20 × 100) = **21 ns** | 1 + (0.05 × 100) = **6 ns** |

**Step 3: Read what the number means.** Studio's average memory request
takes about 6 ns; Value's takes about 21 ns — roughly **3.5 times
longer**. A video export makes millions of memory requests, so this
per-request gap adds up to the minutes-long difference the SmartPick
clerk measured with a stopwatch back in Week 1.

**Step 4: State clearly what we can, and still cannot, say.** We can now
explain the Week 1 mystery with real numbers, using hit rate, miss
penalty, and AMAT. We still cannot explain what happens when a program's
data is simply **too big to fit** in any reasonably sized cache — that
gap is Week 12's job, with virtual memory.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations that were trimmed from the slides
to keep class time short. Read it if you are curious or want more
examples.

**A library, not a warehouse.** Picture a small desk next to you (cache),
a bookshelf in your room (main memory), and a public library across town
(disk). You keep the books you are using right now on the desk. Walking
to the bookshelf is slower than reaching your desk; driving to the
library is slower still. A memory hierarchy is built the same way: keep
what you need most, closest to you.

**Why caches actually predict well.** It sounds risky to guess what a
processor will need next, but real programs are very repetitive: loops
run the same instructions many times (temporal locality), and arrays are
usually read in order (spatial locality). Caches exploit exactly these
two everyday patterns, which is why the "bet" pays off far more often
than it fails.

**Why "just add more cache" is not free.** Fast memory (SRAM, used for
cache) needs more transistors per stored bit than slow memory (DRAM,
used for RAM). More transistors means more cost, more power, and more
heat, in a fixed amount of chip space. Chip designers do not skip a huge
fast cache by accident — it is a real engineering trade-off, the same
kind of trade-off behind the "power wall" from Week 1.

**Where this shows up around you.**

- **Web browsers:** cache recently visited pages, so pressing "back" feels instant
- **Databases:** keep frequently queried ("hot") data in memory, avoiding slow disk reads
- **Content delivery networks (CDNs):** cache videos and images near your city, instead of one far-away server
- **Game consoles:** cache textures and level data close to the processor, to avoid stutter
- **CPUs vs. GPUs:** CPUs use large caches per core; GPUs use smaller caches but many more cores, a different point on the same trade-off

**Who actually designs this, as a job.**

- **Cache and memory-system architects** decide cache size, number of levels, and replacement rules
- **Compiler engineers** write code generators that arrange data to use locality well
- **Database engineers** design indexes and buffer pools, which are really software-level caches
- **Site reliability / performance engineers** measure real cache hit rates in production and tune systems around them

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** A cache answers 180 out of 200 memory requests by itself.
Find the hit rate and the miss rate.
> **Answer:** Hit rate = 180 / 200 = **90%**. Miss rate = 20 / 200 = **10%**.

**Problem 2.** A cache has a hit time of 2 ns, a miss rate of 8%, and a
miss penalty of 90 ns. Compute AMAT.
> **Answer:** AMAT = 2 + (0.08 × 90) = 2 + 7.2 = **9.2 ns**.

**Problem 3.** Two caches have the same hit time (1 ns) and the same
miss penalty (120 ns). Cache A has a 70% hit rate; Cache B has a 96% hit
rate. Which AMAT is lower, and by roughly how much?
> **Answer:** Cache A: AMAT = 1 + (0.30 × 120) = 37 ns. Cache B: AMAT = 1
> + (0.04 × 120) = 5.8 ns. Cache B is lower, by a factor of about 6.

**Problem 4.** In one sentence, explain the difference between temporal
locality and spatial locality.
> **Answer (example):** Temporal locality is reusing the same data soon;
> spatial locality is using data that sits near data you just used.

**Problem 5.** A program reads a huge dataset once, in a random order,
and never reuses any value. Would a bigger cache help this program much?
Why or why not?
> **Answer:** Not much. With no reuse and no nearby-data pattern, there
> is little locality for the cache to exploit, so most requests stay
> misses no matter the cache size.

**Problem 6.** A processor asks for data for the very first time, and it
is not in the cache. Which type of miss is this: compulsory, capacity,
or conflict?
> **Answer:** Compulsory — the data was simply never fetched before, so
> it could not already be in the cache.
