# The Spine: Standard Structure for Every Lecture Week

Computer Architecture (503872-004), 2026-2. This document is the standard.
Every week's deck (`slides/weekNN-*.md`) must follow it. If a deck and this
document disagree, fix the deck.

## Principle

**Motivation always precedes definition.** A student should never meet a
term before meeting the concrete problem that forced someone to invent it.
Every week opens with a broken scenario in plain language, not a formal
statement.

**Weeks chain.** The "Limits" slide that closes week N is, almost verbatim,
the "Pain" slide that opens week N+1. The semester should read as one
argument, not fourteen independent talks.

## The 17 slots

Acts 0, 1, 2, 4 are **mandatory and fixed**: same slot numbers, same order,
every full-spine week. Act 3 (Build) expands or contracts to fit the topic.

### Act 0: LOCATE

| # | Slide | Rule |
|---|---|---|
| 1 | Title | Week #, topic, course code, professor, date |
| 2 | Where we are | Shared roadmap graphic (`_shared/roadmap.md`), current week highlighted |
| 3 | Recap + open wound | One sentence on what last week delivered, one sentence on what it left broken |

### Act 1: MOTIVATE

| # | Slide | Rule |
|---|---|---|
| 4 | The pain | Concrete broken scenario in the running case study. **Zero jargon.** If a technical term appears here, the slide is wrong |
| 5 | Cost of not knowing | What breaks downstream (wrong purchases, wasted budget, missed deadlines) *and* where this bites in industry (interviews, real product failures, job requirements) |
| 6 | Driving question | One sentence the week must answer. Repeat it verbatim on any section-divider slide inside Act 3 |
| 7 | Learning outcomes | 3-4 verbs, each traceable to a syllabus objective |

**Hard rule:** no formal definition before slot 8. If you need one earlier,
the pain slide (4) is too abstract, so fix it instead of breaking the rule.

### Act 2: GROUND

| # | Slide | Rule |
|---|---|---|
| 8 | Origin | Who, when, what forced it. Ideas are answers to historical pain, not arbitrary convention |
| 9 | Core concept | First formal definition of the week |

### Act 3: BUILD (flexible)

| # | Slide | Rule |
|---|---|---|
| 10..N-3 | Mechanics | Stepwise, as many slides as the topic needs |
| N-2 | Worked example | Same running case study, continued from prior weeks; see `slides/_shared/case-study.md` |
| N-1 | Common mistakes | Anti-patterns and why each is tempting |
| N | Check yourself | 2-3 questions; put the answers on the slide immediately after, not the same slide |

### Act 4: CLOSE

| # | Slide | Rule |
|---|---|---|
| N+1 | Limits | What this week's technique cannot do. **This text becomes next week's slot 4** |
| N+2 | Bridge | "Week N leaves X unsolved -> Week N+1 addresses it." Explicit, one sentence |
| N+3 | Summary | Takeaways + reading assignment + what to prepare |
| N+4 | Thank You | Template end slide |

## The semester chain

| Wk | Topic | Limit (leads to next pain) |
|---|---|---|
| 1 | Introduction | We know how the course runs and met the SmartPick mystery, but not yet why the spec sheet did not tell the whole story -> **W2** |
| 2 | Performance & Cost | We can measure speed precisely, but not yet how a number becomes a bit pattern the ALU can act on -> **W3** |
| 3 | Data Representation | Bits are well-defined, but nothing yet says which bit pattern means "add" versus "load" -> **W4** |
| 4 | ISA I | We can name instructions, but not yet compute with the full instruction set -> **W5** |
| 5 | ISA II · Quiz 1 | The instruction set is complete on paper, but no circuit yet executes it -> **W6** |
| 6 | Single-Cycle | A working datapath exists, but it wastes a full clock cycle on every instruction, even fast ones -> **W7** |
| 7 | Multi-Cycle | Multi-cycle saves time per instruction type, but the processor still does only one thing at a time -> **W9** |
| 8 | Midterm | review only, no chain link |
| 9 | Pipelining I | Pipelining overlaps instructions for speed, but overlapping them can produce wrong answers -> **W10** |
| 10 | Pipelining II | Hazards are handled, but every pipeline still waits on a slow memory system -> **W11** |
| 11 | Memory Hierarchy I | Caching speeds up memory, but only for programs and datasets that fit -> **W12** |
| 12 | Memory Hierarchy II | Virtual memory solves capacity, but a single core is still the whole story -> **W13** |
| 13 | Parallelism · Quiz 2 | We can name parallel techniques, but not yet see them working in a real, current design -> **W14** |
| 14 | Presentation | Students present a real design; professor closes remaining gaps -> **W15** |
| 15 | Final Exam | review only, no chain link |

Weeks 8 and 15 use the **short review variant**: Act 0 (slots 1-3) + Act 3
slot "Check yourself" (expanded into full review questions) + Act 4 (slots
N+1..N+4, "Limits" replaced by "What to focus on next"). No Pain or Ground
acts: there is no new concept to motivate. Weeks 5 and 13 carry an embedded
quiz but keep the full spine: new content is still taught that day.

Week 1 uses the **orientation variant**: the entire session is the course
contract (syllabus, grading, policy, schedule) plus a single non-technical
tease of the SmartPick running example — near-zero technical content, no
Act 2/3 (Ground/Build). It still opens with the roadmap and closes with a
Limits -> Bridge -> Summary -> Thank You, so the chain into Week 2 holds.
Materials for Week 1 are handout-only (a course handbook); there is no
worksheet or quiz that week, since no technique is taught yet to practice.

## Enforcement

- Copy `slides/_template/week-XX.md` for every new week. It carries all 17
  slots as HTML comments; fill them in, don't renumber them.
- `slides/_shared/roadmap.md`: single source for the Act 0 roadmap graphic.
- `slides/_shared/case-study.md`: the running example as it stands after
  each week; update it when a week changes it materially.
- Course logistics (grading, textbook, policies) live in an appendix block
  in Week 1 only, outside the spine numbering. Administrative content must
  never sit between the roadmap and the pain slide.
