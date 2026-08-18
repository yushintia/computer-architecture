# Week 1 Handout: Introduction to Computer Architecture

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **Program** | A list of instructions a computer follows, one step at a time |
| **Binary** | A number written using only two digits: 0 and 1 |
| **Clock speed (GHz)** | How many times per second a chip's internal clock "ticks." 1 GHz = one billion ticks per second |
| **Spec sheet** | The list of numbers and features a store shows about a device, like a laptop |
| **Performance** | How fast a machine actually finishes real work, not just the number on the box |
| **Benchmark** | A fair, repeatable test used to measure performance, so different machines can be compared honestly |
| **ISA (Instruction Set Architecture)** | The fixed list of commands a processor understands — the "menu" of what it can be asked to do |
| **Microarchitecture** | One specific way to build a processor that carries out an ISA's commands. Two processors can share an ISA but have very different microarchitectures |
| **Hardware** | The physical chip: real transistors and wires you could touch |
| **Transistor** | A tiny electronic switch. It is either on or off. A modern chip has billions of them |
| **Logic gate** | A small circuit built from transistors (AND, OR, NOT, ...) that does one simple logic operation. You met these in Digital Logic |
| **Cache** | A small amount of very fast memory placed close to the processor, used to avoid slow trips to main memory |
| **Core** | One independent processing unit inside a chip. A chip can have many cores |
| **Multicore** | A chip built with more than one core, so it can do more than one thing at the same time |
| **Parallelism** | Doing more than one piece of work at the same time, instead of one after another |
| **Power wall** | The physical limit that stopped chipmakers from endlessly raising clock speed, because faster chips get too hot |
| **Trade-off** | Gaining one thing (like speed) only by giving up something else (like power use or cost) |
| **Von Neumann architecture** | A computer design where one memory holds both the program's instructions and its data. Almost every computer today still uses this idea |
| **Moore's Law** | The 1965 observation that the number of transistors on a chip roughly doubles every two years |

---

## 2. The SmartPick Story, Worked Out Step by Step

This is the full version of the story from class. Read it slowly if the
in-class pace felt fast.

**The situation.** A customer at SmartPick, the campus electronics store,
is comparing two laptops. Both boxes advertise the exact same clock
speed: **3.0 GHz**. One laptop costs more than the other. She wants to
know why.

**The test.** The store clerk runs the identical task — exporting the
same video file — on both machines, with a stopwatch.

| | Value laptop | Studio laptop |
|---|---|---|
| Advertised speed | 3.0 GHz | 3.0 GHz |
| Cores | 8 | 8 |
| Released | 2019 | 2023 |
| Cache | 8 MB | 24 MB |
| Price | lower | higher |
| **Video export time** | **~3 min 50 sec** | **~1 min 25 sec** |

**Step 1: What is identical?** The advertised clock speed (3.0 GHz) and
the core count (8) are the same on both spec sheets. If you only read the
big numbers, the two laptops look the same.

**Step 2: What does "same ISA" actually guarantee?** Both laptops run
the same operating system and the same software. That means they share
the same **ISA** (instruction set architecture) — the same "menu" of
commands. Sharing an ISA guarantees that the *same software runs on
both*. It says **nothing** about *how fast* it runs.

**Step 3: Find the detail the box does not shout about.** Two lines on
the spec sheet are easy to skip: "Released 2019" vs. "Released 2023,"
and "Cache 8 MB" vs. "Cache 24 MB." The release year is a hint: four
extra years usually means a newer, improved **microarchitecture** — a
different internal design of the same kind of processor. The cache size
is a direct microarchitecture detail: a bigger cache means the processor
needs fewer slow trips out to main memory, on average, so it finishes
work faster.

**Step 4: State clearly what we can, and cannot, say yet.** We *can* now
say, correctly: Studio's newer microarchitecture and bigger cache are
why it wins, not its clock speed. We *cannot* yet put an exact number on
the gap, or predict it for a laptop we have not tested. That precise
number — using **CPU time**, **CPI (cycles per instruction)**, and
**Amdahl's Law** — is what Week 2 teaches.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations that were trimmed from the slides
to keep class time short. Read it if you are curious or want more
examples.

**The ISA is a menu, not a kitchen.** The ISA lists what a processor can
be asked to do — add, load, branch — the same way a restaurant menu
lists what you can order, without saying anything about how the kitchen
actually cooks it. Two restaurants can serve the exact same menu from
very different kitchens, one fast, one slow. Two laptops can run the
exact same software from very different internal designs. Neither the
menu nor the box's GHz number tells you which kitchen you are getting.

**A second, everyday version of the same idea.** Two food-delivery
services both promise "20 minutes or less." One usually beats that
promise; the other usually misses it. The promise is like the ISA — the
same for both. The routing, the vehicles, the drivers' habits are like
the microarchitecture — different for each — and that is what actually
decides the outcome. Whenever something makes a promise (a spec sheet, an
app, a delivery service), the useful question is always: *what is
actually implementing that promise, and how well?*

**Where this shows up around you.**

- **Smartphone chips (SoC):** a whole computer architecture on one small, battery-limited chip
- **Cloud servers (AWS, Naver Cloud):** renting the right processor generation for your workload, at large scale
- **Gaming GPUs:** thousands of simple cores, built for parallel work from the start
- **AI accelerators (TPU, NPU):** chips designed specifically to run neural networks fast
- **Automotive / embedded chips:** must respond in a guaranteed, predictable amount of time

**Who actually designs this, as a job.**

- **Computer architects** design the ISA and microarchitecture trade-offs — this course's core focus
- **Compiler engineers** translate your source code into ISA instructions as efficiently as possible
- **Chip / hardware engineers** turn a microarchitecture design into real, physical silicon
- **Systems / performance engineers** measure real workloads and pick the right hardware for the job — exactly the SmartPick clerk's job, done rigorously

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** Convert the decimal number 13 to binary.
> **Answer:** `1101` (8 + 4 + 0 + 1 = 13)

**Problem 2.** Convert the binary number `1010` to decimal.
> **Answer:** 10 (8 + 0 + 2 + 0)

**Problem 3.** In one sentence, explain what a "program" is, in your own
words.
> **Answer (example):** A program is a list of steps a computer follows,
> in order, to do a task.

**Problem 4.** Two processors have the exact same ISA. Does that mean
they run at the exact same speed? Explain in one sentence.
> **Answer:** No. Sharing an ISA only guarantees the same software runs
> on both; the microarchitecture underneath can still be very different,
> which changes the real speed.

**Problem 5.** Laptop A has an 8 MB cache. Laptop B has a 24 MB cache,
same ISA, same clock speed. Which laptop, on average, makes fewer slow
trips to main memory?
> **Answer:** Laptop B, because a bigger cache holds more data close to
> the processor, so it needs main memory less often, on average.

**Problem 6.** Put these five layers in order, from the code you write
down to the physical chip: `ISA`, `Transistors`, `Application`,
`Microarchitecture`, `Logic Gates`.
> **Answer:** Application -> ISA -> Microarchitecture -> Logic Gates ->
> Transistors.
