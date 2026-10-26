# How to Read a Paper

Reading a paper is not reading it start to finish. It is a skill, and the notes you write are how you practice it.

The goal is not to remember the paper. It is to be able to say: **what they claimed, whether the evidence supports it, and what they didn’t test.** That last part is where your own research ideas come from.

---

## The three-pass method

Adapted from S. Keshav, *How to Read a Paper* (2007).

| Pass | Time | Read | Goal |
|------|------|------|------|
| **1. Skim** | 10 min | Title, abstract, intro, figures, conclusion | Is it worth reading? What is the main claim? |
| **2. Understand** | 1 hour | Everything, but skip proofs and appendix details | Can I explain the method and results to someone else? |
| **3. Critique** | 2+ hours | Everything, including appendix | Could I reproduce it? Where is it weak? What would I do next? |

Most papers only need pass 1. The papers you build research on need all three.

**Tip:** In pass 2, look at the **figures first**. In ML papers, the key result is almost always in one plot or table.

---

## Rules

1. **Write the summary from memory first**, then check the paper. If you can’t, you haven’t understood it yet.
2. **Separate what they showed from what they claimed.** Abstracts often claim more than the experiments show.
3. **Always fill in “What they didn’t test.”** It is the most valuable line in the note.
4. **Keep it short.** A one-page note you write is worth more than a ten-page note you never finish.

---

## Template

Copy this into a new file in `paper-notes/`, named like `2023-sharma-sycophancy.md`.

```markdown
# [Paper title]

- **Authors / org:**
- **Year:**
- **Link:**
- **Date read:**
- **Pass reached:** 1 / 2 / 3

---

## One-sentence summary (from memory, in my own words)

## The problem
- What question are they asking?
- Why does it matter for safety? Which threat or failure mode is it about?

## Method
- Models used:
- Data / environment:
- What did they measure?

## Key results (2–3, with numbers)
1.
2.
3.

## Evidence check
- Is there a **baseline**? What is it compared against?
- Is there a **positive control**? (Can the method detect the thing when it is there?)
- Other **explanations** for the result? Any **confounds**?
- Does the evidence support the claim in the abstract, or is the claim bigger?

## Limitations
- Stated by the authors:
- Ones I noticed:

## Connections to my notes
- Concepts: (e.g. outer alignment, Goodhart, situational awareness)
- Technique → flaw pair: (see techniques-and-their-flaws.md)

## What they didn't test (my follow-up idea)
- Different model / language / setting?
- What would I change if I replicated it?

## Questions I still have
```

---

## Where to start

Practice on the five papers in [Techniques and Their Flaws](./techniques-and-their-flaws.md), one per week:

1. *Towards Understanding Sycophancy in Language Models* — start here; it connects directly to your research project
2. *Sleeper Agents*
3. *Emergent Misalignment*
4. *Alignment Faking in Large Language Models*
5. *Monitoring Reasoning Models for Misbehavior*

---

## Related pages

- [Reading Lists](./reading-lists.md)
- [Quiz Highlights](../07-learning-and-practice/quiz-highlights.md) — the three habits this template trains
