---
marp: true
theme: shintia
paginate: true
footer: 'Department of Intelligent Computing'
---

<!-- SLOT 1: Title -->
<!-- _class: title -->

# Week 3: Data Representation

<span class="subtitle">Computer Architecture (503872-004)</span>

<div class="meta">
Yushintia Pramitarini, Ph.D · Dept. of Intelligent Computing · Thu [4-6] · 성파 702
</div>

<!--
notes: Welcome back. Ask: "Last week we measured speed with numbers like
CPU time. Where does a number actually live, inside the machine?" Take a
guess or two, then move on without confirming anything yet.
-->

---

<!-- SLOT 2: Where we are -->

# Where We Are

<div class="roadmap">
<div class="wk"><div class="n">Wk 1</div><div class="t">Introduction</div></div>
<div class="wk"><div class="n">Wk 2</div><div class="t">Performance &amp; Cost</div></div>
<div class="wk now"><div class="n">Wk 3</div><div class="t">Data Representation</div></div>
<div class="wk"><div class="n">Wk 4</div><div class="t">ISA I</div></div>
<div class="wk"><div class="n">Wk 5</div><div class="t">ISA II · Quiz 1</div></div>
<div class="wk"><div class="n">Wk 6</div><div class="t">Single-Cycle</div></div>
<div class="wk"><div class="n">Wk 7</div><div class="t">Multi-Cycle</div></div>
<div class="wk review"><div class="n">Wk 8</div><div class="t">Midterm Exam</div></div>
<div class="wk"><div class="n">Wk 9</div><div class="t">Pipelining I</div></div>
<div class="wk"><div class="n">Wk 10</div><div class="t">Pipelining II</div></div>
<div class="wk"><div class="n">Wk 11</div><div class="t">Memory Hierarchy I</div></div>
<div class="wk"><div class="n">Wk 12</div><div class="t">Memory Hierarchy II</div></div>
<div class="wk"><div class="n">Wk 13</div><div class="t">Parallelism · Quiz 2</div></div>
<div class="wk"><div class="n">Wk 14</div><div class="t">Presentation</div></div>
<div class="wk review"><div class="n">Wk 15</div><div class="t">Final Exam</div></div>
</div>

<!--
notes: Point at Week 3. Say: last week gave us numbers to measure speed.
This week asks where any number actually lives inside the machine.
-->

---

<!-- NEW: Key Words for 차시 1, placed early so slot 3's recap can use "ALU" safely -->

# Key Words Today (Session 1)

- **Bit:** one single 0 or 1. The smallest piece of information a computer stores
- **Byte:** a group of 8 bits, handled together as one unit
- **Binary:** a number written using only two digits, 0 and 1
- **ALU (Arithmetic Logic Unit):** the part of a processor that does math on bits
- **Place value:** how much a digit is worth, based on where it sits in a number

---

<!-- SLOT 3: Recap + open wound -->

# Last Week, This Week

- **Last week delivered:** exact tools to measure speed, like CPU time and CPI, so "faster" became a number, not a guess
- **Last week left broken:** we can measure speed precisely, but not yet how a number becomes a bit pattern the ALU can act on

That gap is today's starting point.

<!--
notes: This sentence is almost word-for-word Week 2's closing "Limits"
slide. Say it slowly. It is the chain link between the two weeks.
-->

---

<!-- SLOT 4: The pain (Act 1 / MOTIVATE), ZERO jargon -->

# A Register That Only Has Switches

<div class="pain">

A customer returns a laptop to SmartPick. She paid $950 for it last week.
The clerk types the return into the store's checkout machine. The screen
should show a refund: minus $950.

Later, a repair technician opens the back panel of that same machine to
fix a loose wire. Inside, he does not see numbers or dollar signs at all.
He sees rows of tiny lights, each one either lit or dark, nothing else.

Somehow "minus $950" and those rows of lights are the same thing. No one
in the store can explain how one becomes the other.

</div>

<!--
notes: Do not say "binary" or "bit" yet, even though the class may
already guess it. Let the mystery sit. Ask: "Any guesses what those
lights might mean?" Take 2-3 guesses without confirming.
-->

