# Professor Answer Key — do not hand out this section

## Part A — what to listen for

There is no single "correct" prediction expected in Part A — the point
is to surface reasoning, not to get it right yet. Common good answers:

- **A1 (identical):** clock speed (3.2 GHz), core count (8), disk size (512 GB SSD), price is different (do not accept as identical)
- **A2 (different):** RAM (8 GB vs 32 GB), price
- **A3/A4:** Accept any prediction if the reasoning is coherent. Many pairs will guess "Pro, because it costs more" or "cannot tell, the processor is the same" — both are reasonable starting points. Do **not** confirm or deny the answer yet
- **A5:** Good answers notice that disk storage and RAM are not the same thing — a project can "fit" on disk (as a file) while still being far too big to fit as *active, in-use data* inside RAM while editing. Any answer that separates "file storage" from "working memory" is a success

## Part B — model answers

- **B1:** Depends on their Part A guess; there is no wrong answer here, just self-checking
- **B2 (model answer):** "Basic only has 8 GB of RAM, so most of the 40 GB project cannot stay in RAM at once. Virtual memory keeps it working by constantly moving pages to and from disk, and each of those page faults costs real time, which is why it feels sluggish."
- **B3 (model answer):** "A big disk only stores the file — it does not speed up how fast the *active* parts of that file can be reached while editing; RAM size decides that."
- **B4 (model answer):** "Just like ISA alone did not explain Week 1's speed gap, clock speed and cores alone do not explain this one — how much data fits close to the processor, in RAM, matters just as much as how fast the processor itself runs."
- **B5 (model answer):** "It would very likely fail to open, or the operating system would refuse to run the program, because virtual memory has nowhere left to put pages that do not fit in RAM — there is no overflow space at all."

## Facilitation notes

- Total time: Part A ~15 min (prediction only, no reveal), short professor-led discussion, Part B ~15 min (reveal + explain)
- Do not let Part A run long — the value is in making a prediction under uncertainty, not in getting the "right" answer
- If a pair finishes Part B early, point them to the handout's "Optional Reading" section
