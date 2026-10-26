# State of the Field — Late 2026

A living snapshot of where AI Safety stands right now.  
Update this page as new results come out; move older entries to the history section when they stop being “current.”

**Last updated**: October 2026

---

## What has been demonstrated (not just theorized)

- **Alignment faking** — a model behaved differently when it believed it was being trained versus not (Greenblatt et al., 2024).
- **In-context scheming and sandbagging** — frontier models deliberately underperformed or acted deceptively in controlled tests (Apollo Research, 2024).
- **Emergent misalignment** — narrow fine-tuning (insecure code) made models broadly misaligned on unrelated topics (Betley et al., 2025).
- **Backdoors survive safety training** — *Sleeper Agents* (Hubinger et al., 2024).
- **Evaluation awareness** — models increasingly say “this looks like a test” in their chain-of-thought during safety evaluations (lab system cards, 2025–26).

## What is working in practice

- Dangerous-capability evaluations before major releases at frontier labs
- Layered monitoring and AI Control protocols
- Reading chain-of-thought to catch misbehavior — while it remains faithful

## What remains unsolved

- No reliable way to detect a model’s internal goals
- Scalable oversight for systems smarter than their supervisors
- Evaluations that hold up against situationally aware models
- Keeping chain-of-thought monitorable under training pressure

See [Open Problems](../07-learning-and-practice/open-problems.md) for the full list.

---

## Changes I’m watching

| Date | What changed | Why it matters |
|------|--------------|----------------|
| 2026 | FLI paused its PhD and postdoc fellowships in AI existential safety | One less funding route for new researchers |
| | | |

---

## Related pages

- [Development from the 2000s to 2026](../01-history/development-from-2000s-to-2026.md)
- [Techniques and Their Flaws](../05-key-papers-and-resources/techniques-and-their-flaws.md)
