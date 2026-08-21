# Week 11 Worksheet: How Fast Is Memory, Really?

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the instructor can follow your thinking.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

Recall SmartPick's two laptops from Week 1: same clock speed, same core
count, but very different real speed. **Do not look ahead to Part B
yet.**

| Spec line | Laptop "Value" | Laptop "Studio" |
|---|---|---|
| Processor speed | 3.0 GHz | 3.0 GHz |
| Cores | 8 | 8 |
| Cache size | 8 MB | 24 MB |
| Video export time (Week 1 result) | ~3 min 50 sec | ~1 min 25 sec |

**A1.** In your own words, what does a "cache hit" mean?

`________________________________________________________________`

**A2.** In your own words, what does a "cache miss" mean?

`________________________________________________________________`

**A3.** Prediction: which laptop's cache probably has the **higher hit
rate**? Circle one.

**Value** &nbsp;&nbsp;&nbsp;&nbsp; **Studio** &nbsp;&nbsp;&nbsp;&nbsp; **Cannot tell**

**A4.** In 1-2 sentences, explain *why* you predicted that, using the
word "locality" if you can.

`________________________________________________________________`
`________________________________________________________________`

**A5.** If a cache miss happens, where does the processor get the data
from instead, and is that fetch fast or slow?

`________________________________________________________________`

*Stop here. We compare predictions together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your instructor will hand this out after the class discussion of Part A.
It gives you real numbers to work with.

**The numbers.** Assume both laptops have a hit time of 1 ns and a miss
penalty of 100 ns. Value's cache reaches an 80% hit rate. Studio's
larger cache reaches a 95% hit rate.

**B1.** Fill in the missing values.

| | Value laptop | Studio laptop |
|---|---|---|
| Hit rate | 80% | 95% |
| Miss rate | ______ | ______ |
| AMAT | ______ ns | ______ ns |

**B2.** About how many times faster is Studio's AMAT compared to
Value's? (A rough number is fine.)

`________________________________________________________________`

**B3.** Using the words **hit rate** and **AMAT**, explain in 1-2
sentences why Studio's bigger cache leads to a faster video export.

`________________________________________________________________`
`________________________________________________________________`

**B4.** Sort these into the correct miss type: **compulsory**,
**capacity**, or **conflict**.

- The very first time the program reads a file: `______________`
- The program's data no longer fits in a small cache: `______________`

**B5 (stretch, optional).** A friend says: "I'll just buy the laptop
with the biggest cache number, no matter the price." Write one sentence
of advice for your friend, using an idea from this week.

`________________________________________________________________`

---
---

# Instructor Answer Key — do not hand out this section

## Part A — what to listen for

There is no single "correct" prediction expected in Part A — the point
is to surface reasoning, not to get it right yet. Common good answers:

- **A1:** the processor asks for data and finds it already in the cache, so the answer is fast
- **A2:** the processor asks for data and it is not in the cache, so the answer is slow
- **A3/A4:** Accept any prediction if the reasoning is coherent. Many pairs will correctly guess "Studio," reasoning from the bigger cache size seen in Week 1. Some may say "cannot tell" without a hit-rate number yet — that is a reasonable, honest answer at this stage
- **A5:** the processor fetches the data from main memory (RAM), and that fetch is much slower than a cache hit

## Part B — model answers

- **B1:** Value miss rate = 20%, AMAT = 1 + (0.20 × 100) = **21 ns**. Studio miss rate = 5%, AMAT = 1 + (0.05 × 100) = **6 ns**
- **B2:** roughly **3.5 times faster** (21 / 6 ≈ 3.5)
- **B3 (model answer):** "Studio's bigger cache reaches a higher hit rate, so it needs far fewer slow trips to main memory. That lowers its AMAT, and a lower AMAT means less waiting on every single memory request, which adds up across a whole video export."
- **B4:** first-time file read = **compulsory**; data no longer fits = **capacity**
- **B5 (model answer):** "A bigger cache usually helps, but past a point it barely raises the hit rate while still costing more money and chip space — so check the actual hit rate or benchmark, not just the cache size number."

## Facilitation notes

- Total time: Part A ~15 min (prediction only, no reveal), short instructor-led discussion, Part B ~15 min (real numbers + explain)
- Do not let Part A run long — the value is in reasoning from Week 1's story, not in getting the "right" number
- If a pair finishes Part B early, point them to the handout's "Optional Reading" section
