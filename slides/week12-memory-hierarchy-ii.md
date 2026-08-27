---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 12: Memory Hierarchy II

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Welcome the class back. Ask: "Has your laptop or phone ever slowed
down badly when you had too many things open?" Most hands go up. Say:
today we find out exactly why, and what fixes it.
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
<div class="wk now"><div class="n">Wk 12</div><div class="t">Memory Hierarchy II</div></div>
<div class="wk"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

<!--
notes: Point at Week 11 and Week 12. Say: last week made memory fast for
data that fits close to the processor. This week asks what happens when
it does not fit at all.
-->

---

<!-- SLOT 3: Recap + open wound -->

# Last Week, This Week

- **Last week delivered:** caching, small, fast memory that speeds up access to data used again soon
- **Last week left broken:** caching speeds up memory, but only for programs and datasets that actually fit in it

<!-- notes: This second bullet is this week's pain, almost word for word. Do not explain it further yet, let slot 4 make it concrete. -->

---

<!-- NEW: Key Words for 차시 1 -->

# Key Words Today (Session 1)

- **Physical memory (RAM):** the fast, chip-based memory a running program actually uses
- **Address:** a number that names one exact spot in memory
- **Out of memory:** what happens when a program needs more memory than the machine has
- **Disk / storage:** bigger, slower storage that keeps files even when the power is off

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), zero jargon -->

# When the Video Project Stopped Fitting

<div class="pain">

A SmartPick customer bought the faster Studio laptop for video editing. At
first, everything is fast: opening a clip, trimming it, exporting it.

Then she adds forty more clips to the same project, for a longer video.
The laptop slows down badly. Clips take seconds to open. Exporting freezes
for minutes. Same laptop, same buyer, much slower.

The clerk checks the machine. Nothing is broken. The project itself simply
grew bigger than what the laptop can hold close and ready at once.

</div>

<!--
notes: Do not say "virtual memory" or "RAM" limits yet. Let the class sit
with the confusion. Ask: "Any guesses why the same laptop got so much
slower?" Take 2-3 guesses without confirming or denying any of them.
-->

---

# The Same Laptop, Two Very Different Afternoons

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">Small project, 10 clips</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 30%"></div></div>
  <div class="bar-value">~2 sec to open a clip</div>
</div>
<div class="bar-row">
  <div class="bar-label">Large project, 50 clips</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">~25 sec to open a clip</div>
</div>
</div>

Nothing about the laptop changed. Only the size of the project did. That
size crossed a line the laptop could not cross quickly.

---

<!-- SLOT 5: Cost of not knowing -->

# What This Actually Costs

- A video editor misses a client deadline because a large project keeps freezing
- A student's laptop crashes mid-assignment, losing unsaved work right before it is due
- A company's server runs out of memory during peak traffic and stops serving customers

<div class="why">
<strong>In industry:</strong> "out of memory" crashes and slowdowns are a
top cause of real production outages. Interviewers often ask how an
operating system keeps many running programs safe in memory at once.
</div>

---

# It Gets More Expensive the Bigger the System Is

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One student, one crashed file</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 20%"></div></div>
  <div class="bar-value">hours of redone work</div>
</div>
<div class="bar-row">
  <div class="bar-label">One company, server out of memory</div>
  <div class="bar-track"><div class="bar-fill risk-med" style="width: 55%"></div></div>
  <div class="bar-value">an outage, angry customers</div>
</div>
<div class="bar-row">
  <div class="bar-label">One datacenter, memory mismanaged at scale</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 92%"></div></div>
  <div class="bar-value">service down for millions of users</div>
</div>
</div>
<div class="bar-note">these numbers are examples, not measured data — the point is the pattern</div>

Same mistake, three different sizes. Managing memory well matters at every
scale you work at.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"How can a program use more memory than the machine physically has, without programs stepping on each other?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

<div class="cardlist">
<div class="card"><div class="h">Memory Shortfall</div><div class="d">Explain why a program can need more memory than the machine physically has</div></div>
<div class="card"><div class="h">Address Translation</div><div class="d">Describe how virtual memory turns a program's addresses into real memory locations</div></div>
<div class="card"><div class="h">Page Faults</div><div class="d">Explain what happens, step by step, when a needed page is not in RAM</div></div>
<div class="card"><div class="h">Memory Protection</div><div class="d">Explain how virtual memory keeps separate programs from touching each other's memory</div></div>
</div>

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Coming Up Next: Worksheet Part A

