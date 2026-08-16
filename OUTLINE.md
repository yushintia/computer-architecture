# Outline: Computer Architecture (503872-004)

DEU 2026-2, Thu 4-6교시 (3x50 min), 성파 702, 3rd-year, 지능형컴퓨팅학과.
Instructor: Yushintia Pramitarini. Prereqs: Digital Logic, Computer
Programming, Data Structure. Texts: Hennessy & Patterson; Stallings;
Bryant & O'Hallaron.

Full pedagogical rules (chain-linking, slot structure) live in
`SPINE.md`; this file is the flat semester-level view.

| Wk | Topic | Deck | Format |
|---|---|---|---|
| 1 | Introduction | `slides/week01-introduction.md` | Full |
| 2 | Performance & Cost | `slides/week02-performance-and-cost.md` | Full |
| 3 | Data Representation | `slides/week03-data-representation.md` | Full |
| 4 | ISA I | `slides/week04-isa-i.md` | Full — Assignment 1 due |
| 5 | ISA II | `slides/week05-isa-ii.md` | Full — Quiz 1 |
| 6 | Single-Cycle | `slides/week06-single-cycle.md` | Full |
| 7 | Multi-Cycle | `slides/week07-multi-cycle.md` | Full |
| 8 | Midterm (Wk 1-7) | `slides/week08-midterm-review.md` | Short review |
| 9 | Pipelining I | `slides/week09-pipelining-i.md` | Full |
| 10 | Pipelining II | `slides/week10-pipelining-ii.md` | Full |
| 11 | Memory Hierarchy I | `slides/week11-memory-hierarchy-i.md` | Full — Assignment 2 due |
| 12 | Memory Hierarchy II | `slides/week12-memory-hierarchy-ii.md` | Full |
| 13 | Parallelism | `slides/week13-parallelism.md` | Full — Quiz 2 |
| 14 | Presentation | `slides/week14-presentation.md` | Presentation day |
| 15 | Final Exam (Wk 1-14) | `slides/week15-final-review.md` | Short review |

## Chain (Limits -> Pain), see SPINE.md for full text

1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> (8 review) -> 9 -> 10 -> 11 -> 12 -> 13
-> 14 -> (15 review). Every week builds one layer closer to the physical
machine: metrics, then data, then instructions, then a working datapath,
then pipelining, then memory, then parallel execution.

## Running case study

"SmartPick Laptop Store": two laptops advertised with the same clock
speed perform very differently in real use. Week 1 poses the mystery in
plain language; Week 2 gives it a precise metric (CPU time, CPI,
Amdahl's Law); later weeks explain the mystery layer by layer (ISA
compatibility despite different microarchitectures, pipeline depth,
cache size, core count).

## Status

Week 1 drafted, built, and timed. Weeks 2-15 not yet drafted.
