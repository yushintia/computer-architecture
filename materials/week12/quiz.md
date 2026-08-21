# Week 12 Self-Check Quiz (Ungraded)

Computer Architecture (503872-004). This quiz is **ungraded** — it is
only to help you check what stuck. About 10 minutes. Do not look back at
the slides while you answer.

---

**1.** What does virtual memory give each running program?

A. A faster processor
B. Its own large, private view of memory
C. A copy of the operating system
D. More disk storage space

**2.** What is a page table used for?

A. Storing a program's source code
B. Mapping a program's virtual pages to real physical memory frames
C. Listing which programs are currently running
D. Measuring clock speed

**3.** What is a page fault?

A. A bug in a program's code
B. The pause when a needed page is only on disk, not in RAM
C. A crash caused by too many cores
D. An error in the page table's formatting

**4.** Roughly how much slower is a page fault compared to a RAM access?

A. About the same speed
B. About 10 times slower
C. About 1,000 times slower
D. About 2 times slower

**5.** Why can two programs both use virtual address 4,200 at the same
time without colliding?

A. The operating system deletes one of them
B. Each program has its own separate page table, mapping the address to a different physical frame
C. Virtual addresses are always unique across programs
D. Only one program is allowed to run at a time

**6.** What is the TLB (Translation Lookaside Buffer)?

A. A backup copy of a program's data
B. A small, fast cache of recent address translations
C. The part of the disk that stores swap space
D. A tool for measuring clock speed

**7.** A laptop's project needs more active data than the installed RAM
can hold. What does virtual memory do?

A. Refuses to open the project
B. Deletes part of the project automatically
C. Keeps it running, but slower, by swapping pages to and from disk
D. Increases the RAM automatically

**8. (Short answer)** In 1-2 sentences, explain why adding more RAM to a
laptop can make a large project run noticeably faster. Use at least one
key word from this week (page fault, page table, virtual memory).

`_____________________________________________________________`
`_____________________________________________________________`

---
---

# Answer Key

1. **B** — virtual memory gives each program its own large, private view of memory
2. **B** — the page table maps a program's virtual pages to real physical memory frames, or marks them as on disk
3. **B** — a page fault is the pause when a needed page is only on disk, not currently in RAM
4. **C** — roughly 1,000 times slower (RAM ~100 nanoseconds, disk ~100,000 nanoseconds)
5. **B** — each program has its own page table, so the same virtual address maps to a different, private physical frame per program
6. **B** — the TLB is a small, fast cache of recent address translations, so most lookups skip the full page table
7. **C** — virtual memory keeps the project running by swapping pages between RAM and disk, at the cost of speed
8. **Model answer:** "More RAM means more of the project's active data fits directly in RAM, so the operating system needs far fewer page faults, and the program spends far less time waiting on slow disk trips."