Next session, you will work in pairs on
**[Worksheet Part A](materials/week12/worksheet.html)**.

- You will see two laptops with different RAM sizes doing the same big editing job
- Your pair predicts which laptop handles it better, and why
- We compare answers together at the start of 차시 3

<div class="why">
Bring your notebook. No laptop or calculator needed, just the worksheet we
hand out.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: where did this idea come from?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **Virtual memory:** a trick that gives each program its own big, private view of memory
- **Page:** a small, fixed-size chunk that memory is divided into for this trick
- **Page table:** the list that maps a program's pages to real memory locations
- **Virtual address vs. physical address:** the address a program uses, versus where data really sits

---

<!-- SLOT 8: Origin -->

# This Trick Is Older Than You Might Think

<div class="thread">You just felt the pain. Now: who solved it first, and why?</div>

- **1959-1962:** the Atlas computer at Manchester University has far less real memory than programmers want to use
- Tom Kilburn's team invents the "one-level store." Programs write addresses as if memory were huge. The machine quietly moves data in and out behind the scenes

<div class="why">
By the late 1960s, computers began serving many users on one machine at
once. Each user needed private memory, safely separated from the others.
Virtual memory answered both problems at once: bigger, and safer.
</div>

---

# From One Machine, One User, to Everyone at Once

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1962</div><div class="d">Atlas<br>first working virtual memory</div></div>
<div class="pt"><div class="dot"></div><div class="y">1969</div><div class="d">Multics<br>separate memory per user</div></div>
<div class="pt"><div class="dot"></div><div class="y">1980s</div><div class="d">Unix, then Windows/macOS<br>make it a standard feature</div></div>
<div class="pt"><div class="dot"></div><div class="y">Today</div><div class="d">Every phone, laptop, server<br>still runs on this idea</div></div>
</div>

The same idea, sixty years later, runs underneath every app you open
today, including the SmartPick laptops.

---

<!-- SLOT 9: Core concept -->

# Virtual Memory: Definition

<div class="thread">One idea, two problems solved at once. Here it is, formally.</div>

> **Virtual memory** is a technique that gives each running program its
> own large, private view of memory, by translating the program's
> addresses into real physical memory locations, and moving data between
> memory and disk as needed.

- **Private view:** one program cannot see or touch another program's memory
- **Larger than physical:** a program can use more memory than the machine has installed
- **Translation:** every address a program uses is converted before it reaches real memory

---

# Where This Shows Up Around You

<div class="thread">This is not just a video-editing problem. It shows up everywhere.</div>

<div class="appgrid">
<div class="app"><div class="name">Web Browser</div><div class="desc">Each tab gets its own protected memory, so one crashing tab does not kill the browser</div></div>
<div class="app"><div class="name">Photo &amp; Video Editors</div><div class="desc">Large files lean on virtual memory whenever they outgrow installed RAM</div></div>
<div class="app"><div class="name">Video Calls</div><div class="desc">Runs safely alongside other open apps, isolated from each one</div></div>
<div class="app"><div class="name">Cloud Gaming</div><div class="desc">One server's memory is carefully split across many players at once</div></div>
<div class="app"><div class="name">Huge Spreadsheets</div><div class="desc">A file bigger than RAM still opens, just slower once paging starts</div></div>
<div class="app"><div class="name">Multitasking</div><div class="desc">Every open app gets its own private page table, automatically</div></div>
</div>

---

<!-- Act 3 / BUILD -->

# Three Places Your Data Can Be

<div class="thread">Before the mechanics, the map: where does data actually live?</div>

<div class="stack">
<div class="layer view"><span class="h">Virtual Address Space</span> <span class="s">the huge, private memory a program believes it has</span></div>
<div class="layer logical"><span class="h">Physical RAM</span> <span class="s">real, fast chip memory — always limited in size</span></div>
<div class="layer physical"><span class="h">Disk / Swap Space</span> <span class="s">slow overflow storage for pages RAM cannot hold right now</span></div>
</div>

A program only ever sees the top layer. The other two are the machine's
problem to manage, not the program's.

