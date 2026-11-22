---
layout: post
title: "Obstacles to mindreading: Simple, irreducible, and instrumental opacity"
date: November 21, 2026
location: Berkeley
---

Sometimes there's an entity in the world, and after observing that entity's behavior, I choose to [model it as an agent](https://en.wikipedia.org/wiki/Intentional_stance): that is, something that "seeks" some objective. I think I usually do this because I want to predict the entity's behavior in circumstances I haven't observed.

-   I see a weird, wet-looking thing on a rock, moving slowly, with a trail of slime behind it. I might choose to model it as seeking to move in some particular direction. I avoid putting my book down right in front of it, to avoid getting slug slime on my book.
-   I see a tree growing in a cave, with all its branches growing toward the cave entrance. I might choose to model it as aiming for its leaves to be in the sunlight. After seeing lots of examples I might generalize: trees aim for their leaves to be in the sun - I might arrange my garden so that the effect of the trees seeking sunlight is visually pleasing, and the trees' growth toward sunlight won't block pathways in the garden.
-   I see a man with half a plate of food in front of him, fork moving some of the food into his mouth, seeming to enjoy the meal. I might choose to model him as seeking to ingest the food. "I'll have what he's having," I tell the waiter.

"Why is it doing that?" I might ask, about an entity. Some answers will be "internal" reasons (internal to the frame of treating that entity as an agent).

-   "He answered 'A' for that question because he believes Napoleon was German"
-   "It grabbed the fruit because it's hungry"

Other answers will be "external" reasons, that don't stay inside the agentic frame.

-   "It's moving its legs like that because its neurons are firing in such-and-such a pattern and that's leading its muscles to contract like so"
-   "It's falling because it is denser than the medium it's embedded in"

Often, internal reasons have internal reasons of their own.

-   "I'm typing this word on my phone, because I'm typing this sentence on my phone, because I want you to read it, because I want you to know that I will be late, because I don't want you to be as annoyed with me when I don't arrive on time, because I value your friendship"

But sometimes an entity's internal reasons will be "opaque" to me, given the behavior I can observe.

Maybe there simply are no prior internal reasons for the things I observe or infer.

-   The thermostat 'wants' the temperature to match its set point, and when I try to ask "why" it wants that, I find myself only able to find reasons that are more "external": "That's what its manufacturers designed it to seek," or "that's what its firmware is tuned to optimize for." If I try to ascribe more-internal reasons to it, they seem at least a little false: "It thinks the set point is the 'right' temperature for it to be", or "It wants to please its operator" both feel like too much of a stretch; maybe because they don't seem to add anything to my predictions of how the thermostat will behave. Other agents eventually run out of "internal reasons" too.

Or maybe there are prior internal reasons, but they are not visible to me: they are "opaque".

-   A poker player raises. Is she bluffing?
-   When you told me the time, did you know that the clock is broken?
-   Does the author of this edgy tweet sincerely believe that, or are they being ironic, or are they trolling?

Some of this opacity (we might call it "simple opacity") is there because I am merely a little ignorant of some of the agent's behavior, and if I looked more carefully, or in new settings, I'd see enough information to see through the opacity. Some ("irreducible opacity") is logically present for any entity that I'm modeling as a certain kind of agent. And some is what I'd call "instrumental opacity": places where the agent is intentionally hiding its internal reasons from me or from the world.

In the case of simple opacity, I may have just not seen enough information, or made sufficiently good inferences, but the information is not structurally hidden from me.

-   Do you like eating ice cream? What's your favorite color? I haven't checked, so I simply don't know.
-   I see a robot picking up red balls but not green cubes. Does it want to pick up red things but not green things? Or balls but not cubes? I might figure it out by presenting the robot with a red cube (assuming the robot isn't trying to fool me).

Irreducible opacity is usually relative to some particular modeling assumptions: I might try to infer an agent's utility function from its apparent preferences or behavior, but its utility isn't structurally possible to fully disentangle from that agent's beliefs or rationality.

-   I learn that you're spending some effort on entering a sweepstakes for a date with Henry Cavill. Is that because you think there's a good chance you win, and you might like a date with Henry Cavill? Or is it because you think there's a tiny chance you'll win, but you expect that a date with Henry Cavill would be a life-changing-ly good experience for you?
    -   The general form of this - where I might know all your preferences and still not be able to distinguish your beliefs from your values - has been called the "[Jeffrey-Bolker rotation](https://www.lesswrong.com/posts/oheKfWA7SsvpK7SGp/probability-is-real-and-value-is-complex)".
-   Or, still not knowing you, I might notice from watching videos of you on YouTube that you apologize a lot, and that sometimes this leads people to feel uncomfortable and look down on you. Do you do it because you really like apologizing in spite of those effects? Or because you haven't noticed or thought through the consequences?
    -   Stuart Armstrong and Sören Mindermann point to a very general issue like this in inverse reinforcement learning, in their paper "[Occam's razor is insufficient to infer the preferences of irrational agents](https://arxiv.org/abs/1712.05812)".

The most dramatic category is instrumental opacity: The agent wants me not to know its internal reasons, so it shapes its behavior to prevent me from learning them.

-   "Why did you step on my foot?" "Oh sorry, I'm so clumsy!" (but really the person is very angry at me)
-   I'm told that poker players "[protect their range](https://www.pokerskill.com/poker-glossary/range-protection/)": They try to behave in a way that's consistent with many possible hands, while still maximizing the expected value of their strategy.
-   "I can neither confirm nor deny": [Glomarization](https://en.wikipedia.org/wiki/Glomar_response) is a form of instrumental opacity.
-   Intelligence and law enforcement agencies seek "[parallel constructions](https://en.wikipedia.org/wiki/Parallel_construction)" so that they can act on secret information without revealing that they have that information.

Different kinds of opacity suggest different remedies: To resolve simple opacity, I need some information that I could probably get from additional observations or interactions. I can't fully resolve irreducible opacity while sticking to internal reasons, but I can sometimes make different modeling assumptions, or I can choose to predict behavior a different way using external reasons ("What are some structural properties of the policy this AI system implements, regardless of my modeling it as an agent?"). Resolving instrumental opacity may be quite difficult: If you're a skilled adversary, who can outsmart or outmaneuver me, there may be little I can do to learn your true internal reasons - more observation may only solidify my confusion. In some more well-behaved cases, I might be able to incentivize transparency, with (say) [proper scoring rules](https://en.wikipedia.org/wiki/Scoring_rule).

_Thanks to Rafe Kennedy for labeling "internal" and "external" whys, Jeremy Schlatter for the example of poker players "protecting range", John Salvatier for help thinking about the taxonomy and terminology, and various AIs (Claude Fable 5.2, GPT-6.2 Astra, Gemini 4 Carbon) for feedback on the essay._

*You can discuss this post on [LessWrong](https://www.lesswrong.com/posts/3znHBDGQWBjhWEKcQ/obstacles-to-mindreading-simple-irreducible-and-instrumental).*
