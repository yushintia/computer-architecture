# Week 11 Worksheet: How Fast Is Memory, Really?

Computer Architecture (503872-004). Work with your pair. Write short
answers — full sentences are not required, but write enough that your
partner and the professor can follow your thinking.

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

Your professor will hand this out after the class discussion of Part A.
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
