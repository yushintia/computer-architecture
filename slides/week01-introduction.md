---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 1: Introduction

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Ask who has ever argued with a friend or a salesperson about which
laptop is "actually faster." That argument is today's hook.
-->

---

<!-- SLOT 2: Where we are -->

# Where We Are

<div class="roadmap">
<div class="wk now"><div class="n">Wk 1</div><div class="t">Introduction</div></div>
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
<div class="wk"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

<!-- notes: Point out the arc: measure, represent, execute, speed up, remember, parallelize. Fifteen weeks, one machine, built up layer by layer. -->

---

<!-- SLOT 3: What you already bring -->

# What You Already Bring

- **Digital Logic**: you already know gates, truth tables, flip-flops. Today's machine is built entirely out of those parts
- **Computer Programming**: you have written code that "just runs." This course opens the box underneath it
- **Data Structure**: you know arrays and pointers live "in memory." This course explains what memory actually is, physically

We are not starting from zero. We are pointing what you know at the
machine that has been running your code the whole time.

---

<!-- Course logistics appendix: administrative, outside the spine, placed here so it doesn't blunt slot 4 -->

<!-- _class: section -->

# Course Logistics
<div class="driving-q">Read once now, referenced all semester.</div>

---

# Grading & Materials

| Item | Weight |
|---|---|
| Attendance | 10% |
| Midterm | 30% |
| Final | 30% |
| Assignments | 10% |
| Presentation | 10% |
| In-class items | 10% |

<!-- notes: Assignment 1 due Week 4 (ISA I). Assignment 2 due Week 11 (Memory Hierarchy I). Quiz 1 Week 5, Quiz 2 Week 13. Week 14 is a group presentation on a modern processor or architecture case study. -->

---

# Textbook, Policy & Contact

- **Textbook:** Hennessy & Patterson, *Computer Architecture: A Quantitative Approach*, 6th ed., Morgan Kaufmann, 2017
- **References:** Stallings, *Computer Organization and Architecture*, Pearson, 2019; Bryant & O'Hallaron, *Computer Systems: A Programmer's Perspective*, 3rd ed., Pearson, 2015
- **Policy:** attend and participate every class; late assignments are penalized; plagiarism and cheating lead to disciplinary action
- **Contact:** yushintia@deu.ac.kr, office hours by email appointment

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), zero jargon -->

# Two Laptops, One Confusing Afternoon

<div class="pain">

A customer walks into SmartPick, the campus electronics store, holding
two laptop listings pulled up on her phone. Both list the exact same
processor speed, printed in big letters on the box: 3.0 GHz. One costs
more than the other, so she asks the obvious question: since the number
on the box is the same, why is the expensive one worth the extra money?

The clerk tries to answer. He opens both laptops, runs the same video
export, and starts a timer. The cheaper one finishes in just under four
minutes. The expensive one finishes in under ninety seconds, more than
twice as fast, on paper the identical processor speed. He has no idea
why, and neither does she.

</div>

<!-- notes: Do not use the word "architecture" or "microarchitecture" yet. Let the mismatch sit uncomfortably first. -->

---

# The Number on the Box Was Not the Whole Story

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">Cheaper laptop, video export</div>
  <div class="bar-track"><div class="bar-fill long" style="width: 100%"></div></div>
  <div class="bar-value">~3 min 50 sec</div>
</div>
<div class="bar-row">
  <div class="bar-label">Expensive laptop, same export</div>
  <div class="bar-track"><div class="bar-fill short" style="width: 38%"></div></div>
  <div class="bar-value">~1 min 25 sec</div>
</div>
</div>

Same advertised clock speed. More than twice the real-world speed. This
gap is not a rounding error, and it is not marketing. It is this entire
course.

<!-- notes: Let the gap between the two bars sit for a second before moving on. -->

---

<!-- SLOT 5: Cost of not knowing -->

# What Else This Actually Costs

- A student buys the wrong laptop for video editing or game development coursework, based on a spec sheet number that does not mean what they think it means
- A startup rents the wrong cloud server tier for their app, paying for clock speed instead of the performance their workload actually needs
- A company ships a product on hardware that "should" be fast enough on paper, then misses its deadline when it is not

<div class="why">
<strong>In industry:</strong> "why is this slow, and what would you change"
is a standard interview question for hardware, systems, and even backend
roles. At cloud-computing scale, picking the wrong processor generation
for a datacenter has cost real companies millions of dollars a year in
wasted spend.
</div>

---

# It Gets More Expensive the Bigger the Decision Is

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One student, one laptop</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 20%"></div></div>
  <div class="bar-value">a few hundred dollars, wasted</div>
</div>
<div class="bar-row">
  <div class="bar-label">One startup, one cloud contract</div>
  <div class="bar-track"><div class="bar-fill risk-med" style="width: 55%"></div></div>
  <div class="bar-value">real monthly budget, wasted</div>
