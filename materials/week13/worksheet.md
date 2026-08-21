# Week 13 Worksheet: The Photo Kiosk Speedup

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the instructor can follow your thinking. Formula reminder:

> **Speedup(N) = 1 / (S + P / N)**, where S is the serial fraction, P is
> the parallel fraction, S + P = 1, and N is the number of workers.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

SmartPick's print kiosk runs a **Batch Photo Filter** job on 200 photos.
Applying the filter to each photo can be split across cores. Saving the
final, combined print-ready file must happen only after every photo is
filtered, one step at a time.

For this job: **S = 0.10** (10% serial), **P = 0.90** (90% parallel).

**A1.** Which part of the job is the **serial** part, and which is the
**parallel** part? Use your own words.

`________________________________________________________________`

**A2.** Using the formula above, compute the speedup for **N = 4**
workers. Show your work.

`________________________________________________________________`
`________________________________________________________________`

**A3.** Prediction, **before you compute it**: if the kiosk doubles its
workers from 4 to 8, will the speedup roughly double too? Circle one.

**Yes, it roughly doubles** &nbsp;&nbsp;&nbsp;&nbsp; **No, it gains less than double** &nbsp;&nbsp;&nbsp;&nbsp; **Not sure**

**A4.** In 1-2 sentences, explain why you predicted that.

`________________________________________________________________`
`________________________________________________________________`

**A5.** The formula assumes splitting the work has no extra cost. Name
one real-world cost it ignores.

`________________________________________________________________`

*Stop here. We compare answers together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your instructor will hand this out after the class discussion of Part A.
It reveals the full table, then asks you to explain it.

**The real numbers**, for S = 0.10, P = 0.90:

| Workers (N) | S + P/N | Speedup |
|---|---|---|
| 1 | 1.00 | 1.0x |
| 2 | 0.55 | ~1.8x |
| 4 | 0.325 | ~3.1x |
| 8 | 0.2125 | ~4.7x |
| 16 | 0.15625 | ~6.4x |

**B1.** Check your Part A answer (A2). Was your computed speedup for
N = 4 correct?

`Yes  /  No  /  Close`

**B2.** Check your Part A prediction (A3). Going from 4 to 8 workers
(2x the workers), did the speedup roughly double?

`________________________________________________________________`

**B3.** In your own words, explain why doubling the workers from 4 to 8
did **not** double the speedup, even though the task is 90% parallel.

`________________________________________________________________`
`________________________________________________________________`

**B4.** A friend says: "I'll just buy the machine with the most cores."
Write one sentence of advice for your friend, using this worksheet's
numbers.

`________________________________________________________________`

**B5 (stretch, optional).** The kiosk's real, measured speedup at 8
workers was only about **4.4x**, slightly below the formula's 4.7x.
What might the simple formula be leaving out?

`________________________________________________________________`

---
---

# Instructor Answer Key — do not hand out this section

## Part A — what to listen for

- **A1:** Serial = saving the final combined file (must happen last, one
  step at a time). Parallel = filtering each of the 200 photos
  (independent, splittable across cores)
- **A2:** Speedup(4) = 1 / (0.10 + 0.90/4) = 1 / (0.10 + 0.225) =
  1 / 0.325 ≈ **3.08x**. Accept small rounding differences
- **A3/A4:** Accept any prediction if the reasoning is coherent. Many
  pairs will guess "roughly double" by intuition (2x workers -> 2x
  speedup); a few may already suspect diminishing returns from class.
  Do **not** confirm or deny yet — that is the point of the prediction
- **A5:** Good answers mention: communication between workers, waiting
  for the slowest worker, combining results, keeping shared data
  consistent (cache coherence, Weeks 11-12). Any answer naming a real
  coordination cost is a success

## Part B — model answers

- **B1:** Should match ≈3.08x from A2, within rounding
- **B2:** No — speedup only went from ~3.1x to ~4.7x, about 1.5x more,
  not 2x more, even though the worker count doubled
- **B3 (model answer):** "The 10% serial part takes the same fixed time
  no matter how many workers help with the other 90%. As workers grow,
  that fixed serial time becomes a bigger and bigger share of the total,
  so each doubling of workers buys a smaller and smaller speedup gain."
- **B4 (model answer):** "More cores help less and less once the task's
  serial part starts to dominate — check the serial fraction before
  assuming more cores means proportionally faster."
- **B5 (model answer):** "The formula assumes perfectly free splitting
  and combining. Real machines pay a coordination cost: workers must
  communicate, wait for the slowest one, and merge partial results,
  which eats into the theoretical speedup, especially as worker count
  grows."

## Facilitation notes

- Total time: Part A ~15 min (prediction + first computation, no full
  reveal), short instructor-led discussion, Part B ~15 min (reveal +
  explain)
- Encourage pairs to actually do the A2 arithmetic; walking around to
  check for the 0.325 denominator catches most calculation slips early
- If a pair finishes Part B early, point them to the handout's "Optional
  Reading" section