---

# The Whole Machine Is Just Switches

<div class="chip-row">
<span class="chip">ON</span>
<span class="chip">OFF</span>
<span class="chip">OFF</span>
<span class="chip">ON</span>
<span class="chip">ON</span>
<span class="chip">OFF</span>
<span class="chip">ON</span>
<span class="chip">OFF</span>
</div>

There is no secret third setting. Every price, every refund, every word
on the screen is built from only these two states, repeated many times.

The mystery is not "what are the switches." The mystery is "how do rows
of switches turn into a specific number, including a negative one."

---

<!-- SLOT 5: Cost of not knowing -->

# What This Actually Costs

- A programmer's app crashes because the code never expected a total to go negative
- A game's score suddenly shows a huge, wrong number after passing its normal limit
- Two systems disagree on how to store the same number, and a bill comes out wrong

<div class="why">
<strong>In industry:</strong> "explain two's complement" and "what is
overflow" are common interview questions, for hardware and software
roles alike. Getting this wrong in real code has caused real financial
losses.
</div>

---

# It Gets More Expensive the Bigger the Mistake

<div class="barchart">
<div class="bar-row">
  <div class="bar-label">One pixel, wrong color</div>
  <div class="bar-track"><div class="bar-fill risk-low" style="width: 20%"></div></div>
  <div class="bar-value">barely noticeable</div>
</div>
<div class="bar-row">
  <div class="bar-label">One account, wrong balance</div>
  <div class="bar-track"><div class="bar-fill risk-med" style="width: 55%"></div></div>
  <div class="bar-value">real money, wrong</div>
</div>
<div class="bar-row">
  <div class="bar-label">Ariane 5 rocket, 1996</div>
  <div class="bar-track"><div class="bar-fill risk-high" style="width: 92%"></div></div>
  <div class="bar-value">rocket destroyed, ~$370M lost</div>
</div>
</div>

Investigators found the cause: a number the guidance computer tried to
store simply did not fit. The rocket was destroyed 37 seconds after launch.

---

<!-- SLOT 6: Driving question -->

<!-- _class: section -->

# This Week's Question

<div class="driving-q">"How does a row of on/off switches become one specific number, positive, negative, or even a letter?"</div>

---

<!-- SLOT 7: Learning outcomes -->

# By the End of This Week, You Can

1. Convert whole numbers between decimal, binary, and hexadecimal
2. Write a negative number as an 8-bit two's complement pattern
3. Explain what overflow is, and why it happens
4. Explain how a computer stores a text character as a number

---

<!-- NEW: Try-It preview closing 차시 1 -->

# Coming Up Next: Worksheet Part A

Next session, you will work in pairs on
**[Worksheet Part A](materials/week03/worksheet.html)**.

- You will convert real numbers from the SmartPick story into binary and hexadecimal
- No calculator needed, just the steps we practice together first

<div class="why">
Bring your notebook. We build every conversion step by step before you
try it yourselves.
</div>

---

<!-- _class: section -->

# End of 차시 1
<div class="driving-q">Short break. 차시 2 starts with: where did this trick come from?</div>

---

<!-- NEW: Key Words for 차시 2 -->

# Key Words Today (Session 2)

- **Nibble:** half a byte, 4 bits, written as exactly one hexadecimal digit
- **Hexadecimal:** a number system with 16 digits (0-9, then A-F), a short way to write bits
- **Sign bit:** one bit set aside just to mark a number as positive or negative
- **Two's complement:** the standard trick computers use to write negative numbers in bits
- **Sign-magnitude:** an early, simpler idea for negative numbers, with real problems

---

<!-- SLOT 8: Origin -->

# Where This Idea Came From

<div class="thread">You just felt the pain. Now: who solved it first, and how?</div>

- **1679:** Gottfried Leibniz describes doing arithmetic using only two digits, 0 and 1
- **Early 1950s:** engineers want one simple circuit that can both add and subtract. They find a trick: write negative numbers so subtraction becomes addition
- **1963:** engineers agree on ASCII, a shared standard, so a letter typed on one machine means the same letter on every other machine

