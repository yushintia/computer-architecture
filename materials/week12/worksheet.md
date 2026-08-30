# Week 12 Worksheet: How Much Memory Is Enough?

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the professor can follow your thinking.

**Pair names:** ___________________________ / ___________________________

---

## Part A (do this in 차시 2, about 15 minutes)

Below are two real-looking spec sheets from SmartPick, the campus
electronics store. Both laptops will run the same 40 GB video-editing
project. **Do not look ahead to Part B yet.**

| Spec line | Laptop "Basic" | Laptop "Pro" |
|---|---|---|
| Processor speed | 3.2 GHz | 3.2 GHz |
| Cores | 8 | 8 |
| RAM (physical memory) | 8 GB | 32 GB |
| Storage (disk) | 512 GB SSD | 512 GB SSD |
| Price | $700 | $1,050 |

**A1.** List everything that is **identical** between the two spec
sheets.

`________________________________________________________________`

**A2.** List everything that is **different** between the two spec
sheets.

`________________________________________________________________`

**A3.** Prediction: which laptop handles the 40 GB video project better?
Circle one.

**Basic** &nbsp;&nbsp;&nbsp;&nbsp; **Pro** &nbsp;&nbsp;&nbsp;&nbsp; **Cannot tell**

**A4.** In 1-2 sentences, explain *why* you predicted that.

`________________________________________________________________`
`________________________________________________________________`

**A5.** Both laptops have the exact same amount of disk (SSD) storage.
Does that mean the 40 GB project will always fit and open fine on both?
Why or why not?

`________________________________________________________________`

*Stop here. We compare predictions together before you see Part B.*

---

## Part B (do this in 차시 3, about 15 minutes)

Your professor will hand this out after the class discussion of Part A.
It starts with the real answer, then asks you to explain it.

**The real result:** Both laptops can open the 40 GB project — neither
one crashes or refuses. But Basic (8 GB RAM) pages heavily to disk and
feels sluggish, with clips taking many seconds to open. Pro (32 GB RAM)
stays close to smooth, with only occasional, brief pauses.

**B1.** Was your Part A prediction correct?

`Yes  /  No  /  Partly`

**B2.** Using the words **virtual memory** and **page fault**, explain in
1-2 sentences why Basic feels sluggish even though it never actually
crashes.

`________________________________________________________________`
`________________________________________________________________`

**B3.** A friend says: "If the laptop has a big enough hard disk, RAM size
does not matter." Write one sentence explaining what this friend is
getting wrong.

`________________________________________________________________`

**B4.** Both laptops share the exact same ISA and clock speed, like
Value and Studio did back in Week 1. Explain, in one sentence, why RAM
size can still change real performance this much, even with everything
else the same.

`________________________________________________________________`

**B5 (stretch, optional).** Suppose SmartPick sold a laptop with 8 GB of
RAM and *no* disk at all to swap pages to. What would happen when the 40
GB project tried to open? Why?

`________________________________________________________________`