</div>
<div class="bar-row">
  <div class="bar-label">One datacenter, wrong chip generation</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 92%"></div></div>
  <div class="bar-value">millions of dollars a year</div>
</div>
</div>
<div class="bar-note">illustrative, not measured data: the point is the trend, not the exact numbers</div>

Same mistake, three sizes. A system with no way to reason about
performance **will** get this wrong, at whatever scale it operates.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"What's actually happening, layer by layer, when a computer runs a single line of your code?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

1. Describe the layers between a line of source code and the physical transistors that execute it
2. Explain why identical clock speed does not guarantee identical real-world performance
3. Name the semester's major stops: instructions, datapath, pipelining, memory, parallelism
4. State this course's official teaching objectives and where each is covered

---

# This Course's Teaching Objectives

<div class="thread">Not just this week's goals. This is what the syllabus commits this whole course to.</div>

| # | Objective (from the syllabus) | Where |
|---|---|---|
| 1 | Explain how a modern computer system is organized and how its parts interact during execution | Previewed today, all semester |
| 2 | Read and reason about assembly-level instructions; explain how instruction set design shapes implementation | Weeks 3-5 |
| 3 | Analyze single-cycle and pipelined datapaths and quantify the cost of hazards | Weeks 6-7, 9-10 |
| 4 | Evaluate cache and virtual memory designs and their effect on access time | Weeks 11-12 |
| 5 | Explain instruction-level, thread-level, and data-level parallelism in modern designs | Week 13 |

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: where did this whole field come from?</div>

---

<!-- SLOT 8: Origin -->

# This Problem Is Not New

<div class="thread">You just felt the pain. Now: who else felt it, and what did the field do about it?</div>

- **1945:** John von Neumann describes the stored-program computer, a single memory holding both instructions and data. Nearly every computer since, including the laptops in the story, is still built on this idea
- **1965:** Gordon Moore observes that transistor counts double roughly every two years. For four decades, chipmakers used that growth mostly to push clock speed higher and higher

<div class="why">
Around 2004, the "MHz race" hit a wall: pushing clock speed any higher
made chips too hot to cool affordably. The industry's answer was not a
faster single core, it was **more cores running in parallel**. That
single decision is why "same GHz" no longer means "same speed," and it
is why Week 13 exists.
</div>

---

# Sixty Years of the Same Underlying Question

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1945</div><div class="d">Von Neumann architecture<br>one memory, instructions and data</div></div>
<div class="pt"><div class="dot"></div><div class="y">1965</div><div class="d">Moore's Law<br>transistor counts, doubling</div></div>
<div class="pt"><div class="dot"></div><div class="y">~2004</div><div class="d">The power wall<br>clock speed stalls, multicore begins</div></div>
<div class="pt"><div class="dot"></div><div class="y">Today</div><div class="d">Multicore CPUs, GPUs, AI accelerators<br>same principles, still evolving</div></div>
</div>

Every era asked the same question: how do we make programs run faster,
given the physical limits of the moment? This course teaches you to
answer it precisely, not by guessing from a spec sheet.

---

<!-- SLOT 9: Core concept -->

# Computer Architecture: Definition

<div class="thread">Sixty years of engineering point at one precise field. Here it is.</div>

> **Computer architecture** is the design of a computer system as seen
> from three linked layers: the instruction set architecture (what
> software sees), the microarchitecture (how it is implemented), and the
> physical hardware (how it is built).

- **Instruction Set Architecture (ISA):** the contract between software and hardware, the set of instructions a processor understands
- **Microarchitecture:** one specific way of implementing that ISA in circuitry, timing, and internal design
- **Hardware:** the actual transistors, wires, and physical chip

Two laptops can share the same ISA (so the same software runs on both)
while having completely different microarchitectures. That gap is
exactly what the story on the first slide was hiding.

---

<!-- Act 3 / BUILD -->

# The Abstraction Stack: What Software Sees (1/2)

<div class="thread">One definition, six concrete layers. Here is the top half: what a programmer sees.</div>

<div class="stack">
<div class="layer view"><span class="h">Application</span> <span class="s">the video editor, the game, the app you actually use</span></div>
<div class="layer view"><span class="h">Operating System</span> <span class="s">schedules programs, manages memory and devices</span></div>
<div class="layer logical"><span class="h">Instruction Set Architecture</span> <span class="s">the fixed vocabulary of instructions: this course's Weeks 3-5</span></div>
</div>

Everything above the ISA line is software's problem. Everything below
it is this course's problem.

---

# The Abstraction Stack: How It's Built (2/2)

<div class="thread">The bottom half: how one ISA actually gets implemented in silicon.</div>