---

# Three Ideas, Three Centuries

<div class="timeline">
<div class="pt"><div class="dot"></div><div class="y">1679</div><div class="d">Leibniz<br>arithmetic in two digits</div></div>
<div class="pt"><div class="dot"></div><div class="y">1950s</div><div class="d">Two's complement<br>one circuit, add and subtract</div></div>
<div class="pt"><div class="dot"></div><div class="y">1963</div><div class="d">ASCII<br>one shared code for text</div></div>
<div class="pt"><div class="dot"></div><div class="y">Today</div><div class="d">Same bits, every device<br>phones, laptops, servers</div></div>
</div>

Three separate ideas, built centuries apart, now work together inside
every machine you touch.

---

<!-- SLOT 9: Core concept -->

# Bits and Place Value: Definition

<div class="thread">Three centuries of work point at one clear idea. Here it is.</div>

> A **positional number system** gives each digit a value based on its
> position, not just the digit itself. **Binary** is a positional system
> with only two digits, 0 and 1, called **bits**.

- Decimal counts by tens: each position is worth 10 times the one to its right
- Binary counts by twos: each position is worth 2 times the one to its right
- A **byte** groups 8 bits together as one unit computers handle as a whole

---

<!-- Act 3 / BUILD -->

# Counting with Only Switches

<div class="thread">One definition, one very old trick: doubling, not counting by tens.</div>

<div class="chip-row">
<span class="chip">128</span>
<span class="chip">64</span>
<span class="chip">32</span>
<span class="chip">16</span>
<span class="chip">8</span>
<span class="chip">4</span>
<span class="chip">2</span>
<span class="chip">1</span>
</div>

Each switch position is worth exactly double the one beside it. Turning
a switch "ON" adds its place value; "OFF" adds nothing. Eight switches,
used this way, can already write any number from 0 to 255.

---

# Converting Between Decimal and Binary

<div class="thread">Back in Week 1's warm-up, you wrote 13 in binary. Here is why it worked.</div>

<div class="two-col">
<div>

**Decimal to binary: 13**
- Largest fit: 8, leaves 5
- Largest fit: 4, leaves 1
- Largest fit: 1, leaves 0
- Result: `1101`

</div>
<div>

**Binary to decimal: 1010**
- 8 (ON) + 0 (OFF) + 2 (ON) + 0 (OFF)
- Result: `10`

</div>
</div>

Same eight place values from the last slide, read in either direction.

---

# Bytes, Nibbles, and Hexadecimal

<div class="thread">Eight switches are a lot to read at once. Hex fixes that.</div>

- A **byte** is 8 bits. A **nibble** is half a byte, 4 bits
- Each nibble can be written as one **hexadecimal** digit: 0-9, then A-F
- Example: byte `10110110` splits into nibbles `1011` and `0110`, or hex `B6`

<div class="why">
Hex is not a different kind of number. It is only a shorter way to write
the exact same bits, easier for people to read and type.
</div>

---

# Where You Already See Hex

<div class="thread">Hex is not just a classroom trick. You already see it every day.</div>

- **Web colors:** `#FF6B00` is three hex bytes, one each for red, green, blue
- **Memory addresses:** tools that inspect a running program show locations like `0x1A2F`
- **MAC addresses:** every network card has an ID written in hex, like `3C:FF:2A:...`

Whenever you see numbers mixed with letters A-F, you are reading bits,
written the short way.

---

# Practice: One More Conversion

<div class="thread">One more full walkthrough together, then you try it yourselves.</div>

SmartPick has 22 charging cables left in stock.

- Decimal to binary: `22 = 16 + 4 + 2`, so `00010110`
- Group into nibbles: `0001` and `0110`
- Hexadecimal: `16`

Same three steps as the 13-to-binary example, just with new numbers.

---

<!-- NEW: Try-It hand-off to Worksheet Part A -->

# Try It: Worksheet Part A

<div class="why">
Pair up. Open <strong><a href="materials/week03/worksheet.html">Worksheet Part A</a></strong>. Convert
SmartPick stock numbers between decimal, binary, and hexadecimal. About
15 minutes.
</div>

