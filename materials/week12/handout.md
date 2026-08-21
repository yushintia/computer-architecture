# Week 12 Handout: Memory Hierarchy II (Virtual Memory)

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **Physical memory (RAM)** | The fast, chip-based memory a running program actually uses. Always limited in size |
| **Address** | A number that names one exact spot in memory |
| **Disk / storage** | Bigger, slower storage that keeps files even when the power is off |
| **Out of memory** | What happens when a program needs more memory than the machine has |
| **Virtual memory** | A technique that gives each running program its own large, private view of memory |
| **Virtual address** | The address a program uses when it asks for data. Not the real chip location |
| **Physical address** | Where a piece of data actually sits inside real RAM |
| **Page** | A small, fixed-size chunk of a program's virtual memory, often 4 KB |
| **Page frame** | A chunk the same size as a page, but inside real physical RAM |
| **Page table** | The list that maps a program's pages to real physical frames, or marks them as "on disk" |
| **TLB (Translation Lookaside Buffer)** | A small, fast cache of recent address translations, so most lookups skip the full page table |
| **Page fault** | The pause that happens when a program needs a page that is only on disk, not in RAM |
| **Thrashing** | When a machine spends most of its time swapping pages instead of doing real work |
| **Swap space** | The area of disk set aside to hold pages moved out of RAM |
| **Isolation** | Keeping one program's memory completely separate from another's |
| **One-level store** | The original 1959-1962 name for virtual memory, invented for the Atlas computer |

---

## 2. The SmartPick Story, Worked Out Step by Step

This is the full version of the story from class. Read it slowly if the
in-class pace felt fast.

**The situation.** A SmartPick customer buys the Studio laptop, which has
16 GB of real RAM, to edit video. With a small project, everything is
fast. As she adds more clips, it slows down badly, even though nothing
about the laptop changed.

| Stage | Active data needed | Fits in 16 GB RAM? | Result |
|---|---|---|---|
| 10 clips | ~6 GB | Yes | Fast, almost no page faults |
| 50 clips | ~40 GB | No | Constant page faults, slow |

**Step 1: What stayed the same?** The laptop's RAM is still 16 GB. Its
processor did not get slower. Nothing broke.

**Step 2: What changed?** The project's **active data** grew from about 6
GB to about 40 GB. Once that active data no longer fits inside 16 GB of
RAM, the operating system must start using **virtual memory**'s overflow
path: moving pages out to disk to make room, and back in when needed.

**Step 3: Why does this feel so slow?** A RAM access takes roughly 100
nanoseconds. A page fault, which needs a trip to disk, takes roughly
100,000 nanoseconds — about a thousand times slower. A large project can
trigger thousands of page faults in a single editing session, and each
one adds this real delay.

**Step 4: Does virtual memory fail here?** No. It keeps the project
running at all, even though the data does not physically fit in RAM. That
is exactly virtual memory's job: it trades speed for capacity when it has
to. It does not fail, it just gets slower.

**Step 5: What actually fixes the slowdown?** More RAM. With 64 GB of
RAM, the same 40 GB project fits entirely, page faults drop from roughly
300 per minute to roughly 10 per minute, and editing feels fast again.
Virtual memory itself did not change — it simply has to reach for the
disk far less often.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations that were trimmed from the slides
to keep class time short. Read it if you are curious or want more
examples.

**Virtual memory is a promise, not a place.** A program is told: "you
have this much memory, and it is all yours." That promise is virtual
memory. Where the data actually sits — a fast RAM frame, or a slow disk
page — is a decision the operating system makes silently, moment by
moment, without the program ever asking.

**A library card catalog, as an everyday version of a page table.** You
look up a book by its title, not by which physical shelf it sits on. The
card catalog translates title to shelf location for you. A page table
does the same thing for a program: translate a virtual page number to a
physical location, without the program needing to know or care where the
data really lives.

**Isolation is also a security tool.** Because each program gets its own
page table, one program cannot simply reach into another program's
memory and read its data, even by accident. Many real computer-security
attacks are exactly an attempt to trick the hardware into breaking this
separation. This is why "memory isolation" appears often in security job
postings, not only performance ones.

**Where this shows up around you.**

- **Web browsers:** each tab gets separated memory, so one crashing tab does not take down the whole browser
- **Cloud servers:** one physical machine safely runs many customers' programs side by side, each isolated
- **Phones and laptops:** every open app gets its own private page table, all managed automatically
- **Databases:** very large datasets use virtual memory and disk together when they outgrow RAM

**Who actually designs this, as a job.**

- **Operating-system engineers** build and tune the page-fault handling and page-replacement logic this course only sketches
- **Computer architects** design the hardware (page tables, TLBs) that makes translation fast enough to be invisible
- **Security engineers** look for ways this isolation can be broken, and for ways to make it stronger
- **Systems / performance engineers** decide how much RAM a real server needs, so it rarely has to touch the disk at all

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** In one sentence, explain what a page table does.
> **Answer:** A page table maps a program's virtual pages to real physical
> memory frames, or marks a page as being only on disk.

**Problem 2.** A program asks for virtual address 4,200. Does that number
tell you where the data physically sits in RAM? Why or why not?
> **Answer:** No. The virtual address is only what the program sees. The
> page table translates it into the real physical location, which the
> program never needs to know.

**Problem 3.** RAM access takes about 100 nanoseconds. A page fault takes
about 100,000 nanoseconds. Roughly how many times slower is a page fault?
> **Answer:** About 1,000 times slower (100,000 ÷ 100 = 1,000).

**Problem 4.** Two programs both use virtual address 4,200 at the same
time on the same laptop. Explain why they do not read or write each
other's data.
> **Answer:** Each program has its own separate page table, so the same
> virtual address maps to a different physical frame for each program.

**Problem 5.** A laptop's video project needs 40 GB of active data, but
the laptop only has 16 GB of RAM. Does the project fail to open? Explain.
> **Answer:** No, it still opens. Virtual memory keeps it running by
> swapping pages between RAM and disk, but it runs much slower because of
> the added page faults.

**Problem 6.** Name one everyday app or task (not from the slides) where
virtual memory quietly does its job. Explain briefly.
> **Answer (example):** A phone running many apps at once — messaging,
> music, a map — relies on virtual memory to keep each app's memory
> separate and to let the total memory used exceed the phone's installed
> RAM.
