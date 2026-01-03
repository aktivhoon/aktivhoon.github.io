---
title: Hippocampal spatio-predictive cognitive maps adaptively guide reward generalization
layout: post
tags: [Reinforcement Learning, Neuroscience, Representation Learning]
categories: [Paper Review]
date: 2023-09-23 22:31:00 +0900
use_math: true
---

## Key Ideas

* Humans live in complex, ever-changing environments. However, experiences are rarely independent, and environments are constructed with a statistical structure as it's backbone.
* Therefore, we can predict outcomes for situations which we never experienced by generalizing from the information we obtained in previous experiences
* Orbitofrontal cortex (OFC) is known to represent task states in situations where these are not directly observable. Thus, OFC might play crucial role in internal representation of the world. But how?

## Theoretical details & Methods
### Experiment design

<img src="https://github.com/aktivhoon/active_inference/assets/4964573/34c60b14-0bdf-499e-95b1-7a3583fd7f71" width="450">

The experiment is conducted for total three days.

**Day 1:** Participants freely navigate through the virtual arena, while being instructed to remeber the location of the stimuli. The stimuli only appeared when they approached close enough. After exploration, participants performed object location memory task by being placed to random location in the arena, and to navigate to hidden location of a presented stimulus. The replacement error was measured.

**Day 2:** For day 2, the participants were first provided to freely navigate through the virtual arena before the scanning session. Object location memory task *with feedback* was followed after the navigation. During the fMRI scanning session, participants were presented with the monsters for two seconds in a random order on a red or blue background. Occansionally, two monsters were presented simultaneously, and **participants had to choose which of the two monsters was located closer in space** to the monster they had seen immediately before the two montsters. After scanning session, another round of object location memory task was performed but *without feedback*.

**Day 3:** For day 3, the participants conducted another round of object location memory task, *without feedback*. During fMRI scanning session, they were presented pairs of monsters and instructed to **select the monster that would lead to the highest reward**. (Note: *reward distribution was related to the position of the monsters in space, and the context as indicated by the background color, and participants were instructed that they would recieve similar amounts of points for monsters located near each other in space*.) After the choice stask (still in the fMRI scanning session), **picture-viewing task** was performed in the scanner. Participants were instructed to **think about each monter's location in space and associated value**. Occassionally when two monsters were presented simultaneously, participants had to indicate which of the two monsters was located closer in space to the monster they had seen immediately before the two monsters, or which monster had a more similar value. After scanning session, snother object location mmeory task was done, followed by four brief tasks: 1) indicate sliding scale from 0 to 100 **how many points they would receive for each monster** in each context, 2) **rate how much they liked** each monster, 3) **arrange** monsters in an arena according to their **similarity**, or 4) **spatial location**.

### Modeling

#### GP regression

Using Gaussian-process regression model, we estimate the reward of given stimuli. The regression model can use multiple different kernels for reward estimation & generlaization.

For spatial cognitive map case, the kernel would be a Gaussian kernel:


$$
K(x, x') = \sigma_f^2 \text{ exp } \left( - \frac{\left\| x -x' \right\| ^2}{2\lambda^2} \right)
$$


where $$\sigma^2_f$$ is the parameter controlling the degree to which the predictions differ from the mean, and $$\lambda$$ is the lengthscale parameter.

For the case of predictive map, the diffusion kernel can be constructed based on the hypothesis that predictive relations for generalization. We can first start from computing the successor matrix $$M$$:


$$
M(s, s') = \mathbb{E} \left[ \sum_{t=0}^{\infty} \gamma^t \mathbb{I} (s_t = s') \mid s_0 = s \right]
$$




