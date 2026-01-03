---
title: AGI between philosophy and profitability
layout: post
tags: [Machine Learning, Artificial General Intelligence]
categories: [Opinion]
date: 2025-01-28 00:11:00 +0900
use_math: true
---

### OpenAI's o3 and the debate over true intelligence

On December 20, 2024, OpenAI revealed their new model o3, stating they are now exteremly near to achieving artificial general intelligence (AGI). The model performed signficantly better in numerous advanced level benchmarks, including AIME 2024, GPQA diamond, and EpochAI frontier math, with the most notable outcome being its performance in ARC-AGI (2024 version).

ARC-AGI task can be described simply as a pixel based puzzle game, with three to five input and output pairs of the tasks, followed by a final task with only the input listed. Humans can easily solve these problems with 75 perecent accuracy on average, while most of the language models before o3 struggled in solving the task (the o1's highest performance was about 32 percent). Given this, it is easy to imagine how surprising it was when OpenAI announced that their new model o3 performed nearly 83 percent in the ARC-AGI benchmark. François Chollet, who is one of the primary contributors to the development of ARC-AGI, claimed that [this does not imply that o3 is AGI](https://arcprize.org/blog/oai-o3-pub-breakthrough):

> ARC-AGI serves as a critical benchmark for detecting such breakthroughs, highlighting generalization power in a way that saturated or less demanding benchmarks cannot. However, it is important to note that ARC-AGI is not an acid test for AGI - as we've repeated dozens of times this year. (...) Passing ARC-AGI does not equate to achieving AGI, and as a matter of fact, I don't think o3 is AGI yet.

Recent research, however, gives us the impression that AGI is no longer a theoretical idea but rather a 'existential' challenge, that humanity may face in the next years. While the precise concept of AGI has yet to be determined, François Chollet [recently made a valid argument](https://www.youtube.com/watch?v=s7_NlkBwdj8). He thinks that determining AGI based on benchmarks is ill-posed:

> You are confusing the output of the process with the process itself. (...) The first thing to keep in mind is the distinction between a static skill and fluid intelligence. So between having access to a large collection of static programs to solve known problems like what LM (language model) would do versus being able to synthesize brand new programs on the fly to solve a problem you've never seen before.

Do I believe his argument is valid? In some ways, yes; in others, no. While I concur that the current benchmark approach would be insufficient to verify whether the system we constructed achieved AGI, I disagree with the distinction between static skill and fluid intelligence. In addition, I contend that the distinction between the two may not be of that great importance to the industry at large.
### Fluid intelligence is just a 'broader' static skill
A key hallmark of fluid intelligence is the ability to adaptively recombine previously learned skills or concepts to solve novel problems. In other words, fluid intelligence must possess the capability for *compositional reasoning*. By *compositional*, we mean the ability to break tasks into more fundamental building blocks and reassemble them in novel ways.

While reinforcement learning (RL) is not the most suitable method for solving all problems, it aligns with the current trend in AI, where intelligence is often evaluted based on the system's ability to provide an *appropriate response*. Given this context, it seems reasonable to adopt an RL perspective for further discussion.

In the RL framework, fluid intelligence can be described as follows: if an agent learns the policy $$\pi(a \vert s)$$ for a finite set of tasks ($$T_1, \cdots, T_k$$ ), represented as $$\pi(a \vert s, T_k)$$ , it should be able to infer $$\pi(a \vert s, T_{\text{new}})$$ for a novel task $$T_{\text{new}}$$. If we define the task using a parameter set $$\theta$$, then acquiring general knowledge of the task is equivalent to learning a generalized policy $$\pi(a \vert s,\theta)$$.



<img src="https://github.com/user-attachments/assets/830f1c32-2d38-4d08-bb15-feda03a2c79f" alt="Ring Manifold" style="zoom:10%;" />

For example, consider an agent learning multiple "'ring manifolds", each with a different angular offset in a 3D space. With finite set of these manifolds. After training on a finite set of such manifolds, if the agent discovers these ring manifolds can be unified as sections of a generalized "torus manifold," it gains the ability to quickly adapt to novel situations that also belong to this broader manifold. In this sense, fluid intelligence can be theoretically achieved by learning a more "generalized" static skill manifold, along with the ability to identify the appropriate "section" of it for a given task. From this viewpoint, fluid intelligence can be seen as merely an extension of static skill, generalized to a broader scope.

However, the true parameters underlying the real-world task are not explicitly provided. Many factors likely play a role in enabling human intelligence to infer the latent factors that compose the real world, but I believe language has contributed the most. Language inherently possesses the property of compositionality, and reflects fundamental principles of the world (See my [earlier post](https://aktivhoon.github.io/posts/What-is-language-really-for/) for more details). It is no coincidence that the success of large language models (LLMs) has marked a significant step toward achieving AGI. Language, as a medium for representing the building blocks of the world, has enabled neural networks to learn a broad static skill manifold. This manifold, in turn, can be conveniently "cross-sectioned" through *learned compositions*, allowing for versatile adaptation and problem-solving. 
[A recent study](https://openaccess.thecvf.com/content/ICCV2023/html/Dravid_Rosetta_Neurons_Mining_the_Common_Units_in_a_Model_Zoo_ICCV_2023_paper.html) supports this idea by demonstrating that langauge models tend to endorse invalid syllogisms when they align with world knowledge and reject valid syllogisms when they contradict it. However, [another study](https://arxiv.org/abs/2306.04031) showed that this phenomenon disappears when the model is explicitly instructed to rely on mathematical logic. This suggests that a model's ability to solve a task heavily depends on the components it has learned during training.

### AGI: a philosophical question, not a practical one
Since the current models like o3 are still not AGI, there seems to be something more needed to achieve it. While some may place faith in the scaling law, I personally disagree with its sufficiency. 

However, as I mentioned earlier, I would argue that whether we are truly heading towards AGI may be outside of the scope of the industry's primary interests. The question of whether the system has "true" fluid intelligence is more  philosophical in nature — and, in fact, it remains unclear what AGI truly is or even how "fluid" human intelligence actually is. What matters to the industry is whether a system can reliably solve a variety of tasks. If a system is sufficiently fluid to pass many real-world benchmarks of intelligence, it would not be a major concern if it falls short of a more pure or more theoretical definition of AGI.

<img src="https://github.com/user-attachments/assets/5b7a9b97-9652-4628-8a83-f937ea91df79" alt="Private investment" style="zoom:25%;" />

In the early 2020s, some predicted the arrival of a third AI winter. The reason for this concern varied, but I believe the lack of profitability was a significant factor. Nearly a decade had passed since deep learning triumphed in the ImageNet challenge in 2012, and six years had gone by since AlphaGo defeated the world's best Go players. Yet, there were very few —if any— companies that truly profited from AI. As the saying goes, the greater the expectations, the deeper the disappointment.

<img src="https://github.com/user-attachments/assets/98e07384-f31e-452d-a986-6cb09b528469" alt="Private investment in generative AI" style="zoom:25%;" />

However, I believe the release of ChatGPT completely changed the narrative. Its impact was monumental: suddenly, everyone was talking about AI. OpenAI’s monthly revenue surged to $300 million by August 2024, an explosive increase compared to early 2023. Starting with ChatGPT, the AI industry began generating a noticeable and substantial amount of profit. This shift is also reflected in the significant rise in private investment in generative AI throughout 2023. Today, there are numerous LLMs, including Claude, ChatGPT, Gemini, and the latest challenger, DeepSeek R1.

What I want to emphasize here is that the fundamental driver of current AI funding is rooted in the expectation of profitability, not the pursuit of AGI. While the desire to create true AGI may still motivate AI researchers, the reality is that the industry’s primary focus lies in making consumers willing to pay for the services these companies provide. For companies and developers, the goal isn’t to create an AI system that satisfies philosophical definitions of AGI, but rather one that can reliably address real-world challenges, automate processes, and create tangible value. This can largely be achieved with sufficiently broad static skills—though it’s clear that no current model has fully reached that level yet.

### AGI: a dream too costly?

Asking whether the industry should pursue AGI is essentially the same as asking wheter it's truly "worth it." In other words, is it really necessary to develop an AGI to create value? Consider the industrial revolution: while machines surpassed the physical capabilities of humans, we did not aim to create a single universal machine capable of handling every step in the manufacture process. Instead, it was far more efficient to develop specialized machines for each specific task. Why should it be any different for intellectual machines? Do we really need an intellectual system that knows everything? The question becomes even more pressing when we consider the enormous monetary expense currently being poured into the AI industry.

<img src="https://github.com/user-attachments/assets/db5c3dc7-59ef-493f-818c-8e49a8c896c0" alt="DeepSeek R1" style="zoom:50%;" />

[DeepSeek R1](https://github.com/deepseek-ai/DeepSeek-R1), released just last week by a Chinese hedge fund firm, has sent shockwaves through the industry. Remarkably, its training cost was only about $6 million, a stark contrast to the hundreds of millions spent by OpenAI. While the aspects of DeepSeek R1 that surprised AI experts might differ from what caught the attention of the general public, its rise to prominence is largely attributed to its outstanding performance. This highlights a fundamental truth: as long as the industry remains at the forefront of AI development, the market will prioritize performance over whether or not true AGI has been achieved.

This raises another question: if pursuing AGI is an inefficient strategy for dominating the market, why does it continue to attrtact so much attention? There could be several reasons for this.

One reason is the legacy of the idea that "you build the system, and the system learns the rest," a belief that has persisted since the early days of the deep learning era. This faith in the emergence of knowledge has been supported by several testimonies, such as [AlphaGo's famous move 37](https://en.wikipedia.org/wiki/AlphaGo_versus_Lee_Sedol#Game_2) or [AlphaFold](https://deepmind.google/technologies/alphafold/)'s groundbreaking contributions to synthetic biology. However, these testimonial moments were possible because the systems operated within a clearly defined and limited set of rules. The real world, by contrast, lacks such universally agreed-upon rules. As a result, we may eventually have to confront the fact that building AGI might not yield transcendental solutions for many problems. It may offer valuable insights, but not ones fundamentally beyond what more specialized, "static skill" systems can achieve.

Secondly, from a service perspective, it is simpler to have one universal solution that can address a broader range of consumer needs. Each inidividual has different purpose for using AI-based services, so having an AGI that excels across all field is more appealing than relying on multiple specialized services. However, can such a universal system maintain its position if achieving AGI comes with exponentially high costs? I would argue it cannot. 

AGI would inherently require immense computational power, making such systems highly centralized. However, there have already been studies suggesting a performance decline in models like chatGPT since their initial release. While there may be various reason for this, one key factor I'd like to highlight is that individuals preferences vary widely, and in some cases, are completely contradictory. These mixed reward signals can undermine the system's ability to satisfy all users effectively.

In my opinion, there is significant evidence suggesting that AI companies may shift their focus towards personalized, cost-efficient neural networks. Wheter we achieve the "rainbow" of true fluid intelligence in the next few years will likely determine the industry's trajectory. If AGI is reached, it could open an entirely new chapter. However, if it remains out of reach, the industry may pivot to developing personalized models, leaving AGI as a niche research area pursued by a smaller group of researchers with an interest in tackling "philosophical questions."

## References

1. [Chollet, F., OpenAI o3 breakthrough high score on ARC-AGI-Pub](https://arcprize.org/blog/oai-o3-pub-breakthrough)
2. [Chollet, F., Talk @ AGI-24: It's not about scale, it's about abstraction](https://www.youtube.com/watch?v=s7_NlkBwdj8)
3. [Dasgupta, I., Lampinen, A. K., Chan, S. C., Creswell, A., Kumaran, D., McClelland, J. L., & Hill, F. (2022). Language models show human-like content effects on reasoning. _arXiv preprint arXiv:2207.07051_, _2_(3).](https://web.stanford.edu/~jlmcc/papers/DasguptaLampinenEtAl22LMsShowHumanLikeContentEffectsInReasoning.pdf)
4. [Poesia, G., Gandhi, K., Zelikman, E., & Goodman, N. D. (2023). Certified deductive reasoning with language models. _arXiv preprint arXiv:2306.04031_.](https://arxiv.org/abs/2306.04031)
5. [AI Index report 2024, by Standford University](https://aiindex.stanford.edu/report/)

