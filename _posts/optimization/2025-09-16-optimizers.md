---
layout: post
title: "On Optimization Methods in Machine Learning"
date: 2025-09-16
description: "This post discusses some thoughts on common optimization methods used in machine learning, which includes SGD, momentum, RMSprop, and Adam."
tags: math
categories: optimization
toc:
    sidebar: left
---

> This post discusses some thoughts on common optimization methods used in machine learning, which includes SGD, momentum, RMSprop, and Adam.

This post discusses some thoughts I have after watching the [some](https://youtu.be/NE88eqLngkg?si=Y6f4ciVDTaJoFeZh) [videos](https://youtu.be/NE88eqLngkg?si=uM4Kmt7uYn3nzRpo) on the common optimization methods used in machine learning, including SGD, momentum, RMSprop, and Adam.

Since we are in the realm of machine learning, let us denote the variable to be \\(W_t\\), representing the weights at iteration \\(t\\). The step-size will be denoted by \\(\eta\\) and be termed as the learning rate. The gradient oracle is represented as \\(g(\cdot)\\).

Different optimization methods have their own advantage and disadvantage. Knowing the respective properties allows one to use the "right" method for specific task at hand.

## Stochastic gradient descent
The most basic method of them all is the stochastic gradient descent. The usual gradient descent is calculated by having
<p>

$$
g(W) = \nabla J(W),
$$
</p>
where \\(J\\) is the loss function. However, in the case of a learning problem, the exact value to \\(J\\) actually depends on the *data distribution* that we want to learn. Consider data being denoted by a random variable \\(\boldsymbol{\xi}\\), we have
<p>

$$
J(W) = \mathbb{E}_{\boldsymbol{\xi}}[Q(W;\boldsymbol{\xi})].
$$
</p>
The expectation can be approximated by an averaging over the whole dataset.

This might be pretty costly as there can be **a lot** of data. And calculating the average of so many terms only attributes to a single gradient step. Pretty inefficient, isn't it. Instead, we can take the approximation by an average over a smaller batch. Or in the extreme case, take
<p>

$$
g(W_t) = \nabla_W Q(W_t;\boldsymbol{\xi}_t), \text{ and } W_{t+1} = W_{t} - \eta g(W_t).
$$
</p>
This is stochastic gradient descent, or SGD for short. The stochasticity (randomness) originates from the gradient being computed using random sampling of the data distribution.

### Disadvantage of SGD
#### Stuck at local minima?
One might assume that similar to the usual gradient descent, SGD also suffers from easily getting stuck in local minima. However, this is simply not the whole picture.

As depicted in [this video by Welch Labs](https://youtu.be/NrO20Jb-hy0?si=ZV1VWD79zVV76qWD), for each different data sample \\(\boldsymbol{\xi}_t\\), the optimization loss landscape is different for each SGD update iteration. In order for SGD to be stuck at a local minima, it is required that it be stuck at the same point for ALL samples \\(\boldsymbol{\xi}\\)'s. Which, if you think about it, is not an easy task.

The stochasticity inherent within the method actually helps *kick* the iteration away from local minima.

#### Slow convergence
An important disadvantage to SGD that is mentioned by both videos is its slow convergence to the global / local minima.

As \\(W_{t}\\) gets closer and closer to the global / local minima, the size of the gradient becomes smaller and smaller and the movement becomes slower and slower. We need a way to improve this, to make the descent go a bit faster.

## Momentum
The momentum methods addresses the slow convergence of SGD near minima by including *intertia* into the update law. The *momentum* \\(M_t\\) represents the velocity of a point, viz., the update law is \\(W_{t+1} = W_{t} - \eta M_{t}\\).

The movement \\(M_t\\) at a point \\(W_t\\) is not only determined by its current gradient \\(g(W_t)\\), but also by the movement / momentum from previous iteration \\(M_{t-1}\\). The update law for GD with momentum is thus
<p>

$$
\boxed{
\begin{aligned}
    M_{t} &= \beta M_{t-1} + (1-\beta) g(W_t), \\
    W_{t+1} &= W_{t} - \eta M_{t}.
\end{aligned}
}
$$
</p>
The size of the inertia is denoted by \\(\beta\\), often given the value of \\(0.9\\). The new momentum is a weighted sum of previous momentum and current gradient. The inclusion of such a weighted sum allows for faster convergence speed when one has gradients pointing in similar directions across iterations.

The disadvantage of momentum will be discussed later when we are considering Adam.

### Nesterov momentum
The Nesterov momentum can be viewed as an *optimistic* momentum descent. The mathematical formulation is as below:
<p>

$$
\boxed{
\begin{aligned}
    M_{t} &= \beta M_{t-1} + (1-\beta) g(W_t - \eta M_{t-1}), \\
    W_{t+1} &= W_{t} - \eta M_{t}.
\end{aligned}
}
$$
</p>
The optimism here means that the Nesterov momentum *looks ahead* and computes the gradient at a point that the algorithm *predicts* it to be at instead. As computing the momentum at the predicted point actually gives a more accurate description of the future behavior, this look-ahead might give a finer adjustment to the momentum and improve the convergence rate (if the loss function is well-suited).

## RMSprop
In optimizing a function of the form
<p>

$$
J(x_1,x_2) = 100 x_1^2 + 0.01 x_2^2,
$$
</p>
the gradient computed in the \\(x_1\\) direction will be way larger than the gradient in the \\(x_2\\) direction. This seems unfair! We should make the update in both direction be of same size as they are both just minimizing a quadratic function. How can we normalize the gradients? The root-mean-square propagation method considers exactly this.

Consider the \\(i\\)th parameter \\([W _t] _i\\), its update law is
<p>

$$
\boxed{
\begin{align*}
    [ v _{t+1}] _{i} &= \beta [v_{t}]_i + (1-\beta) [g(W_t)]_i^2, \\
    [W_{t+1}] _{i} &= [W_{t}]_i - \frac{\eta}{\sqrt{[v_{t+1}]_i} + \varepsilon} \cdot [g(W_{t})]_i.
\end{align*}
}
$$
</p>
The vector \\(v_t\\) records the *(root-mean-square) variance* of each component of the update, it is updated by weighted average. The small number \\(\varepsilon\\) is for numerical stability. Note that components with a larger RMS is dampened to be smaller, while those that have smaller RMS is enhanced.

The disadvantage to RMSprop is a bit similar to that of SGD.

### Note
The [Muon optimizer](https://leloykun.github.io/ponder/steepest-descent-non-riemannian/) with its Newton-Schulz iteration and Finsler manifold optimization actually has the same spirit has RMSprop: to **normalize** the update directions.

## Adam
Adam is a combination of both momentum and RMSprop.

Further more, as stated in the paper "[Old Optimizer, New Norm: An Anthology](https://arxiv.org/abs/2409.20325v1)", Adam is simply the combination of (1) an optimization over the \\(\ell_\infty\\)-norm, which corresponds to the normalization of RMSprop, and (2) the *exponential moving average* (EMA), which corresponds to the weighted sum of present and past mean and variance of step in momentum methods.

### Disadvantage of momentum
Besides going too fast so that the iteration might escape of minima (which can also be a benefit in some scenarios), momentum methods suffer from cases where *averaging* is not beneficial.

In applications such as reinforcement learning, the environment to the system might change abruptly. In these cases, the past momentum information bear little to none resemblance to the present gradient. The weighted sum between previous momentum and present gradient might lead the update astray from the right direction, thus worsening the performance.

---
In conclusion, momentum allows faster speed to convergence when close to the minima and the optimization landscape is not changing, while RMSprop allows for normalized sizes of update across all coordinates.