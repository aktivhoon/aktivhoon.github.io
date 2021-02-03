---
title: Generalization inference of brains and AI
layout: post
tags: [Neuroscience, Representation Learning]
categories: [Paper Review]
date: 2021-02-03 23:35:01 +0900
use_math: true
---

Despite the overwhelming victory of AlphaGo against human beings in 2016, artificial intelligence still does not replace human beings in many fields. Most artificial intelligence that has shown human-like (or even superior) performance in decision-making tasks are based on reinforcement learning algorithms. These algorithms however do not fully implement the ability to generalize what they have learned from millions of trials: if it is placed to another task, it will need another tremendous trial to learn to be good at it.

Animals in contrast have the flexibility to transfer knowledge learned from one domain to another. This enables them to quickly learn and adapt to new situations. People who study intelligence define this ability as **generalization**. If an intelligent system has truly understood the structure of the task, it can simply use the knowledge to adapt to tasks with the same structure, but different stimuli. Making artificial intelligence to understand the task structure is therefore the key to unlock the ability of generalization. Although it is not the only way to solve big questions in artificial intelligence, taking inspiration from the field of neuroscience is a very efficient approach to do so.

## Hippocampus and Entorhinal cortex: Capturing task specific features

The hippocampus is known to play important roles in various kinds of cognitive processes including generalization, memory, one-shot imagination, and navigation. The well-known **successor representation** model suggests place cells and grid cells found in the hippocampus and entorhinal cortex emerge based on learning the state transition matrix. According to conventional reinforcment learning algorithms, we can define state value function of state $$s$$ as below:


$$
V(s)=\mathbb{E} \left[ \sum_{t=0} ^{\infty} \gamma^t R(s_t) | s_0 = s \right]
$$


where $$s_t$$ is the state visited at time $$t$$, and $$\gamma \in [0, 1]$$ is decaying discount factor. The idea of successor representation is to decompose the value function into the inner product of the reward function with predictive representation of the state (SR), denoted $$M$$:


$$
V(s) = \sum_{s'} M(s, s')R(s')\\
\text{where } M(s,s') = \mathbb{E} \left[ \sum_{t=0} ^{\infty} \gamma^t \mathbb{I}(s_t = s') | s_0 = s \right] = \sum_{t=0}^{\infty} \gamma^t T^t
$$


where $$T$$ is the transition probability matrix.

<img src="https://user-images.githubusercontent.com/4964573/106280072-c24b9000-6280-11eb-80b9-19d17aa51dcd.png" width="500">

