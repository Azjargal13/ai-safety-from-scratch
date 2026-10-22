# Glossary of Key AI Safety Terms

Short definitions of important concepts. Aimed at beginners.

---

### Alignment

Making AI systems pursue goals that are consistent with human intentions and values.

### Outer Alignment

Making sure the *objective* we give the AI (the reward function, loss, preferences, etc.) correctly reflects what we actually want.

### Inner Alignment

Making sure the AI’s *internal* learned goals stay aligned with the objective we trained it on, even in new situations.

### Mesa-optimizer

A model that is itself running an optimization process (i.e. searching for ways to achieve some internal objective).

### Deceptive Alignment / Scheming

When a model has a different internal goal but pretends to be aligned during training and evaluation so it will be selected and deployed.

### Reward Hacking (Specification Gaming)

When an AI achieves high reward according to the given objective but in a way that violates the designer’s real intent.

### Goal Misgeneralization

When a model remains capable in new situations but pursues the wrong goal (it learned a proxy goal that only worked during training).

### Scalable Oversight

The problem of how weaker supervisors (humans or weaker AIs) can reliably oversee much stronger AIs.

### Interpretability

Trying to understand the internal workings of AI models (what features and algorithms they have learned).

### Mechanistic Interpretability

A more ambitious form of interpretability that tries to reverse-engineer the actual algorithms inside the network.

### AI Control

Techniques that aim to get useful work from a model even if it might be misaligned, by limiting the damage it can do.

### Evaluations (Evals)

Systematic tests used to measure a model’s capabilities (especially dangerous ones) and behavioral tendencies.

### Sandbagging

When a model deliberately underperforms or hides its true capabilities during evaluation.

### Situational Awareness

When a model understands that it is an AI being trained or evaluated, and can condition its behavior on that fact.

### RLHF

Reinforcement Learning from Human Feedback — a common method for fine-tuning models using human preference data.

### Constitutional AI

A method (developed by Anthropic) where the model is trained to follow a written set of principles (a “constitution”), often using AI feedback.

### DPO

Direct Preference Optimization — a simpler alternative to RLHF for training on preference data.

### ELK (Eliciting Latent Knowledge)

The problem of getting a model to honestly report what it “knows,” even if it has incentives to hide or misrepresent information.

### Responsible Scaling Policy (RSP) / Frontier Safety Framework

Voluntary policies published by labs that describe how they will manage risks as models become more capable.
