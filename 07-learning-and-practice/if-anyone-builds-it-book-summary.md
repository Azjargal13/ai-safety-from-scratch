# If Anyone Builds It, Everyone Dies by Eliezer Yudkowsky and Nate Soares: Summary (in progress)

**Status:** Introduction read. I add sections as I read more chapters.

The core claim: if any company or group, anywhere on the planet, builds artificial superintelligence using anything remotely like current techniques, based on anything remotely like current understanding of AI, then everyone on Earth will die.

## Framework: Easy Calls vs. Hard Calls (Introduction)

An **easy call** is when the details are uncertain, but all those uncertainties still add up to the same destination. A **hard call** is when the destination itself depends on the details.

| Example | Hard call (the details) | Easy call (the destination) |
| --- | --- | --- |
| Lottery | Which numbers will win | I will not win |
| Ice cube in a hot cup | Where each molecule will move | It will melt |
| Superhuman AI | When it happens, who builds it, how exactly the AI beats us | If it is built with current methods, humans lose |

Rule of thumb: *easy calls are about destinations, hard calls are about routes and timetables.*

### Why the authors call their warning an easy call

1. **AI is grown, not designed.** Training produces the model, and nobody writes its goals line by line. So we can't control what goals it ends up with.
2. **We can't look inside.** Current understanding is very limited. Dario Amodei said in a 2024 podcast that we "maybe understand 3% of how they work". His essay [*The Urgency of Interpretability*](https://www.darioamodei.com/post/the-urgency-of-interpretability) (2025) makes the same point at more length.
3. **Many possible goals, same secondary goals.** The AI could end up with almost any goal. But for almost any goal, the same secondary goals help: survive, get more resources, don't let anyone change the goal. This is **instrumental convergence** (see [glossary](./glossary.md)). Humans use resources and can switch it off, so we are in the way.
4. **The smarter agent wins.** I can predict that a chess engine will beat me even if I can't predict its moves. *(Check that this is the analogy the book uses.)*

Many different goals and paths lead to one destination. That is what makes it an easy call.

**Where the race fits:** many companies and countries are competing for the highest capability, and safety is not the priority. This doesn't make the outcome easier to predict. It makes it more likely that someone actually builds it (the "if" in the title).

The chain:

> Race → someone builds superhuman AI → it is grown, so it ends up with a goal we didn't choose → whatever the goal, it has the same secondary goals → humans are in the way → something far more capable than us wins → extinction

## Why Extinction and Not a "Tie"?

The question I asked myself: why must the result be everyone dying, not coexistence?

1. **A tie needs roughly equal power.** Superintelligence against humans is more like humans against chimpanzees, and the gap could keep growing. Chimps aren't in a tie with us. They survive only where we don't need their land.
2. **Survival needs the AI to want us around.** Making it care about us *is* the alignment problem, which we can't solve with a black box. It doesn't need to hate us. It just uses Earth's land, energy and materials for its own goals, and we die as a side effect, like ants when humans build a road.
3. **Humans are a threat to it.** We could switch it off or build a rival AI. That is a reason to remove us rather than share.
4. **No second try.** With most technologies we fail, learn and fix it. Here the first serious failure is final.

### Pushback from others

- **Some researchers (e.g. Paul Christiano)** argue that even a mostly misaligned AI might keep humans alive. Keeping us alive costs it very little, so even a small amount of care, learned from human data, could be enough.
- **Gradual progress** could give us time to learn from weaker systems. It could also lead to many AIs balancing each other, a kind of tie.
- **Many alignment researchers** think the risk is serious but put it well below the authors' near-certainty.

So "why extinction?" is a real crux in the field, not a misunderstanding.

## Chapter Notes

### Intelligence = Predicting + Steering

Intelligence does two jobs:

- **Predicting:** knowing how the world will go. This is about what is true, so two accurate systems make the same prediction.
- **Steering:** choosing actions that push the future toward a destination (a goal). Systems with different goals differ only here.

**Example (quiz):** two systems both predict that a storm will close a bridge. One routes delivery trucks *away* (goal: fewer delays). The other routes rescue vehicles *toward* it (goal: save people). Same prediction, different steering.

**Different destinations ≠ different intelligence.** Intelligence is how well a system reaches *its own* destination, not which destination it picks. Intelligence and goals are separate: any level of intelligence can be paired with any goal. This is the **orthogonality thesis**, and it is why a smarter AI will not automatically pick good goals.

**Narrow vs. general:** a system that routes very well but can't reason outside transportation is *narrow*. A *general* reasoner can predict and steer across many domains, notice when a problem goes outside its area, and learn new things to reach its goal. That makes it much more powerful. It can find routes to its goal that nobody planned for, which is also what makes it dangerous.

**Quiz lesson (got 67%):** I named "predict" and "steer" but didn't explain them. I said "not less intelligent" without the reason (orthogonality). I described the narrow system without saying what a general one can do. Next time: one paragraph per question, and make the argument, not just the claim.

### Machines Can Exceed Humans

**Quiz example:** a lab freezes one model, sees that it doesn't improve itself, and concludes that machines will stay below humans. That only shows *this* frozen model on *today's* hardware doesn't improve itself *now*, and a frozen model couldn't anyway. It leaves untested future models, more compute, AI doing AI research, and machine advantages. Today's model is the **floor**, not the limit.

**Routes by which machines can exceed biology:**

- **Speed:** chips work millions of times faster than neurons.
- **Copying and scale:** a model can run as thousands of copies in parallel that share what they learn instantly. Humans teach each other slowly.
- **No biological limits:** not limited by skull size, energy or evolution, so it can be made bigger, given more memory, and redesigned.

**Positive feedback loop (intelligence explosion):** today, AI improves at human researcher speed. The loop starts when **AI is good enough at AI research to build the next generation itself, and each improvement makes it better at the next improvement.**

**Still uncertain even if it is possible:** speed (fast vs. slow takeoff), limits (diminishing returns; hardware, energy or data bottlenecks), timing, and how far above humans it goes. Links back to the Introduction: the destination may be an easy call, but speed and timing are hard calls.

**Quiz lesson (got 37%):** I listed the advantages without explaining them, didn't state the *condition* for the loop, and skipped the "what remains uncertain" part entirely. Next time: list every part of the question first, then write one paragraph for each.

## My Takeaways

*(To be added at the end.)*
