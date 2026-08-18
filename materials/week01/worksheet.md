# Week 1 Worksheet: The SmartPick Laptop Mystery

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the instructor can follow your thinking.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

Below are two real-looking spec sheets from SmartPick, the campus
electronics store. **Do not look ahead to Part B yet.**

| Spec line | Laptop "Value" | Laptop "Studio" |
|---|---|---|
| Processor speed | 3.0 GHz | 3.0 GHz |
| Cores | 8 | 8 |
| Released | 2019 | 2023 |
| Cache | 8 MB | 24 MB |
| Price | $600 | $950 |

**A1.** List everything that is **identical** between the two spec
sheets.

`________________________________________________________________`

**A2.** List everything that is **different** between the two spec
sheets.

`________________________________________________________________`

**A3.** Prediction: which laptop finishes the same video-export task
faster? Circle one.

**Value** &nbsp;&nbsp;&nbsp;&nbsp; **Studio** &nbsp;&nbsp;&nbsp;&nbsp; **Cannot tell**

**A4.** In 1-2 sentences, explain *why* you predicted that.

`________________________________________________________________`
`________________________________________________________________`

**A5.** What is one piece of information you wish the spec sheet
included, that it does not?

`________________________________________________________________`

*Stop here. We compare predictions together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your instructor will hand this out after the class discussion of Part A.
It starts with the real answer, then asks you to explain it.

**The real result:** Value finishes the video export in about **3
minutes 50 seconds**. Studio finishes it in about **1 minute 25
seconds** — more than twice as fast.

**B1.** Was your Part A prediction correct?

`Yes  /  No  /  Partly`

**B2.** Using the words **ISA** and **microarchitecture**, explain in
1-2 sentences why Studio is faster even though the GHz number is the
same on both.

`________________________________________________________________`
`________________________________________________________________`

**B3.** Two spec lines were different: "Released" and "Cache." One of
these is a **direct** microarchitecture detail. The other is only a
**hint** that the microarchitecture is probably different. Which is
which?

`________________________________________________________________`

**B4.** A friend tells you: "I'll just always buy the laptop with the
highest GHz number." Write one sentence of advice for your friend.

`________________________________________________________________`

**B5 (stretch, optional).** Can we say *exactly* how many seconds faster
Studio will be on a completely different task, like photo editing? Why
or why not?

`________________________________________________________________`

---
---

# Instructor Answer Key — do not hand out this section

## Part A — what to listen for

There is no single "correct" prediction expected in Part A — the point
is to surface reasoning, not to get it right yet. Common good answers:

- **A1 (identical):** clock speed (3.0 GHz), core count (8)
- **A2 (different):** release year (2019 vs 2023), cache size (8 MB vs 24 MB), price
- **A3/A4:** Accept any prediction if the reasoning is coherent. Many pairs will guess "Studio, because it's more expensive" or "cannot tell, the numbers look the same" — both are reasonable starting points. Do **not** confirm or deny the answer yet; that is the point of the "we cannot tell yet" moment
- **A5:** Good answers mention: benchmark scores, actual test results, microarchitecture generation/name, RAM speed, cooling design. Any answer showing they want *more than the advertised number* is a success

## Part B — model answers

- **B1:** Depends on their Part A guess; there is no wrong answer here, just self-checking
- **B2 (model answer):** "Both laptops share the same ISA, so the same software runs on both. But they have different microarchitectures — different internal designs — and Studio's design needs fewer steps to finish the same work, which is why it is faster even at the same GHz."
- **B3:** Cache size is the **direct** microarchitecture detail (it is literally part of the chip's internal design). Release year is only a **hint** — a newer release usually, but not always, means an improved microarchitecture
- **B4 (model answer):** "GHz alone does not tell you real speed — ask for benchmark results or the release year and cache size instead."
- **B5 (model answer):** "No, we cannot give an exact number yet. We know *that* Studio is faster and roughly *why* (better microarchitecture, bigger cache), but turning that into a precise, predictable number for a new task requires tools we have not learned yet — CPU time, CPI, and Amdahl's Law, which is exactly what Week 2 teaches. This 'we cannot tell yet' feeling is intentional: it is the reason the rest of the course exists."

## Facilitation notes

- Total time: Part A ~15 min (prediction only, no reveal), short instructor-led discussion, Part B ~15 min (reveal + explain)
- Do not let Part A run long — the value is in making a prediction under uncertainty, not in getting the "right" answer
- If a pair finishes Part B early, point them to the handout's "Optional Reading" section