---

# How One Address Becomes Another

<div class="thread">The core mechanic behind everything else this week.</div>

<div class="pipeline">
<div class="stage"><div class="h">Program</div><div class="s">asks for virtual address #4,200</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Page Table</div><div class="s">looks up which real page holds it</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Physical RAM</div><div class="s">the program's data actually lives here</div></div>
</div>

Every single memory access in your program passes through this
translation, automatically, every time.

---

# Memory, Cut Into Equal Pieces

- A **page** is a small, fixed-size chunk of a program's virtual memory, often 4 KB
- A **page frame** is the same size chunk, but inside real physical RAM
- The page table simply records: "this virtual page currently sits in that physical frame"
- Some pages may not be in RAM at all yet, only sitting on disk

---

# A Page Table In Practice

<div class="thread">The idea from the last slide, made concrete with real-looking numbers.</div>

| Virtual page | Status | Physical frame |
|---|---|---|
| Page 0 | in RAM | Frame 12 |
| Page 1 | in RAM | Frame 47 |
| Page 2 | on disk | — |
| Page 3 | in RAM | Frame 3 |

The program only ever asks for "page 2." The page table quietly decides
whether that means a fast frame in RAM, or a slow trip to disk.

---

# A Cache for the Page Table Itself

<div class="thread">Last week's idea, reused: keep the hot data close.</div>

- Checking the full page table on every single memory access would be too slow
- The **TLB** (Translation Lookaside Buffer) is a small, fast cache of recent translations
- Most of the time, the answer is already in the TLB, so translation is nearly free
- This is last week's caching idea, applied to addresses instead of data

---

# When the Page Is Not There Yet

- Sometimes the page table says a page sits only on disk, not in RAM
- This is called a **page fault**
- The processor pauses, and the operating system steps in
- The OS finds a free frame, loads the page from disk, updates the page table, then lets the program continue

<div class="why">
A page fault costs far more than a cache miss. RAM answers in
nanoseconds; a disk can take milliseconds, thousands of times slower.
</div>

---

# Keeping Programs Out of Each Other's Memory

- Each running program gets its own separate page table
- Two programs can both use virtual address 4,200 and never collide, since each maps to a different physical frame
- If a program tries to touch a physical frame it does not own, the hardware blocks it
- This is why one crashing app usually does not crash your whole computer

---

# Two Programs, Same Virtual Address

<div class="thread">The isolation idea from the last slide, made concrete.</div>

| | Virtual address | Physical frame |
|---|---|---|
| Program A | 4,200 | Frame 8 |
| Program B | 4,200 | Frame 55 |

Same number, different program, different real memory. Program A can
never accidentally read or write Program B's data.

---

# Isolation Is Also a Security Feature

<div class="thread">Keeping programs separate is not only about speed and crashes.</div>

- A browser tab cannot read another tab's private data, because of this same address separation
- Malware in one program cannot simply reach into another program's memory
- Many real security bugs are exactly a program tricking the hardware into breaking this separation

<div class="why">
This is why "isolation" appears constantly in real security job postings,
not only in performance ones.
</div>

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week12/worksheet.html">Worksheet Part A</a></strong>. You will compare two
laptops with different RAM sizes doing the same big editing job. About 15
minutes.
</div>

- Write down your prediction and your reason
- It is fine to be unsure, write down what you do not know too
- We compare answers together at the start of 차시 3

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work. Do not confirm any answers yet, the real discussion happens next
session.
-->

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: what happens when memory really is not enough?</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **Page fault:** the pause that happens when a needed page is only on disk
- **Thrashing:** when a machine spends most of its time swapping pages instead of working
- **Swap space:** the area of disk set aside to hold pages moved out of RAM
- **Isolation:** keeping one program's memory completely separate from another's

---

<!-- SLOT N-2: Worked example -->

# Case Study: Studio's Big Project, Explained

<div class="thread">Back to the pain from 차시 1. Now we can actually explain it.</div>

Studio has 16 GB of real RAM. The video project needs far more active data
as more clips are added.

| Stage | Active data needed | Fits in 16 GB RAM? | Result |
|---|---|---|---|
| 10 clips | ~6 GB | Yes | Fast, almost no page faults |
| 50 clips | ~40 GB | No | Constant page faults, slow |