$$
\hat{M}(s, :) \leftarrow \hat{M}(s, :) + \eta \left[ \mathbb{1}_{s} + \gamma \hat{M} (s',:) - \hat{M}(s, :) \right]
$$

where $$\gamma$$ is the discount factor. From the definition of $$M$$, the transition matrix $$T$$ can be computed as:


$$
T = \frac{M^{-1}-I}{-\gamma}
$$


where $$I$$ is the identity matrix. The diffusion kernel $$K$$ can be formulated as


$$
K = \text{exp} (-\lambda L)
$$


where the $$L$$ is the normalized graph Laplacian which equals $$I-T$$.




## Results

### Both spatial and predictive relationship guide generalization

To test which map (spatial vs. predictive vs. spatio-predictive) best explains how participants generalized rewards, each GP model were made to predict the reward of both monsters, conditioning the GPs on all monster-reward pairs observed in the relevant context up to that point. The predicted difference in reward between the two presented monsters was entered into the mixed-effect logistic regression model to fit t he GP model.

<img src="https://github.com/aktivhoon/active_inference/assets/4964573/397e7ea3-225f-45db-9a86-41aabeff824f" width="600">

As shown above, (Left figure) **spatio-predictive map had the highest predictability among all GP models.** Also, the model-predicted value reproduced the difference in value rating for the high- and low-inference stimuli. (Right figure)

<img src="https://github.com/aktivhoon/active_inference/assets/4964573/435a2ab3-d191-4a38-b6c5-e6ca6c024cb2" width="600">

However, the **spatial effect and predictive effect size had negative correlation**, meaning **two maps might compete with each other in generalization process.** (Left figure) When comparing the spaital weight with the inference error, individuals who depended on the spatial map had lower mean inference error, meaning spatial map had higher accruacy in reward generalization. (Right figure)



### Hippocampus encoded spatial and predictive maps guide choices

The next question would be where and how exactly these spatial and predictive maps are encoded as neural representations. After the choice task on day 3, fMRI were obtained from participants. During scanning the stimuli were presented in random order on two background colors. After each stimulus, participants were presented with two stimuli and insturcted to report which one was either closed in space or more similar in value.

The basic idea for analysis was **fMRI adaptation**. The hypothesis is that *in regions encoding a cogntivie map of the stimulus relationships, the **size of the adaptation effect should scale with spaital and predictive relations between stimuli***.

<img src="https://github.com/aktivhoon/active_inference/assets/4964573/c558dda1-f579-4766-860e-21b19f8c9ebf" width="550">

The adaptation effect was tested by including spatial and predictive distances as a parametric modulator in the same GLM. For predictive distances, no voxels survived the conservative correction procedure, while for spatial distances, the **right hippocampal cluster** survived.

<img src="https://github.com/aktivhoon/active_inference/assets/4964573/cb9ece6c-9a2d-4df0-ad26-5e1395d2a0d5" width="580">

When compared the fMRI effect with the effect on choice behavior for both spatial and predictive map, the **fMRI effects were highly correlated with the effect on choice behavior**. However, the **performance itself was only predictable based on the spatial fMRI effect**, while predictive fMRI effect did not.

The next question we can ask will be whether the spatial and predictive influences on beahvior and neural map representation specific to the hippocampus. To answer the question, spatial and predicctive effects on choice behavior were included as covariates on the second level in the GLM. 

<img src="https://github.com/aktivhoon/active_inference/assets/4964573/a8e6b974-2858-43e4-ae13-ccdc528e1be7" width="580">

For both predictive and spatial map, localized clustered were found in the hippocampal formation. The representation of the spatial map in the hippocampas was stronger while the representation of the predictive map was weaker in individuals who made smaller inference error. Thus, **participants who represented the spatial map more strongly in the hippocampus were more capable to generalize according to the spatial distances in the choice task, and performed better in the inference task**.



### Representations of cognitive maps adapt to the task demands

Since the choice behavior is best explained with combination of both spatial and predictive map, we can hypothesize that individuals might adjust the degree to which they rely on one map over the another, depending on the outcome contingencies.

<img src="https://github.com/aktivhoon/active_inference/assets/4964573/585cbaa2-ee17-48aa-97f0-ff912d38b51e" width="850">

For most cases, the predictive map explained the generalization behavior in the choice task better initially, but **as the choice task progressed, the spatial map became more influential**. Additionally, the slope of the **logistic function was steeper in participants who performed better in the choice task and for inference task**. **Individuals with steeper slope** (meaning larger increase in the contribution of spatial map on choices) also showed a **larger increase in the neural representation of the spatial map**.

Next, a GLM that included a parametric regressor that reflected the difference in the degree to which the spatial map influneced choice from one trial to next (the weight update signal) was set up.

<img src="https://github.com/aktivhoon/active_inference/assets/4964573/5abd6c09-a7a8-4ba7-a6c5-4b7dd3ed24c7" width="650">

This identified a region in the left hippocampus. Furthermore, changes in the spatial map representation from session 2 to session 3 across the whole brain were measured, while using the parameter reflecting spatial weight update (extracted from the hippocampal ROI) as its covariate. The left hippocampal formation has shown a significant positive effect. Thus, **neural weight update signal might have led to an increase in the neural representation of the relevant map**.

Based on the fact that compositional map in the hippocampas have changed as the individual experienced reward contingencies in the choice task, we can assume there would be a relation between the reward prediction error and spatial updating signal. Then, the **fMRI signal must covary more with reward prediction error in participants whose hippocampal weight updating signal was stronger**. Moreover, the brain might also track how consistent the observed outcome is with the predictions made based on eight of the two cognitive maps, allowing the brain to adaptively adjust the cognitive map depending on task relevance.

<img src="https://github.com/aktivhoon/active_inference/assets/4964573/e57cf4bf-9e9d-4e2f-96a3-71b85e084a41" width="800">

For **reward prediction error**, regions including the **orbitofrontal cortex and the striatum, as well as the bilateral hippocampus** was observed. In the case of map accuracy, the trial-wise unsigned prediction errors for each outcome was calculated for both the spatial and predictive map. The difference between these prediction errors is the measurement of how much more expected outcome was according to the spatial as compared with the predicted map. As a result, **the orbitofrontal cortex was the only region where the relative map accuracy covaried with the hippocampal updating signal**.

Moreover, mediation path diagram was obtained to understand the relationship between relative map accuracy, spatial weight update, and change in spatial representation. **The relationship between the OFC signal and the change in hippocampal map representation was found, which can be fully accounted for by the hippocampal weight update**. 



## Food for thought

* What would have happened if some reward points were not defined based on the spatial distance, making the brain be confused about which map to use?
* Is the shift from one map to another continuous, or is it more of a discrete process, involving a dramatic shift from one map to another?



## References

1. [Garvert, M. M., Saanum, T., Schulz, E., Schuck, N. W., & Doeller, C. F. (2023). Hippocampal spatio-predictive cognitive maps adaptively guide reward generalization. *Nature Neuroscience*, 26(4), 615-626.](https://www.nature.com/articles/s41593-023-01283-x)