# Week 13 Self-Check Quiz (Ungraded)

Computer Architecture (503872-004). This quiz is **ungraded** — it is
only to help you check what stuck. About 10 minutes. Do not look back at
the slides while you answer. (This is separate from today's in-class
Quiz 2.)

---

**1.** What does "parallelism" mean, in this course's plain-language
definition?

A. Making a single core run at a higher clock speed
B. Doing more than one piece of work at the same time, on more than one worker
C. Writing a program using fewer lines of code
D. Storing data in a faster type of memory

**2.** A laptop doubles its core count from 8 to 16, but a task only
gets a little faster, not twice as fast. What is the most likely reason?

A. The extra cores are defective
B. The task has a serial part that does not shrink, no matter how many cores help
C. Clock speed dropped when cores were added
D. The operating system does not support more than 8 cores

**3.** What best describes data-level parallelism?

A. Different workers doing completely different jobs at once
B. One core running two operating systems at once
C. The same operation repeated across many pieces of data at once
D. Splitting a program's code into smaller files

**4.** Using Speedup(N) = 1 / (S + P/N), a task is 100% parallel
(S = 0, P = 1). What is its speedup on 8 workers?

A. 1x
B. 4x
C. 8x
D. 16x

**5.** Using the same formula, a task is 100% serial (S = 1, P = 0).
What is its speedup on 8 workers?

A. 1x
B. 4x
C. 8x
D. It cannot be computed

**6.** Which task is the best fit for a GPU's data-level parallelism?

A. Deciding a game's next move, which depends on the previous move
B. Brightening every pixel of a large photo
C. Reading one file from disk, one time
D. Running a single line of setup code once

**7.** What is "coordination overhead"?

A. The cost of buying more cores
B. Extra time workers spend communicating or waiting, instead of computing
C. The advertised clock speed of a chip
D. A type of virtual memory error

**8. (Short answer)** In 1-2 sentences, explain why a task's serial
fraction limits how much speedup extra workers can ever provide. Use at
least one key word from this week (serial, parallel, speedup, or
coordination).

`_____________________________________________________________`
`_____________________________________________________________`

---
---

# Answer Key

1. **B** — parallelism means doing more than one piece of work at the
   same time, on more than one worker
2. **B** — the task's serial part takes the same fixed time no matter
   how many cores handle the parallel part, capping the total speedup
3. **C** — data-level parallelism repeats the same operation across
   many independent pieces of data
4. **C** — Speedup = 1 / (0 + 1/8) = 8x, a perfect, proportional
   speedup when the task is fully parallel
5. **A** — Speedup = 1 / (1 + 0) = 1x; a fully serial task gains
   nothing from extra workers
6. **B** — brightening every pixel is the same repeated operation over
   many independent data items, exactly what GPUs are built for
7. **B** — coordination overhead is the extra time workers spend
   communicating or waiting, instead of computing
8. **Model answer:** "The serial part must happen one step at a time and
   takes the same amount of time no matter how many workers are added,
   so as more workers speed up the parallel part, the fixed serial part
   makes up a bigger share of the total time and caps the overall
   speedup."
