---
layout: post
title: "Proximal Map"
date: 2025-09-12
description: "What are proximal maps? Learn with me as I start reading from the book by Boyd."
tags: math
categories: optimization
toc:
    sidebar: left
---

> What are proximal maps? Learn with me as I start reading from the book by Boyd.

In the simplest Euclidean descent algorithms, I introduce how we can transform a descent optimization algorithm into a minimization problem
<p>

$$
    x_{t+1} = \arg\min_{x} \left\{\langle g,x\rangle + \frac{1}{2\eta} \|x-x_{t}\|^2\right\}.
$$
</p>
By replacing the squared distance with Bregman divergence, we obtain the mirror descent; replace it with norms, we obtained the steepest descent on normed spaces.

In this post, however, I discuss about what happens if we replace the inner product at the front with different things? It brings us to the optimization technique of proximal methods.

I have known the term "proximal maps" for a long time. I have met proximal maps before when dealing with Douglas-Rachford algorithms, also when I was learning about compressive sensing. Needless to say, the proximal map completes our basic toolbox of optimization after mirror descent. Reading through this [blog post](https://leloykun.github.io/ponder/steepest-descent-finsler/#3-general-solution-via-block-wise-primal-dual-hybrid-gradient-pdhg-algorithm), I came to see that it is about time I learn more thoroughly about proximal maps.

## Proximal method
This introduction to proximal methods takes main reference from [the book](https://web.stanford.edu/%7Eboyd/papers/pdf/prox_algs.pdf) by Parikh and Boyd.

Let \\(f\\) be a closed[^closed] convex function, then the proximal operator of \\(f\\) with step-size \\(\eta\\) is defined as

[^closed]: A *closed* convex function is one where its epigraph is closed.

<p>

$$
\mathrm{prox}_{\eta f}(v) = \arg\min_x \left\{f(x) + \frac{1}{2\eta}\|x - v\|_2^2\right\}.
$$
</p>
The norm \\(\\|\cdot\\|_2\\) is the usual Euclidean 2-norm. The minimizer is unique as the function inside is at least \\(1\\)-strongly convex.

### Examples

#### \\(f\\) is differentiable
If \\(f\\) is differentiable, then we obtain
<p>

$$
\mathrm{prox}_{\eta f}(v) = v - \eta \nabla f(v),
$$
</p>
which is the usual gradient descent method! This can be readily checked by applying the first-order condition for extrema.

#### Indicator function
Define the indicator function as
<p>

$$
I_C(x) = \begin{cases}
0, &x\in C;\\
+\infty, &x\notin C.
\end{cases}
$$
</p>
The indicator function is close convex if and only if \\(C\\) is also closed convex. Then, the proximal operator is
<p>

$$
\mathrm{prox}_{I_C}(v) = \arg\min_{x\in C} \|x-v\|^2,
$$
</p>
which is simply the Euclidean projection!


---
Interesting. The proximal map is kinda like a smoothed method that can be used to minimize a non-smooth function iteratively. A prime example is the indicator function in the example above. Another possible example is the minimization of the \\(\ell^1\\) function, which is used in compressive sensing.

As mentioned above, this post was written after I read through [this blog post](https://leloykun.github.io/ponder/steepest-descent-finsler/#3-general-solution-via-block-wise-primal-dual-hybrid-gradient-pdhg-algorithm). It seems suitable that I have myself be accustomed to the methods of proximal maps, alternating direction method of multipliers (ADMM), Douglas-Rachford, method, and primal dual hybrid gradient (PDHG) algorithm.

There is still much to be covered about proximal maps, but I have yet read those sections. So, until next time.
