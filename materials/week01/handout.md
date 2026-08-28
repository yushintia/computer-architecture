# Week 1 Course Handbook: Computer Architecture

Computer Architecture (503872-004) — for students to keep and read
again. Use plain, simple English on purpose, so it is easy to read
even if English is not your first language. This handbook mirrors the
course contract covered in the Week 1 slides. There is no worksheet or
quiz for Week 1 — no technique has been taught yet to practice.

---

## 1. Course Description

This course opens the box underneath the code you already know how to
write. It covers how a program becomes instructions a chip can run
(the instruction set), how a processor design — single-cycle,
multi-cycle, pipelined — carries those instructions out, and how
memory and parallel hardware make a real machine fast. Every idea ties
back to one question: what makes a real computer fast or slow?

## 2. Learning Objectives

By the end of this course, you can:

1. Explain how a line of code becomes work a physical chip performs.
2. Compute and compare CPU performance using CPU time, CPI, and
   Amdahl's Law.
3. Represent numbers, text, and instructions as bits.
4. Read and write basic assembly instructions.
5. Explain how a single-cycle and a multi-cycle processor design work.
6. Explain how pipelining speeds up a processor, and what can go wrong.
7. Explain how cache, virtual memory, and parallelism make a modern
   machine fast.

## 3. Prerequisites

- **Digital Logic**
- **Computer Programming I & II**
- **Data Structure**

We do not start from zero. If gates and flip-flops, writing working
code, or arrays and pointers feel shaky, say so early — it compounds
fast otherwise.

## 4. Textbooks

- **Primary:** Hennessy & Patterson, *Computer Architecture: A
  Quantitative Approach*, 6th ed., 2017
- **Secondary:** Stallings, *Computer Organization and Architecture*,
  2019; Bryant & O'Hallaron, *Computer Systems: A Programmer's
  Perspective*, 3rd ed., 2015
- **Also:** the lecture slides themselves are a listed course
  reference

## 5. How This Course Runs

Each 150-minute class is split into three 50-minute sessions (차시 1,
2, 3). Each session mixes short lectures with a warm-up question, a
recap of what last week left unsolved, pair or group activities, and
(most weeks) a short, ungraded self-check quiz. You will talk in this
class, not just listen.

## 6. Weekly Schedule

| Wk | Topic | Wk | Topic |
|---|---|---|---|
| 1 | Introduction | 9 | Pipelining I |
| 2 | Performance & Cost | 10 | Pipelining II |
| 3 | Data Representation | 11 | Memory Hierarchy I — **Assignment 2** |
| 4 | ISA I — **Assignment 1** | 12 | Memory Hierarchy II |
| 5 | ISA II — **Quiz 1** | 13 | Parallelism — **Quiz 2** |
| 6 | Single-Cycle | 14 | Presentation — **Group Presentation** |
| 7 | Multi-Cycle | 15 | **Final Exam** (Wks 9-14) |
| 8 | **Midterm Exam** (Wks 1-7) | | |

## 7. Grading

| Component | Weight |
|---|---|
| Attendance | 10% |
| Midterm | 30% |
| Final | 30% |
| Assignments (×2) | 10% |
| Presentation | 10% |
| In-class items | 10% |

**Grade distribution guideline:** A ≤30%, B ≤40%, C-F ≤30% of the
class. This may shift after the add/drop period, based on final
enrollment.

## 8. Assignments

| # | Released | Due | Topics |
|---|---|---|---|
| 1 | Wk 2 | Wk 4 | Binary representation, instruction encoding basics |
| 2 | Wk 9 | Wk 11 | Datapath/pipelining trace, cache behavior |

## 9. Feedback Policy

> Assignments graded within one week with rubric and model answers;
> exam item-analysis shared with weak-topic guidance and individual
> review on request.

In plain terms: you will know what you got wrong, and why, quickly
enough for it to still matter for the next assignment or exam.

## 10. Attendance & Late Work

- **Attendance** is 10% of your grade and is recorded every session.
- **Late arrival:** arriving within 15 minutes of the start is
  on-time; after that, you're marked late. Three lates equal one
  absence.
- **Can't attend?** Email the professor *before* the session to be
  marked excused — unexcused absences aren't eligible for makeup
  credit.
- **Late work:** loses 10% of that assignment's grade per day late, up
  to 3 days. No credit after 3 days, unless arranged with the
  professor in advance.

## 11. Academic Integrity

- **Academic integrity:** submit your own work. Copying another
  student's work, having someone else complete it for you, or
  submitting unattributed AI-generated work as your own is a
  violation.
- **First violation:** zero credit on that assignment or exam, plus a
  formal report. **Repeat violation:** may result in failing the
  course, per university policy.
- If anything here is unclear, ask — now is the cheapest time to ask.

## 12. Support for Students with Disabilities

- **Hearing-impaired:** front-row seating, lecture material files
  provided where possible, urgent notices given in writing
- **Mobility-impaired:** extended exam time
- **Other documented conditions:** extended exam time, materials
  provided in advance, enlarged exam copies, or other reasonable
  accommodation based on need

Contact the professor early, and the Disability Student Support
Center or Academic Affairs Team, so accommodations are ready before
you need them.

## 13. Contact

- **Email:** yushintia@deu.ac.kr
- **Office hours:** by appointment, email first
- Email is the fastest way to reach the professor outside of class.

## 14. The SmartPick Story (Preview, Not Explained Yet)

This semester's worked examples come back to SmartPick, the campus
electronics store, and two of its laptops with the exact same
processor speed printed on the box, but very different real-world
speed. Week 1 only poses this mystery. Week 2 starts to explain it,
with real numbers instead of a stopwatch guess.
