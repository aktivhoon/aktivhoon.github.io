---
title: The snapshot of intelligence
layout: post
tags: [Artificial General Intelligence, Machine Learning]
categories: [Opinion]
date: 2026-01-02 23:45:00 +0900
use_math: true
---

Looking back at 2025, there is a palpable sense that the industry's long-standing obsession with benchmarks is beginning to wane. We still care about benchmarks, but the focus has shifted from pure scores towards what new models can actually achieve. I do not have a clear idea why the narrative changed. It may be the 'AI bubble' fueling doubts about practical utility; it might be a growing gut feeling, as I predicted in an [earlier post](https://psych.ai.kr/posts/AGI-between-philosophy-and-profitability/), that benchmarks are insufficient indicators of true AGI; or, it might simply be people getting tired of seeing similar models with distinct benchmarks. I am not sure which would be the most plausible case. But I am pretty much sure that the era of scaling laws is reaching its dusk.

I have recently enjoyed listening to Andrej Karpathy and Ilya Sutskever’s insights on Dwarkesh Patel’s podcast, drawing a great deal of inspiration from them. It was especially interesting to hear both of them specifically invoke 'evolution' and frame it as the biological process equivalent to an LLM’s pretraining. Despite their consensus, I found myself disagreeing with this specific mapping.

## The Three-Layer Hierarchy

To understand where I diverge from the 'Evolution-as-Pretraining' analogy, let's first look at a neural network through a more rigorous lens. At its most basic level, an AI model is a function: $$y=f(x)$$. It maps an input to an output based on a set of weights. However, I would argue that the hallmark of true intelligence is not the function $$f$$ itself, but the process of efficient adaptation: the ability to find the right $$f$$ from only a few-shot experience. This capactiy for adaptation is what I call $$g$$.

If $$f$$ represents the crystallized knowledge of an agent, then $$g$$ represents its fluid intelligence. $$g$$ encompasses the learning rules, the synaptic plasticity, and the specific anatomical structures, which are the inductive biases that dictate which regions receive which inputs. It is the "seed" that allows an agent to metabolize a handful of real-world observations and permanently restructure its internal model. Without $$g$$, a system cannot truly learn; it can only recall. This learning engine, $$g$$, however does not emerge by accidient. It is the result of a higher-order optimization process; $$h$$, in other words, evolution. The evolution has searched the vast space of possible architectures and learning mechanisms to find the specific configuration of $$g$$ that is most efficient for survival in the veredical world.

Accepting this hierarchy, it becomes clear why mapping current LLM pretraining to "evolution" is fundamentally misleading. The modern AI research takes a lazy shortcut of the hierarchy process. Pretraining is an attempt to skip the development of $$h$$ and $$g$$. Instead of building a system that know *how* to learn, we are using massive compute to approximate a stable $$f$$, a frozen snapshot of human knowledge that mimics the *products* of intelligence without possessing the mechanism of it. We aren't building an agent that can grow; we are building a library that can talk.

## The Digestion Gap

To be fair, current LLMs exhibit a remarkable form of intelligence through In-Context Learning (ICL). They can successfully apply pretrained rules to new data and even extract novel patterns from a few examples provided in a prompt. In this sense, they are performing a simulation of adaptation. However, the true bottleneck (and the reason I believe we are hitting a wall) is the digestion gap.

In a biological system, there is no hard wall between 'learning' and 'being'. When we encounter a new rule, our $$g$$ (plasticity and learnig rules) ensures that this knowledge eventually modified our $$f$$ (synaptic weights). We digest the experience into our structure. In a LLM, the weights are effectively frozen during interaction. Even if we were to unfreeze them, current architectures lack the efficiency to blend new experiences into their permanent state. Because of their brittle and data-hungry learning process, it takes thousands of repetitions for a new fact to settle into the weights without causing catastrophic interference with existing knowledge.

Without a $$g$$ capable of efficient, online structural updates, the model is trapped in a loop of transient mimicry. It can handle the "now" within its context window, but it cannot move from $$f_{t}$$ to $$f_{t+1}$$ to become "more". It remains a ghost: a high resolution recording of past intelligence that can simulate the present, but lacks the hardware level metabolism to turn experience into self.

## The Impossibility of Veridcal Coverage

If the industry's current path is to skip the seed ($$g$$) and simply build a larger tree ($$f$$), then the ultimate goal must be veridical coverage: a model so vast that it has pre-recorded every possible truth about the world. However, I claim this goal is not just difficult; it is impossible. There are three fundamental reasons.

The first wall is computational irreducibility. Some might argue that the future is merely an interpolation of the past: with enough data, every new event is a rearrangement of old patterns. This assumes that the universe is a stable distribution where all possible outcomes are already statistically latent in the data. In reality, our world is a generative, open ended system where the only way to know the end state is to let the system run. 

Because reality is emergent, a pretrained model is mathematically confined to the convex hull of its training data. It can successfully navigate the space between points it has already seen, but it cannot interpolate its way into an state that requires the system to actually execute. Without online learning, the model is a spectator of a finished game, unable to participate in a world where the calculation is still unfolding.

This leads to the second wall, non-stationarity. While irreducibility suggests we cannot predict the calculation of the future, non-stationarity observes that the very rules of that calculation are constantly shifting. The world is an open system where the map itself is expanding in real-time.

Consider the emergence of new biological organisms, the birth of disruptive technologies, or the sudden pivots of global culture. These are not just new data points within an existing distribution; they are the creation of entirely new dimensions. The nuances of language evolve, and the underlying laws of the economy are rewritten by innovation. Without a high-efficiency $$g$$ to update its permanent weights, the model's veridical coverage decays.

The final barrier is causal opacity. Pure observation reveals correlations, but it rarely reveals true causality. As Judea Pearl has argued, to truly understand a system, an agent must intervene. It must be a participant, not just a spectator. To be clear, scaling laws managed to overcome this intervention gap by consuming a tremendous volume of relatively information-poor observations that are action blind. By seeing every possible sequence of human thought and action billions of times over, models could statistically approximate the causal links they were never allowed to experience directly.

However, we are reaching the limit of this strategy. This brute-force substitution is only a lazy approximation of intelligence. Without a $$g$$ capable of efficient online learning, the model cannot digest new causal truths the moment they appear in the real world. We have reached the point where no amount of passive data can replace the information-density of a single, well-timed intervention.

## Time to Shift Toward the 'Seed'

End of scaling laws does not signal the end of AI progress. We have spent the last decade perfecting the crystallized intelligence of $$f$$ and building the world's most impressive library. The next era of research will not be (or, must not be) about adding more leaves to a dead tree; it will be about rediscovering the seed. 

It is time to rethink what intelligence really is. What are the inductive biases or learning rules that enable efficient optimization of $$f$$ in real time? How can we build systems that efficiently digest experience into their weights? I personally believe that a good starting point would be to see what representations commonly emerge among different models. We can then think of what information and learning objectives must be given for the model to efficiently learn those representations. The goal is no longer to build a larger library of the known, but to engineer the mechanism of $$g$$ that allows a system to navigate and metabolize the unknown.

## References

1. [Andrej Karpathy - Animals vs Ghosts](https://karpathy.bearblog.dev/animals-vs-ghosts/)
1. [Andrej Karpathy on Dwarkesh Podcast](https://youtu.be/lXUZvyajciY?si=fknG2hMaUjdsU2eh)
1. [Ilya Sutskever on Dwarkesh Podcast](https://youtu.be/aR20FWCCjAs?si=gDfK3iUCLEEM17FD)
