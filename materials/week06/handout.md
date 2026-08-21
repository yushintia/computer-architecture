# Week 6 Handout: Single-Cycle Datapath

Computer Architecture (503872-004) — for students to keep and read again.
Use plain, simple English on purpose, so it is easy to read even if
English is not your first language.

---

## 1. Glossary: Key Words This Week

Read each definition once now. You do not need to memorize them today —
you will use them all semester.

| Term | Plain definition |
|---|---|
| **Datapath** | The wiring inside a chip that moves data from one part to another |
| **Control unit** | The part of the chip that decides which wires turn on, for each instruction |
| **Clock cycle** | One tick of the chip's clock, the smallest slice of time it works in |
| **Register file** | A small, very fast set of storage slots inside the chip |
| **ALU (Arithmetic Logic Unit)** | The circuit that does math (add, subtract) and comparisons |
| **Program counter (PC)** | A storage slot that always holds the address of the next instruction |
| **Instruction memory** | The storage that holds the whole program, one instruction per address |
| **Data memory** | Bigger, slower storage used only by load and store instructions |
| **Opcode** | The short code inside an instruction that names which operation to do |
| **Funct** | A second field inside an R-type instruction, naming the exact ALU operation |
| **Multiplexer (mux)** | A switch that picks one of several input wires to pass through |
| **Sign extension** | Stretching a short built-in number to full size before the ALU uses it |
| **Immediate** | A small number built directly into an instruction, instead of read from a register |
| **Control signal** | One on/off wire the control unit sets, like RegWrite or MemRead |
| **Critical path** | The slowest chain of steps a single clock cycle must wait for |
| **Single-cycle datapath** | A design where every instruction, of any type, finishes in exactly one clock cycle |

---

## 2. The SmartPick Story, Worked Out Step by Step

This is the full version of the story from class. Read it slowly if the
in-class pace felt fast.

**The situation.** SmartPick's chip team finishes a complete, checked
list of every command their new laptop chip should understand. They send
it to a factory that builds a test chip.

**The test.** An engineer feeds the test chip one simple command: add
two numbers. Nothing happens. There is no wiring yet that carries a
command from start to finish. A complete list on paper does not move a
single number by itself.

**Step 1: Name the parts a datapath needs.** Every instruction needs
somewhere to read what to do (**instruction memory**), somewhere to read
values (**register file**), somewhere to compute (**ALU**), and
sometimes somewhere to store or fetch data (**data memory**). A
**control unit** decides which wires turn on for each instruction.

**Step 2: Trace one instruction, `add $t0, $t1, $t2`.** Assume `$t1`
holds 5 and `$t2` holds 7.

1. **Fetch:** the PC points at this instruction in instruction memory
2. **Decode:** the register file reads `$t1` = 5 and `$t2` = 7
3. **Execute:** the ALU adds them, producing 12
4. **Write Back:** 12 is written into `$t0`

Control signals for this instruction: RegWrite = on, MemRead = off,
MemWrite = off, Branch = off. Add never touches data memory at all.

**Step 3: Compare add, load, and branch.** Using these stage timings —
fetch 200 ps, register read 100 ps, ALU 200 ps, data memory 200 ps,
register write 100 ps — the three instruction types need very different
real amounts of time:

| Instruction | Real steps used | Real time needed |
|---|---|---|
| Add (R-type) | fetch, decode, execute, write back | 600 ps |
| Load word | fetch, decode, execute, memory, write back | 800 ps |
| Branch | fetch, decode, execute | 500 ps |

**Step 4: State clearly what single-cycle design forces.** Every
instruction must share one clock cycle length, fixed to the **slowest**
instruction: load, at 800 ps. Add wastes 200 ps every single cycle.
Branch wastes 300 ps every single cycle. This waste is not a mistake in
the design — it is a direct result of one shared clock for every
instruction type, and it is exactly what Week 7's multi-cycle design
fixes.

---

## 3. Optional Reading: Extra Detail (Not Required, Not on the Quiz)

This section holds extra explanations that were trimmed from the slides
to keep class time short. Read it if you are curious or want more
examples.

**The mux is a traffic switch, not a mixer.** A multiplexer does not
combine its input wires together. It picks exactly one of them to pass
through, based on a control signal, the same way a train switch sends a
train down exactly one of two tracks, never both at once. The ALU's
second input is a classic example: a mux picks between a register value
(for add) and a sign-extended immediate (for load), one or the other,
every single cycle.

**Why two adders, not one.** The main ALU is already busy every cycle
doing the instruction's real work. But "current address plus four," to
find the next instruction, still needs computing every cycle too, even
while the ALU is busy elsewhere. Real single-cycle datapaths add a
second, separate adder just for this PC-plus-four step, so the two jobs
never compete for the same circuit.

**Where this shows up around you.**

- **Microcontrollers:** many small embedded chips (in toys, appliances, simple sensors) still use single-cycle-like, low-complexity designs
- **Teaching processors:** MIPS, used in most textbooks, was designed specifically to make this circuit easy to draw and verify
- **RISC-V cores:** simple, low-power RISC-V implementations often start from this exact single-cycle design before adding speed features
- **FPGA prototyping:** engineers often build a single-cycle version of a new design first, to check correctness before optimizing for speed

**Who actually designs this, as a job.**

- **Computer architects** decide the overall circuit plan and trade-offs — this course's core focus
- **Digital design engineers** draw and build the exact datapath wiring, part by part
- **Verification engineers** test the finished circuit against every instruction before it ships
- **Embedded engineers** build small, simple chips that often still use this single-cycle idea directly

---

## 4. Practice Problems (With Answers)

Try each problem yourself before checking the answer underneath it.

**Problem 1.** Name the five main parts of a single-cycle datapath, plus
the control unit.
> **Answer:** Program counter (PC), instruction memory, register file,
> ALU, data memory, plus the control unit.

**Problem 2.** Put these steps in the right order for a load
instruction: write back, execute, memory, fetch, decode.
> **Answer:** Fetch -> Decode -> Execute -> Memory -> Write Back.

**Problem 3.** Using this week's stage timings (fetch 200 ps, register
read 100 ps, ALU 200 ps, data memory 200 ps, register write 100 ps),
compute the real time needed by a store instruction (fetch, decode,
execute, memory — no write back).
> **Answer:** 200 + 100 + 200 + 200 = 700 ps.

**Problem 4.** If the datapath's clock cycle is fixed at 800 ps (set by
load), how much time does the store instruction from Problem 3 waste
every cycle?
> **Answer:** 800 - 700 = 100 ps wasted every cycle.

**Problem 5.** A friend says: "A single-cycle design can give a fast
instruction, like add, a shorter clock cycle than a slow one, like
load." Is this true? Explain in one sentence.
> **Answer:** No. Every instruction shares one clock signal, so all
> instructions get exactly the same fixed cycle length, set by the
> slowest instruction.

**Problem 6.** Name the control signal that must be "on" for a load
instruction but "off" for an add instruction.
> **Answer:** MemRead. Load reads data memory; add never touches data
> memory at all.