<div class="stack">
<div class="layer logical"><span class="h">Microarchitecture</span> <span class="s">the datapath and pipeline that execute those instructions: Weeks 6-10</span></div>
<div class="layer physical"><span class="h">Logic Gates</span> <span class="s">AND, OR, adders, registers, built from your Digital Logic course</span></div>
<div class="layer physical"><span class="h">Transistors</span> <span class="s">the physical devices switching on and off, billions per chip</span></div>
</div>

This course lives mainly in the middle two layers: ISA and
microarchitecture. That is exactly where the two laptops differed.

---

# The ISA Is a Menu, Not a Kitchen

<div class="thread">One layer from the stack, zoomed in, with an analogy that makes it concrete.</div>

**The ISA is the contract.** It lists what a processor can be asked to
do (add, load, branch), the same way a restaurant menu lists what can be
ordered, without saying anything about how the kitchen prepares it.

<div class="why">
Two restaurants can serve an identical menu from completely different
kitchens, one fast, one slow. Two laptops can run the exact same
software, the same "menu," from completely different internal designs,
one fast, one slow. Neither the menu nor the box's clock-speed number
tells you which kitchen you are getting.
</div>

---

# Preview: A Number That Actually Explains the Gap

<div class="thread">The abstraction stack explains where the difference lives. Next week gives it a number.</div>

Two processors at the same clock speed can still need a different
number of clock cycles to finish the same instruction, because their
microarchitectures are different "kitchens." A processor that needs
fewer cycles per instruction finishes the same program faster, even at
an identical GHz rating.

<div class="why">
This single idea, cycles needed per instruction, is precisely why the
expensive SmartPick laptop won the video-export race. Week 2 turns this
sentence into a formula you can compute with.
</div>

---

# Demo, Step by Step: Decoding a Real Spec Sheet

<div class="thread">Four steps, one real listing page, applying everything from the last four slides.</div>

**Step 1 of 4: Read the raw listing, as a customer would.**

| Spec line | Value laptop | Studio laptop |
|---|---|---|
| Processor | 3.0 GHz, 8 cores | 3.0 GHz, 8 cores |
| Released | 2019 generation | 2023 generation |
| Cache | 8 MB | 24 MB |

At a glance, the top row makes them look identical.

---

# Demo, Step by Step: Decoding a Real Spec Sheet

**Step 2 of 4: Separate what the ISA guarantees from what it doesn't.**

Both list "8 cores, 3.0 GHz," and both run the same Windows software:
same ISA family, so the same programs install and run on either machine.
The ISA guarantees compatibility. It says nothing about speed.

---

# Demo, Step by Step: Decoding a Real Spec Sheet

**Step 3 of 4: Find the line the box doesn't advertise loudly.**

"Released 2019" versus "Released 2023" is a proxy for a different
microarchitecture generation, four years of design improvements. The
cache size difference (8 MB vs 24 MB) is a direct microarchitecture
detail: more cache means fewer slow trips to main memory per
instruction, on average.

---

# Demo, Step by Step: Decoding a Real Spec Sheet

**Step 4 of 4: State what is still missing.**

We can now say, correctly, that Studio's newer microarchitecture and
larger cache are why it wins, not its clock speed. What we still
**cannot** do is put a number on the gap, or predict it for a laptop
that has not been benchmarked yet. That precise number is Week 2.

---

# Case Study: Meet the Running Example

<div class="thread">The stack above is abstract. Here is the concrete pair this whole course keeps coming back to.</div>

This semester, most worked examples return to **SmartPick's two
laptops**, "Value" and "Studio":

<div class="chip-row">
<span class="chip">Value: 3.0 GHz</span>
<span class="chip">Studio: 3.0 GHz</span>
<span class="chip">Same ISA (x86-64)</span>
<span class="chip">Different microarchitecture</span>
</div>

Week 2 assigns both machines real numbers (instruction count, cycles per
instruction) and computes, precisely, why Studio wins. Later weeks
reopen this same pair for pipelining, cache size, and core count.

---

# Where This Field Shows Up Around You

<div class="thread">You just met one running example. Here is where the same questions live in products you already use.</div>

<div class="appgrid">
<div class="app"><div class="name">Smartphone SoC</div><div class="desc">a whole computer architecture on one chip, battery-limited</div></div>
<div class="app"><div class="name">Cloud servers (AWS, Naver Cloud)</div><div class="desc">renting exactly the right CPU generation, at scale</div></div>
<div class="app"><div class="name">Gaming GPU</div><div class="desc">thousands of simple cores, parallel by design</div></div>
<div class="app"><div class="name">AI accelerators (TPU, NPU)</div><div class="desc">chips built specifically to run neural networks fast</div></div>
<div class="app"><div class="name">Automotive / embedded chips</div><div class="desc">real-time constraints, safety-critical timing</div></div>
</div>