Virtual memory does not fail here. It keeps the project running at all,
just far slower, because it must keep swapping pages to and from disk.

---

# Why the Slowdown Feels So Extreme

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One RAM access</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 5%"></div></div>
  <div class="bar-value">~100 nanoseconds</div>
</div>
<div class="bar-row">
  <div class="bar-label">One page fault (disk)</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">~100,000 nanoseconds</div>
</div>
</div>

One page fault costs about as much time as a thousand RAM accesses. A
large project can trigger thousands of page faults in a single afternoon.

---

# What If We Just Add More RAM?

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">16 GB RAM, 50-clip project</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">~300 page faults / min</div>
</div>
<div class="bar-row">
  <div class="bar-label">64 GB RAM, 50-clip project</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 8%"></div></div>
  <div class="bar-value">~10 page faults / min</div>
</div>
</div>

Same laptop, same project, more RAM. Virtual memory itself did not
change; it just barely needs to reach for the disk anymore.

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week12/worksheet.html">Worksheet Part B</a></strong>. Check your Part A
prediction against the real answer, then answer two new questions. About
15 minutes.
</div>

- The answer key explains why more RAM helps. Virtual memory alone cannot make it as fast as truly fitting in RAM
- That gap, between "it still works" and "it works well," is what this week explains

<!--
notes: Hand out Worksheet Part B (it includes the Part A answer key at
the top). After ~15 minutes, cold-call 2-3 pairs to share their reasoning
before moving on.
-->

---

# Let's Trace One Memory Access, Start to Finish

<div class="thread">Before closing, connect every piece back to today's opening story.</div>

<div class="pipeline">
<div class="stage"><div class="h">Program</div><div class="s">asks for a virtual address</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">TLB / Page Table</div><div class="s">translates it, cache first</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">RAM</div><div class="s">found here: fast, done</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Disk</div><div class="s">not found: page fault, slow reload</div></div>
</div>

Every layer from this week and last week works together on this one
path, on every single memory access.

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"Virtual memory means unlimited memory":** it is bounded by disk space, and gets very slow once it is used heavily
- **"A page fault costs about the same as a cache miss":** it does not. A page fault is far more expensive, since disk is thousands of times slower than RAM
- **"More RAM never helps once you have virtual memory":** more RAM directly means fewer page faults, and a faster machine

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. In your own words, why can a program use more memory than the machine physically has installed?
2. Two programs both use virtual address 4,200 at the same time. Why don't they collide?

<div class="why">
After this, take the short <a href="materials/week12/quiz.html">self-check quiz</a> for more
practice. It is ungraded.
</div>

---

# Answers

1. A page table translates the program's virtual addresses into real memory, and moves pages between disk and RAM as needed. The program never needs all its data in RAM at once
2. Each program has its own separate page table. The same virtual address maps to a different, private physical frame for each one

---

<!-- SLOT N+1: Limits (Act 4 / CLOSE), becomes Week 13 slot 4 -->

# What Virtual Memory Cannot Do

<div class="limits">
We can now give any program more memory than the machine physically has,
safely separated from every other program. But everything so far still
assumes one core, doing one thing at a time. Virtual memory solves
capacity, but a single core is still the whole story.
</div>

---

<!-- SLOT N+2: Bridge -->

# Next Week

Week 12 leaves **using many cores together** unsolved. **Week 13,
Parallelism**, addresses it: how modern chips split work across cores,
and Quiz 2.

---

<!-- SLOT N+3: Summary -->

# Summary

- Virtual memory gives every program its own large, private view of memory, using pages and a page table
- A page fault, loading a page from disk, costs far more time than a cache miss or a TLB hit
- A separate page table per program is what keeps one program from touching another's memory
- **You did today:** Worksheet Parts A and B, self-check quiz
- **Reading:** Bryant & O'Hallaron, *Computer Systems*, 3rd ed., Chapter 9, "Virtual Memory"
- **Handout:** [materials/week12/handout.md](materials/week12/handout.html), glossary and the full SmartPick walkthrough
- **Prepare:** think of one everyday task where two things happen "at once." Bring it to class

---

<!-- SLOT N+4: Thank You -->
<!-- _class: end -->

# Thank You
