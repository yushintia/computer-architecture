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