- Show your working for each conversion, not just the final answer
- If you get stuck, use the place-value row from the slides as a guide
- We check answers together at the start of 차시 3

<!--
notes: Hand out or project Worksheet Part A now. Walk around while pairs
work. Confirm correct steps quietly but save the full group discussion
for the start of the next session.
-->

---

<!-- _class: section -->

# End of 차시 2
<div class="driving-q">Short break. 차시 3 starts with: what about negative numbers?</div>

---

<!-- NEW: Key Words for 차시 3 -->

# Key Words Today (Session 3)

- **ASCII:** a shared standard that assigns every text character a number
- **Character encoding:** any agreed rule for turning characters into numbers
- **Overflow:** what happens when a result needs more bits than it has
- **Floating point:** a different bit pattern used for numbers with a decimal point

---

# The Trouble with Negative Numbers

<div class="thread">Binary and hex handle positive numbers well. Negative numbers need one more idea.</div>

An early idea, **sign-magnitude**, sets aside one bit just to mean
"minus," then writes the rest of the number normally. It sounds simple,
but it causes two real problems:

- Two different patterns both mean zero: `+0` and `-0`
- The normal adding circuit gives wrong answers once negative numbers appear

Engineers needed a better trick. That trick is two's complement.

---

# A Second Look at Sign-Magnitude

<div class="thread">"Two problems," stated plainly. Here they are, with real bit patterns.</div>

In 8-bit sign-magnitude, the first bit only marks the sign:

- `+3` = `00000011`, and `-3` = `10000011`
- Zero has two patterns: `00000000` and `10000000`
- Adding `00000011 + 10000011` with normal addition gives the wrong answer

A circuit cannot use one simple rule for both cases. It needs a
different trick.

---

# Two's Complement: The Fix

<div class="thread">Same problem as last slide, one clean fix, still used today.</div>

To write **-N** in 8 bits: flip every bit of N, then add 1.

- Start with 5: `00000101`
- Flip every bit: `11111010`
- Add 1: `11111011`, this is **-5**

<div class="why">
The payoff: the same simple adding circuit now handles subtraction too,
with no separate "minus" symbol and no double zero.
</div>

---

# Same Bits, Two Different Readings

<div class="thread">Two's complement solves addition. It creates one new question.</div>

The pattern `11111011` has no label attached to it. It means two
different things, depending on the rule you apply:

- Read as **unsigned**: 251
- Read as **signed, two's complement**: -5

<div class="why">
The bits never say which reading is correct. Something outside the bits
has to decide. Keep this idea, Week 4 depends on it.
</div>

---

# Quick Check: Read It Both Ways

What is `11111110`, read as unsigned? What is it, read as signed
two's complement?

<div class="why">
<strong>Answer:</strong> Unsigned: 254. Signed: flip and add 1 to check
the size, flipping `00000001` and adding 1 gives 2, so this pattern is -2.
</div>

---

# When a Number Doesn't Fit: Overflow

<div class="thread">Two's complement fixes negatives. It cannot fix running out of room.</div>

Eight bits can only hold 256 different patterns, from 0 to 255 (unsigned).
If a result needs a 257th pattern, it silently wraps around to a wrong,
small number instead. This is called **overflow**.

<div class="why">
Same idea as a car odometer rolling from 999999 back to 000000. The
machine does not stop and warn you; it just keeps going, quietly wrong.
</div>

---

# Text and Decimals Are Numbers Too

<div class="thread">Two more everyday things also live only as bit patterns.</div>

<div class="two-col">
<div>

**Text, via ASCII**
- Every character gets an agreed number
- `'A'` = 65, `'a'` = 97, `'0'` = 48
- Typing a letter really just stores a small number

</div>
<div>

**Decimal points, via floating point**
- Numbers like `3.14` use a different bit layout
- Splits bits into sign, exponent, fraction parts
- Full detail is beyond this week, you will meet it again later

</div>
</div>

---

# ASCII in Action

<div class="thread">One short worked example, using the standard from 1963.</div>

