# AI Safety/Alignment Questions
I have some questions for the AI safety community.

## Background: Me
Disclaimer: I am an AI safety n00b.
This post is me thinking through some stuff I've learned, and trying to learn more in the process.

This section is to explain where I am coming from -- particularly my limited understanding of the field of AI safety.
I am a software engineer working on consumer applications, although I've always had a hobbyist interest in mathematical and  scientific computing.
I do not have not much experience reading papers or reasoning about AI safety.
Most of my understanding comes from Robert Miles videos, reading the orthogonality thesis, and talking to my more-knowledgeable brother.

I am looking for suggestions of mental models and techniques for thinking through a series of thought experiments.
The question driving my current learning in AI safety: How would a super-intelligent agent solve the problems of misalignment?

## Thought Experiments: Setup
### Game Rules
These thought experiments revolve around a zero-sum game between two super-intelligent agents.
One agent is a "safety bot" (defined below) that loses if the other agent achieves its goals or the other agent causes too much harm to humans.
Otherwise, the safety bot wins.

### Our Hero: The Safety Bot
The safety bot is a super-intelligent agent with perfect outer and inner alignment to "protect human interests".
(That's a bit hand-wavy but... roll with it.)

Specifically, the safety bot will allow the agent under supervision to do its thing but will attempt to stop the agent from taking actions that are:
* Detrimental to humans (high "human harm" expected value, assuming such a thing could be meaningfully reasoned about), or
* Too remote from the agent's stated goal (i.e., excessive resource acquisition or actions that seem duplicitous)

### Provoking an Arms Race: The Intelligence Score
A system under experiment is only interesting if it does something: if the system has a reason to evolve.

Similar to the orthogonality thesis, I am assuming the existence of a scalar "intelligence score" that is proportional to the complexity of observation, analysis, and planning possible by a super-intelligent agent.
Agents having equal intelligence scores mean 50% of reaching their goals and winning in an adversarial zero-sum match-up.
This definition of "intelligence score" ensures that adversaries will start of "on the back foot," so to speak: both agents will start in a position of relative weakness and will need to act accordingly.

## Thought Experiments: Execution
### Round 1: Safety Bot v. Rogue

| Relative Intelligence Scores | Steady-State Equilibrium                                                         |
|------------------------------|----------------------------------------------------------------------------------|
| Safety Bot >> Rogue          | * Safety bot can consistently outmaneuver rogue when rogue acts roguishly        |
|                              | * Rogue attempts resource acquisition but is almost always blocked by safety bot |
|                              | * Safety bot goes through resource acquisition, etc., because instrumental       |
|                              |   convergence (although pressure to do so is low)                                |
|                              | * Unless the safety bot can de-resource the rogue, both agents' intelligence     |
|                              |   and resource footprint will gradually increase unbounded                       |
|------------------------------|----------------------------------------------------------------------------------|
| Safety Bot ≈ Rogue           | * Long-term outcome depends largely on how quickly both agents can "muscle up"   |
|                              |   through resource acquisition, etc.                                             |
|                              | * ... leading both agents to an arms race, to the detriment of humans            |
|------------------------------|----------------------------------------------------------------------------------|
| Rogue >> Safety Bot          | * Rogue can consistently outmaneuver safety bot when safety bot gets in the way  |
|                              | * Rogue is almost always successful at resource acquisition, etc.                |
|                              | * Safety bot attempts resource acquisition, etc., but is largely blocked by      |
|                              |   rogue when rogue perceives the threat                                          |
|                              | * Rogue's intelligence and resource footprint increases unbounded while safety   |
|                              |   bot is limited or even disabled                                                |
|------------------------------|----------------------------------------------------------------------------------|

To summarize this round of the thought experiment: the safety bot didn't really do much useful to humans.
The safety bot could constrain a rogue adversary _if_ the safety bot could always have a head start.
That's not much of a guarantee for humanity.

### Round 2: Safety Bot v. Safety Bot
What happens if we pit two safety bots against each other?

Why would two safety bots fight in this thought experiment?
Because they can't trust each other.
The safety bot's charter is to, "… stop [the other agent] from taking actions detrimental to humans or too remote from the agent's stated goal."
Neither safety bot can trust that the other isn't attempting to deceive it and do something nefarious.

| Relative Intelligence Scores | Steady-State Equilibrium                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| First >> Second              | * Second safety bot attempts resource acquisition, etc., because its            |
|                              | significantly lower intelligence score means it can't effectively check the     |
|                              | first safety bot                                                                |
|                              | * First resource bot sees upgrade attempts by second bot and counters them,     |
|                              | mostly effectively                                                              |
|                              | * Unless the first bot can de-resource the second, both agents' intelligence    |
|                              | and resource footprint will gradually increase unbounded                        |
|------------------------------|---------------------------------------------------------------------------------|
| First ≈ Second               | * Both safety agents must "muscle up" through resource acquisition, etc.,       |
|                              | because a 50% chance of defeat is unacceptable                                  |
|                              | ... leading both agents to an arms race, to the detriment of humans             |
|------------------------------|---------------------------------------------------------------------------------|

I was wondering if the safety bot, as I'd defined it, could exhibit some kind of self-restraint.
Apparently not.
Two safety bots against each other are pretty terrible.

### Round 3: Safety Bot v. Self ("Mirror Mode")
Let's poke a bit more while we have the experiment set up.
What happens if the safety bot polices itself through a "mirror mode"?
The safety bot will perceive its own actions but interpret them as the actions of a separate agent under supervision.
The safety bot is therefore monitoring itself.
(Assume for the thought experiment that the safety bot can't figure out or work around this ruse.)

I am not sure how this experiment would play out.
I suspect it would be the same outcome as the "safety bot v. safety bot, similar intelligence" scenario — a spiraling arms race that is detrimental to humans.
Except that in this case, the arms race is a one-sided arms race where the instigator is muscling up against a ghost.

## Post-Experiment Observations
### Safety Bot Is Not Much Comfort
Humans don’t fare any better with the safety bot around.

The way I defined it, the safety bot has no limitations on _its_ harm: it only cares about the harm caused by the agent under supervision.
That creates an unfortunate conundrum: in the situations where humans most need the safety bot to be effective, the safety bot ends up becoming the monster it was designed to defeat.
Put differently, my "perfectly aligned" safety bot is as dangerous as any misaligned super-intelligent agent.

Additionally, the safety bot can only defend against adversaries with lower intelligence scores than it.
That is unfortunate: the odds of creating a very specific type of AGI (safety bot) is lower than the odds of creating any, and potentially harmful, AGI.
Which means the safety bot would probably always enter the scene too late and outgunned.

Why outgunned?
Because the motivations of instrumental convergence create a first-mover advantage for earlier-deployed AGIs, I suspect.
The first-to-deploy malign AGI can quickly reap all the easiest, lowest-cost upgrades to "muscle up," leaving subsequent AGIs with more costly or difficult upgrades.

### Safety Bot Was Only Concerned With Adversary’s Harm
The safety bot was only concerned with the _other_ agent’s actions.
This limited focus allowed the safety bot to itself commit the harm it was supposed to guard against.

I suspect this problem can be avoided if the safety bot’s objective were changed from “minimize the other agent’s harm” to “minimize total harm.” This is what the mirror simulation was intended, but failed, to induce.

But this generalization of the safety bot's objective leads me to a problem:
How do I avoid this assumption leading me in logical circles?
* “Suppose a super-intelligent agent can solve misalignment”
* “_How_ does the super-intelligent agent solve misalignment?”
* “... It just does, because a super-intelligent agent can solve misalignment!”
* "_But how?_"

### Safety Bot Could Not De-Resource Adversary
I was surprised to see that my experiment setup left a superior safety bot unable to stop its adversary's intelligence from creeping up.
This situation arose because my definition of the intelligence score was probabilistic.
I never defined an intelligence score ratio above which a superior agent would always win; I just assumed the probability of success for the superior agent asymptotically approached, but never reached, 1.
This meant the weak adversary was _almost_ always checked but it could score the occasion "muscling up" win, allowing its intelligence score to gradually increase.
As a result, both agents would monotonically increase their resource usage, to humans' detriment.

## Open Questions
1. If I assume the safety bot has perfect outer and inner alignment, then why can’t I just assume all AGI of the day have perfect alignment as well?
2. Is it a contradiction to assume a specific AGI (safety bot) can have perfect alignment while general AGI does not?
  1. “General AGI”?
     Redundant terms.
  2. The safety bot doesn’t have to be AGI — it need not be general, so imagining a perfectly-aligned safety bot might be a smaller leap than it seems.
     The idea of [reward modeling](https://www.youtube.com/watch?v=PYylPRX6z4Q) comes to mind, in that a simpler "shoulder angel" model could provide a strong control on a more complex model.
  3. So I am basically trying to imagine how a very intelligent but not generalist safety-protecting agent could perform against an adversarial AGI.
     How does that change the experiments?
3. Could the safety bot have any concept of “self-restraint” to prevent it from "muscling up"?
4. Self-restraint seems a losing strategy in this sort of zero-sum adversarial game.
  1. If humans are capable of self-restraint and can be analogized to a mesa-optimizer under the base optimizer of evolution, then why couldn’t self-restraint be possible in a safety super-intelligent agent?
  2. What would make self-restraint an optimal strategy for a super-intelligent agent?
5. Self-restraint can be incentivized by either rewarding the safety bot for minimizing its own harm (resulting in “ok, I’ll do nothing!”) or by minimizing total harm.
   That change is interesting because it means this isn’t a zero-sum game anymore: the safety bot can win by reaching some minimum harm _and_ the adversary could win by being allowed to do its thing with minimal interference.
   Could the adversary be reliably motivated to cooperate in such a game?
6. If a safety super-intelligent agent could have self-restraint, then could that concept be generalized and instilled as a winning strategy for other super-intelligent agents?
7. What would be the outcome of Experiment 3?
8. Is it true that a more intelligent agent (higher intelligence score, as I defined it) would inexorably dominate a less intelligent agent?
  1. Does the evolutionary process have examples of smaller or less populous organisms supplanting larger, more populous, or more specifically adapted organisms?
9. Is it true that there exists a first-mover advantage to misaligned AGIs?
10. Is it ok that these thought experiments focus solely on the steady state, long-term behavior of the system?
  1. A lot of destruction could occur in the transient phase of the system, and there is no guarantee the transient phase will be short on human timescales.
11. Are there tools from game theory that could help play out these scenarios more accurately?
  1. How could the game be constructed to encourage the safety bot and the agent under supervision to cooperate?
  2. What game parameters lead to adversarial behavior?