Every one of these is a different answer to the same question this
course teaches: given a fixed budget of transistors and power, how do
you design the fastest possible machine?

---

# Who Actually Designs This

<div class="thread">A field this old has specialized roles. Here is who does what.</div>

- **Computer architects:** design the ISA and microarchitecture trade-offs (this course's core focus)
- **Compiler engineers:** translate source code into the ISA's instructions as efficiently as possible
- **Chip / hardware engineers:** turn a microarchitecture design into physical silicon
- **Systems / performance engineers:** measure real workloads and choose the right hardware for the job, exactly the SmartPick clerk's job, done rigorously

---

# Common Mistakes

- **"Higher GHz always means faster":** clock speed is only one factor; cycles needed per instruction matters just as much, as the SmartPick story showed
- **"Architecture is just hardware, software doesn't matter":** compilers and instruction set design shape performance just as much as circuitry does
- **"More cores always means faster":** a program that cannot be split into independent pieces gains little from extra cores; Week 13 makes this precise

---

# Check Yourself

1. Two laptops advertise the same clock speed but finish the same task at very different speeds. Name one architectural reason this can happen, using this week's vocabulary.
2. Put these in order, from the software you write to the physical chip: microarchitecture, application, transistors, ISA, logic gates.

---

# Answers

1. They can share the same ISA while having different **microarchitectures**, so one needs fewer clock cycles per instruction than the other, even at the same clock speed.
2. **Application -> ISA -> Microarchitecture -> Logic Gates -> Transistors.**

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: what this map still can't tell us.</div>

---

<!-- Act 3 / BUILD, continued -->

# One More Look at the Whole Machine

<div class="thread">Before closing, connect every layer back to the exact story that opened today.</div>

<div class="pipeline">
<div class="stage"><div class="h">Application</div><div class="s">video export button, clicked</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">ISA</div><div class="s">same instruction set, both laptops</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Microarchitecture</div><div class="s">different "kitchen," different speed</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Transistors</div><div class="s">where the work physically happens</div></div>
</div>

Every remaining week of this course zooms into one stage of this
diagram. When a topic feels disconnected, find it here first.

---

# A Second, Everyday Version of the Same Idea

<div class="thread">One more grounding example, away from laptops entirely, so the idea sticks.</div>

Two food-delivery riders, 배달의민족 and Coupang Eats, both promise "20
minutes or less." One consistently beats the estimate, the other
consistently misses it. Same promise (the "ISA"), different routing,
different bikes, different rider habits (the "microarchitecture"). The
promise never explains the outcome; the implementation underneath it
does.

<div class="why">
Whenever a spec sheet, a delivery app, or a product page makes a
promise, the real question this course trains you to ask is: what is
actually implementing that promise, and how well?
</div>

---

# This Semester's Real Shape

<div class="thread">Six layers, sixty years of history, one running example. Here is the order you will build it in.</div>

<div class="pipeline">
<div class="stage"><div class="h">Measure</div><div class="s">performance metrics<br>Week 2</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Represent</div><div class="s">data, bits<br>Week 3</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Instruct</div><div class="s">the ISA<br>Weeks 4-5</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Execute</div><div class="s">datapath, pipeline<br>Weeks 6-10</div></div>
<div class="arrow">&rsaquo;</div>
<div class="stage"><div class="h">Remember &amp; Parallelize</div><div class="s">memory, cores<br>Weeks 11-13</div></div>
</div>

Every station on this line answers one more piece of "why was Studio
faster than Value."

---

<!-- SLOT 14: Limits (Act 4 / CLOSE), becomes Week 2 slot 4 -->

# What Today's Map Cannot Do Yet

<div class="limits">
We now have the vocabulary and the layered map: ISA, microarchitecture,
hardware. But we still cannot put an actual number on which machine is
faster, or by how much, or why. Knowing the layers exist is not the
same as being able to measure them.
</div>

---

<!-- SLOT 15: Bridge -->

# Next Week

Week 1 leaves **how to measure and compare performance precisely**
unsolved. **Week 2, Performance and Cost**, addresses it: CPU time,
clock rate, CPI, and Amdahl's Law, the exact tools to settle the
SmartPick argument with numbers instead of a stopwatch.

---

<!-- SLOT 16: Summary -->

# Summary

- Computer architecture spans three linked layers: ISA, microarchitecture, and hardware, with logic gates and transistors underneath
- Identical clock speed does not guarantee identical performance, because microarchitecture differs even when the ISA does not
- The power wall around 2004 shifted the field from raw clock speed to multicore and parallelism, this course's final major topic
- **Reading:** Hennessy & Patterson, 6th ed., Chapter 1
- **Prepare:** find one real spec sheet (a laptop, a phone) and bring one number from it you cannot yet fully explain

---

<!-- SLOT 17: Thank You -->
<!-- _class: end -->

# Thank You
