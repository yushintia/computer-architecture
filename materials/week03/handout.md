# Week 3 Handout: Data Representation

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **Bit** | One single 0 or 1. The smallest piece of information a computer stores |
| **Byte** | A group of 8 bits, handled together as one unit |
| **Nibble** | Half a byte, 4 bits, written as exactly one hexadecimal digit |
| **Binary** | A number written using only two digits: 0 and 1 |
| **Decimal** | The everyday number system, written using ten digits: 0 through 9 |
| **Hexadecimal** | A number system with 16 digits, 0-9 then A-F. A short way to write bits |
| **Place value** | How much a digit is worth, based on where it sits in a number |
| **Positional number system** | A number system where each digit's value depends on both the digit and its position |
| **ALU (Arithmetic Logic Unit)** | The part of a processor that does math and logic on bits |
| **Sign bit** | One bit set aside just to mark a number as positive or negative |
| **Sign-magnitude** | An early, simple idea for negative numbers: one sign bit, then the number written normally. It has real problems |
| **Two's complement** | The standard trick computers use to write negative numbers in bits: invert every bit, then add 1 |
| **Unsigned** | A way of reading a bit pattern where every bit only adds a positive amount, never negative |
| **Signed** | A way of reading a bit pattern where the pattern can represent a negative number, using two's complement |
| **Overflow** | What happens when a result needs more bits than are available. The answer silently wraps to a wrong number |
| **ASCII** | A shared standard, from 1963, that assigns every text character an agreed number |
| **Character encoding** | Any agreed rule for turning characters into numbers, ASCII is one example |
| **Floating point** | A different bit pattern, used for numbers with a decimal point, like 3.14 |

---

## 2. The SmartPick Register, Worked Out Step by Step

This is the full version of the story from class. Read it slowly if the
in-class pace felt fast.

**The situation.** A customer returns a laptop to SmartPick, the campus
electronics store. She paid $950 for it. The store's checkout machine
must record a refund and update the stock count. A repair technician,
opening the same machine later, sees only rows of tiny lights, each one
either lit or dark. Nothing else. How does "$950" or "minus 5 units"
become those lights?

**Step 1: Turn a plain quantity into bits.** The return also puts 5
units of stock code `B6` back into inventory. To store the quantity
change as -5, in 8 bits:

- Start with the positive number, 5, in binary: `00000101`
- Flip every bit: `11111010`
- Add 1: `11111011`

That pattern, `11111011`, is -5 in 8-bit two's complement. The exact
same steps work for any negative number.

**Step 2: Turn a stock code into bits.** The stock code `B6` is already
written in hexadecimal, a short way to write bits. Each hex digit is
one nibble (4 bits): `B` = `1011`, `6` = `0110`. Together, `B6` is the
byte `10110110`.

**Step 3: Read the bits back correctly.** The pattern `11111011` means
two different things, depending on the rule applied:

- Read as **unsigned**: 251
- Read as **signed, two's complement**: -5

The bits alone never say which reading is correct. The register's
program has to already know which rule to use, for each value it
stores. That is a design decision made ahead of time, not something the
bits announce.

**Step 4: State clearly what we can, and cannot, say yet.** We *can* now
say, correctly: every value on that screen, the price, the refund, the
stock code, is really just a row of switches, read with an agreed rule.
We *cannot* yet say which bit pattern tells the processor to *do*
something, like "add these two numbers" or "load this value from
memory." That is Week 4's job.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations that were trimmed from the slides
to keep class time short. Read it if you are curious or want more
examples.

**The Ariane 5 story, in a little more detail.** In 1996, the European
Space Agency launched the Ariane 5 rocket. About 37 seconds after
launch, the guidance computer tried to store a number that did not fit
in the space set aside for it. The resulting error crashed the
guidance software, and the rocket had to be destroyed for safety. The
mistake cost roughly $370 million. The lesson computer architects and
software engineers took from it: always know how many bits a value
needs, and what happens if it needs more.

**ASCII grew into Unicode.** ASCII only covers 128 characters, mostly
English letters, digits, and punctuation. It cannot represent 한글,
emoji, or most of the world's writing systems. **Unicode**, developed
later, extends the same idea, one agreed number per character, to
cover almost every writing system in use today. Your phone's messaging
app almost certainly uses Unicode, not plain ASCII.

**Where signed vs. unsigned mistakes show up.** Choosing the wrong type
for a number is a common, real bug. A shopping cart total that should
never go negative, stored as "unsigned," will wrap around to a huge
number instead of showing an error, if a bug ever makes it try to go
below zero. Security researchers specifically look for this kind of
mistake, because it can let an attacker trick a program into
misreading a value.

**Where hexadecimal shows up around you.**

- **Web colors:** `#FF6B00` is three hex bytes, one each for red, green, blue
- **Memory addresses:** debugging tools show computer memory locations in hex, like `0x1A2F`
- **Network hardware IDs:** MAC addresses, printed on routers and network cards, are written in hex

**Who actually designs this, as a job.**

- **Compiler engineers** decide how a language's number types map onto real bit patterns
- **Security researchers** hunt for overflow and sign-confusion bugs before attackers find them
- **Database engineers** choose the smallest safe number type for each column, to save space without causing overflow
- **Firmware and embedded engineers** work directly with raw bits, often with very few spare bits to work with

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** Convert the decimal number 25 to binary.
> **Answer:** `11001` (16 + 8 + 0 + 0 + 1 = 25)

**Problem 2.** Convert the binary number `1111` to decimal.
> **Answer:** 15 (8 + 4 + 2 + 1)

**Problem 3.** Convert the byte `01000011` to hexadecimal.
> **Answer:** `43` (nibble `0100` = 4, nibble `0011` = 3)

**Problem 4.** Write -1 as an 8-bit two's complement pattern. Show your
steps.
> **Answer:** 1 = `00000001`. Flip every bit: `11111110`. Add 1:
> `11111111`. So -1 is `11111111`.

**Problem 5.** The pattern `11111101` is stored in 8 bits. What decimal
number is it, read as unsigned? What is it, read as signed two's
complement?
> **Answer:** Unsigned: 253. Signed: flip `00000010` and add 1 gives 3,
> so the pattern is -3.

**Problem 6.** What is the ASCII number for the character `'B'`? (Hint:
`'A'` is 65.)
> **Answer:** 66. ASCII numbers letters in order, so `'B'` is one more
> than `'A'`.
