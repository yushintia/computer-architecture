# Answer Key

1. **B** — virtual memory gives each program its own large, private view of memory
2. **B** — the page table maps a program's virtual pages to real physical memory frames, or marks them as on disk
3. **B** — a page fault is the pause when a needed page is only on disk, not currently in RAM
4. **C** — roughly 1,000 times slower (RAM ~100 nanoseconds, disk ~100,000 nanoseconds)
5. **B** — each program has its own page table, so the same virtual address maps to a different, private physical frame per program
6. **B** — the TLB is a small, fast cache of recent address translations, so most lookups skip the full page table
7. **C** — virtual memory keeps the project running by swapping pages between RAM and disk, at the cost of speed
8. **Model answer:** "More RAM means more of the project's active data fits directly in RAM, so the operating system needs far fewer page faults, and the program spends far less time waiting on slow disk trips."