As shown in the figure ([K.L. Stachenfeld *et al.*, *Nature Neurosciene*, 2018](https://www.nature.com/articles/nn.4650)) above, the grid cell firing rate histograms are highly alike the low-dimensional eigendecomposition of the successor representation. These results suggest that the entorhinal cortex captures important features of the task structure.

Many research implying the important role of the hippocampus and entorhinal cortex in understanding and representing the task and stimuli cemented a theory neuroscientists are highly interested in, called **cognitive map theory**. Unlike the traditional belief that the hippocampus and its nearby structures have a very unique pattern in representing spatial memories, studies have begun suggesting that these brain regions represent non-spatial dimensions in a similar way.

## Hippocampal-entorhinal system in ANN

A study published by DeepMind ([A. Banino, *et al*., *Nature*, 2018](https://www.nature.com/articles/s41586-018-0102-6)) showed emergence of grid-like representations in neural networks using supervised learning. Thus, it indirectly proved the efficiency of grid-pattern coding to represent states in a spatial navigation task.

<img src="https://user-images.githubusercontent.com/4964573/106313376-6f3b0280-62ab-11eb-97c3-d866e2e55283.png" width="550">

Still, the neural network **required ground truth labels of what to predict**: in this case, the actual $$x, y$$ coordinates. Since $$x, y$$ coordinates of the agent is the most crucial feature to represent current states in spatial navigation task, approach done in the paper has limitations in explaining how animals and humans find what features they should learn to predict from high-dimension stimuli.

A paper published in NeurIPS 2018 ([J.C.R. Whittington, *et al*. *NeurIPS Conference*, 2018](https://papers.nips.cc/paper/2018/file/99064ba6631e279d4a74622df99657d6-Paper.pdf)) came up with a solution with this problem. Here, they considered an agent to passively move through a 2D graph while observing a non-unique sensory stimulus on each vertex. All task environments share the same structure, while varying in stimuli distributions. The agent should learn abstract representations of the task structure to quickly adpat to environments with different stimuli.

<img src="https://user-images.githubusercontent.com/4964573/106315092-15880780-62ae-11eb-969e-788ec74347de.png" width="700">

To acheive this goal, they propose grid cells to be the bases for constructing abstract representation of space, and place cell representation for the formation of fast episodic memories. Memories should link 'what' to 'where'. In other words, memories need to conjuct location information with sensory stimuli. In this paper they suggest place cells to form conjunctive representation between the sensory input and grid input.

The model proposed in the paper has two different networks: **Generative and Inference network**.

<img src="https://user-images.githubusercontent.com/4964573/106602991-14eabc00-65a1-11eb-8ee1-12aac35f950b.png" width="400">

### Generative Model

The agent have a generative model which factorises as

$$
p_{\theta} (\mathbb{x}_{\leq T}, \mathbb{p}_{\leq T}, \mathbb{g}_{\leq T}) = \prod^T_{t=1}p_{\theta}(\mathbb{x}_t | \mathbb{p}_t)p_{\theta}(\mathbb{p}_t | M_{t-1}, \mathbb{g}_t)p_{\theta}(\mathbb{g}_t | \mathbb{g}_{t-1}, \mathbb{a}_t)
$$



where $$\mathbb{x}_t$$ is the instantaneous sensory stimulus (one-hot vector where each of its $$n_s$$ elements represent a sensory identity) and latent variable $$\mathbb{p}_t$$ and $$\mathbb{g}_t$$ are grid and place cells. $$M_t$$ is the agent's memory composed from past place cell representations, and $$a_t$$ represents the current action. $$\theta$$ are parameters of the generative model.

### Inference Network

The posterior $$p(\mathbb{g}_t, \mathbb{p}_t \vert  \mathbb{x}_{\leq T}, \mathbb{a}_{\leq T})$$ is intractable, therefore we need to approximate it. The recognition distribution by the inference network can be factorised as below:


$$
q_{\phi} \left( \mathbb{g}_{\leq T}, \mathbb{p}_{\leq T} \vert  \mathbb{x}_{\leq T}\right) = \prod _{t=1} ^T q_{\phi}(\mathbb{g}_t \vert \mathbb{x}_{\leq t}, M_{t-1}, \mathbb{g}_{t-1}) q_{\phi}(\mathbb{p}_t \vert \mathbb{x}_{\leq t}, \mathbb{g}_t)
$$


where $$\phi$$ denote the parameters of the inference network.

### Grid Cells

##### Generative Model

From the equation above, $$p_{\theta}(\mathbb{g}_t \vert \mathbb{g}_{t-1}, \mathbb{a}_t)$$ is a Gaussian transition probability density, with the transitions taking the form as below:


$$
\mathbb{g}_t = f_{\mu_g}(\mathbb{g}_{t-1} + D_a \mathbb{g}_{t-1}) + \sigma \cdot \epsilon_t\\
\epsilon_t \sim \mathcal{N}(0, \mathbb{I})\\
\text{where } Vec[D_a] = f_D (\mathbb{a}_t), \,\, \sigma =f_{\sigma_g}(\mathbb{g}_{t-1})
$$


Some might struggle in understanding the exact meaning of $$D_a$$. Remind that $$f_D$$ is a multi-layer perceptron estimating the transition matrix for given action $$a_t$$. Thus, $$D_a$$ captures the state-to-state transition in the domain of $$\mathbb{g}$$, which is the abstracted latent space to encode states. The paper mentions to give restrictions to connections in $$D_a$$, so that connections are defined from low frequency to the same or higher frequency only.

##### Inference Model

$$q_{\phi}(\mathbb{g}_t \vert \mathbb{x}_{\leq t}, M_{t-1}, \mathbb{g}_{t-1})$$ can be factorized as below:


$$
q_{\phi}(\mathbb{g}_t \vert \mathbb{x}_{\leq t}, M_{t-1}, \mathbb{g}_{t-1})= q_{\phi} (\mathbb{g}_t \vert \mathbb{g}_{t-1}, \mathbb{a}_t) q_{\phi}(\mathbb{g}_t \vert \mathbb{x}_{\leq t}, M_{t-1})
$$


To know where we are, we infer grid code of current state $$\mathbb{g}_t$$, and this can be successfully done by integrating the path, as well as using sensory information we have seen previously. Note that each approach is captured in the factorized term, respectively.

### Place Cells

From the equation above, $$p_{\theta}(\mathbb{p}_t \vert M_{t-1}, \mathbb{g}_t)$$ is a Gaussian probability density for retrieving memories. Memories of place cells are stored in Hebbian weights between place cells. The learning rule to update the memory is as below:

$$
M_t = \lambda M_{t-1} + \eta (\mathbb{p}_t - \hat{\mathbb{p}}_t)(\mathbb{p}_t + \hat{\mathbb{p}}_t)^T
$$


where $$\hat{\mathbb{p}}_t$$ represents place cells generated from inferred grid cells. So before we move on to details about how place cells store memories, let's first go back and understand how they infer $$\mathbb{p}_t$$.

As mentioned previously, memory is a conjunction between sensorium and structural information from grid cells. Sensorium is obtained by first compressing the sensory data $$\mathbb{x}_t$$ to $$f_c(\mathbb{x}_t)$$. This enables the sensory data $$\mathbb{x}_t$$ to have same dimension as $$\mathbb{g}_t$$. After so, it is filtered via exponential smoothing into different frequency bands, $$\mathbb{x}_t ^f$$. To clarify why they use exponential smoothing, let's take a look at the definition of it. For time series $$x_t$$, the simplest exponential smoothed value $$s_t$$ will be:


$$
s_0 = x_0 \\
s_t = \alpha x_t + (1-\alpha)s_{t-1}, \,\,\, t>0
$$


We can re-write this as


$$
s_t = \alpha \sum_{k=0}^t (1-\alpha)^k x_{t-k}
$$


Now if we define $$\alpha x_{t-k}$$ as $$c_k$$ and estimate $$(1-\alpha)^k$$ to be $$\text{exp}(-k\alpha)$$


$$
s_t = \sum_{k=0}^t c_k e^{-k\alpha} \approx \int_{0} ^{\infty} c_k e^{-sk} dk
$$


Now we can say exponential smoothing is actually Laplace transform when $$c_k$$ is non-zero value only for $$k= 0 , 1, \cdots, t$$. Thus, exponential smoothing with coefficient $$\alpha$$ is very similar to Laplace transform of $$x_t$$ with $$s=\alpha$$.

After normalization step, each $$\mathbb{x}_t ^f$$ is conjuncted with $$\mathbb{g}_t ^f$$ to give mean of the distribution, $$q_{\phi} (\mathbb{p}_t \vert \mathbb{x}_{\leq t}, \mathbb{g}_t)$$.

An attractor network of the form $$\mathbb{h}_{\tau} = f_p (\alpha * \mathbb{h}_{\tau-1} + M_t \mathbb{h}_{\tau-1})$$ is used to retrieve memories, where $$\tau$$ is the iteration of the attractor network and $$\alpha$$ is the decay term. The input of the 

Stored memories are extracted via an attractor network using $$f_g(\mathbb{g}_t)$$.