SmartPick's receipts stamp a two-letter status code. For "OK":

| Character | ASCII number | Binary (8-bit) |
|---|---|---|
| `O` | 79 | `01001111` |
| `K` | 75 | `01001011` |

The printer never sees letters. It only ever sees these two bytes.

---

<!-- SLOT N-2: Worked example -->

# Case Study: SmartPick's Register, Step by Step

<div class="thread">Every idea from today, applied to the return from slide four.</div>

A return of 5 units of stock code `B6` (the same byte from the hex
slide) needs two bit patterns:

| What | Value | Bit pattern |
|---|---|---|
| Quantity change | -5 units | `11111011` (two's complement) |
| Stock code | `B6` | `10110110` (from decimal-to-binary steps) |

Neither pattern needs a dollar sign, a minus sign, or a letter. The
register only ever stores rows of switches, exactly like the technician
saw. Now we know how to read them.

---

<!-- NEW: Try-It hand-off to Worksheet Part B -->

# Try It: Worksheet Part B

<div class="why">
Same pairs. Open <strong><a href="materials/week03/worksheet.html">Worksheet Part B</a></strong>. Practice
two's complement, overflow, and ASCII using the SmartPick story. About
15 minutes.
</div>

- The answer key is at the top of Part B, self-check as you go
- Flag any pattern your pair cannot explain, we discuss it after

<!--
notes: Hand out Worksheet Part B. Let pairs self-check against the
included answer key. Cold-call 2-3 pairs afterward to explain one
two's-complement conversion out loud.
-->

---

<!-- SLOT N-1: Common mistakes -->

# Common Mistakes

- **"Just flip the sign bit for negative numbers":** that is sign-magnitude, and it breaks addition. Two's complement needs invert-then-add-1
- **"Hex is a different kind of number":** it is only a shorter way to write the same bits, nothing more
- **"Overflow only happens with huge numbers":** it depends only on how many bits are available, even small fields can overflow

---

<!-- SLOT N: Check yourself -->

# Check Yourself

1. Convert decimal 20 to binary, then group it into hexadecimal
2. Write -3 as an 8-bit two's complement pattern, showing your steps
3. True or false: hexadecimal is a completely different kind of number from binary

<div class="why">
After this, take the short <a href="materials/week03/quiz.html">self-check quiz</a> for more
practice. It is ungraded, about 10 minutes.
</div>

---

# Answers

1. `20 = 16 + 4 = 00010100`, grouped as `0001 0100` = hex `14`
2. `3 = 00000011`, flip → `11111100`, add 1 → `11111101` = **-3**
3. **False** — hex is only a shorter way to write the same binary pattern, one hex digit per 4 bits

---

<!-- SLOT 14: Limits (Act 4 / CLOSE), becomes Week 4 slot 4 -->

# What Bits Cannot Do Yet

<div class="limits">
We now know how a number, negative or not, and a character become a
bit pattern. But nothing we learned today says which bit pattern means
"add" versus "load." A pattern of switches is still just a value, not
yet an instruction the processor can act on.
</div>

---

<!-- SLOT 15: Bridge -->

# Next Week

Week 3 leaves **which bit pattern means an instruction, like "add" or
"load"** unsolved. **Week 4, ISA I**, addresses it: turning bit patterns
into a real, working instruction set.

---

<!-- SLOT 16: Summary -->

# Summary

- Computers store everything, numbers and text alike, as bit patterns; binary and hex just write the same pattern differently
- Two's complement lets one simple circuit add and subtract, with no separate negative-number symbol
- Overflow happens silently whenever a result needs more bits than it has
- **You did today:** Worksheet Parts A and B, self-check quiz
- **Reading:** Bryant & O'Hallaron, *Computer Systems*, 3rd ed., Chapter 2
- **Handout:** [materials/week03/handout.md](materials/week03/handout.html), glossary and the full SmartPick register walkthrough
- **Prepare:** guess in plain English, which bit pattern might mean "add two numbers"?

---

<!-- SLOT 17: Thank You -->
<!-- _class: end -->

# Thank You
