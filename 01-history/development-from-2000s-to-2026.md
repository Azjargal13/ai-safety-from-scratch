# Development of AI Safety: Early 2000s to 2026

This page traces how the modern AI Safety field formed, which people were involved early and stayed active, and how the main ideas evolved.

---

## Early 2000s – Foundations

In the early 2000s, only a small number of people were seriously thinking about the long-term risks of advanced AI.

### Key people at the beginning

- **Eliezer Yudkowsky** — Founded the Singularity Institute (later MIRI) in 2000. Developed early ideas about Friendly AI, recursive self-improvement, and the difficulty of alignment.
- **Nick Bostrom** — Philosopher at Oxford. Wrote about existential risks and later published *Superintelligence* (2014), which brought the topic to a much wider audience.
- **Stuart Russell** — Already a leading AI researcher (co-author of the standard textbook *Artificial Intelligence: A Modern Approach*). Over time he became one of the strongest mainstream academic voices warning about the control problem.

Most of the broader AI research community did not take these concerns seriously at the time.

---

## 2008 – 2014: Building the Intellectual Core

Important ideas were developed mainly in a small community centered around LessWrong, MIRI, and a few academics.

Key developments:

- Detailed arguments about why alignment is hard
- Early discussion of decision theory and logical uncertainty (MIRI)
- Growing attention to the “control problem”

**Paul Christiano** began contributing around this period and later became one of the most influential technical thinkers in the field (especially on scalable oversight and iterated amplification).

---

## 2014 – 2016: Wider Attention

- **2014**: Nick Bostrom’s book *Superintelligence* is published. It significantly increases public and academic interest.
- **2015**: OpenAI is founded with a strong safety mission stated at the beginning.
- **2016**: The paper *Concrete Problems in AI Safety* (Amodei, Olah, Steinhardt, Christiano, Schulman, Mané) is released. This paper helped translate abstract concerns into concrete technical problems that machine learning researchers could work on (including reward hacking, safe exploration, etc.).

Stuart Russell also becomes more publicly active in warning about the risks.

---

## 2017 – 2020: Technical Field Begins to Form

New people and organizations enter:

- **Anthropic** is later founded by former OpenAI members (including Dario Amodei) who wanted a stronger focus on safety.
- **CHAI** (Center for Human-Compatible AI) at Berkeley, led by Stuart Russell, grows.
- Paul Christiano’s work on **Iterated Amplification** and scalable oversight becomes highly influential.
- The paper *Risks from Learned Optimization* (Hubinger et al., 2019) introduces mesa-optimization and deceptive alignment — ideas that remain central today.

During this period the field starts shifting from mostly conceptual arguments toward more technical research.

---

## 2021 – 2023: Rapid Growth

Major changes:

- Large language models become dramatically more capable.
- Alignment research expands quickly inside OpenAI, DeepMind, and Anthropic.
- New independent organizations appear or grow (Redwood Research, ARC → METR, Apollo Research, etc.).
- Techniques such as RLHF, Constitutional AI, and early interpretability methods (especially mechanistic interpretability) become major research areas.
- Chris Olah, Neel Nanda, and others help make mechanistic interpretability a serious subfield.

Many researchers who started in the earlier conceptual community move into or collaborate with the big labs.

---

## 2024 – 2026: Mainstream and Institutionalization

By this period AI Safety has become a recognized research area with:

- Dedicated safety teams at all major frontier labs
- Government involvement (AI Safety Institutes in the UK, US, and elsewhere)
- International scientific efforts (International AI Safety Report led by Yoshua Bengio, Singapore Consensus, etc.)
- Much more empirical work on evaluations, control, interpretability, and model organisms of misalignment

### People who have been involved across many years

- **Eliezer Yudkowsky** — From the very beginning (2000) to the present
- **Stuart Russell** — From academic AI into becoming a major safety voice
- **Paul Christiano** — From early theoretical work to influencing lab research and later ARC/METR-related ideas
- **Dario Amodei** — From early OpenAI safety work to co-founding Anthropic
- **Nick Bostrom** — Early philosophical framing that still shapes discussion

Newer leading contributors (e.g. in interpretability, evaluations, and control) mostly entered the field after 2018–2020.

---

## Summary of the Intellectual Path

1. **Early conceptual warnings** (Yudkowsky, Bostrom, others)
2. **Translation into concrete ML problems** (Amodei et al. 2016 and related work)
3. **Scalable oversight and theoretical frameworks** (Christiano and collaborators)
4. **Mesa-optimization and deceptive alignment** (Hubinger et al.)
5. **Empirical and lab-scale research** (RLHF, Constitutional AI, interpretability, evaluations, control)
6. **Institutional and international phase** (2024–2026)

The field moved from a small group of concerned individuals to a substantial research community with significant resources, while many of the original core worries remain unsolved.

## Which Academic Domains Does AI Safety Draw From?

AI safety is not a single isolated subject; it sits at the intersection of several distinct fields. If you look at where the research is concentrated, it pulls most heavily from:

- Machine Learning & Deep Learning (The Core): Reinforcement learning (RL), optimization theory, transformer architectures, and representation learning. You cannot critique or align a system unless you understand its mathematical guts.
- Cybersecurity & Systems Engineering: Threat modeling, penetration testing (red-teaming), privilege escalation, and sandbox isolation. As AI models become autonomous agents using software tools, AI safety increasingly resembles offensive/defensive computer security.
- Formal Methods & Software Verification: A branch of computer science focused on mathematically proving that a system satisfies certain invariants (e.g., "this system will never perform state transition).
- Game Theory & Mechanism Design (Microeconomics): Multi-agent coordination, principal-agent problems, and auction theory. When multiple AI models interact with each other and with humans, they create economic and game-theoretic equilibria that must be governed.
- Cognitive Science & Computational Neuroscience: Especially relevant in Mechanistic Interpretability. Researchers study neural networks the way neuroscientists study biological brains—probing activations, mapping neural circuits, and identifying feature representations.
- Formal Epistemology & Decision Theory: Foundational mathematics dealing with how an agent updates its beliefs under radical uncertainty, handles causal vs. evidential decisions, and defines utility functions.
