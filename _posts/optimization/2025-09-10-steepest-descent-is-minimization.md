---
layout: post
title: "Steepest Descent as a Minimization Task"
date: 2025-09-10
description: "This post shows how gradient descent algorithms on Riemannian manifolds and normed spaces can also be recast into a minimization problem."
tags: math
categories: optimization
toc:
    sidebar: left
---

> This post shows how gradient descent algorithms on Riemannian manifolds and normed spaces can also be recast into a minimization problem.

It can be easily seen how gradient descent in an Euclidean space \\(V\in\mathbb{R}^n\\): let \\(x_{t}\in V\\), \\(\eta\in\mathbb{R}\\), and \\(g \in V^\* \cong V\\),
<p>

$$
x_{t+1} = x_{t} - \eta g
$$
</p>
can be viewed equivalently as the minimization task of
<p>

$$
x_{t+1} = \arg\min_{x\in V} \left\{\langle g,x\rangle + \frac{1}{2\eta} \|x - x_{t}\|^2\right\}.
$$
</p>
The inner product here is the usual Euclidean inner product, and the norm is the Euclidean 2-norm.

Let us argue how this description can be generalized.

First of all, if the norm is replaced by the [Bregman divergence](/blog/2025/Bregman-divergence), a squared distance, then we obtain the [mirror descent](/blog/2025/mirror-descent). What if we simply replace the norm by a norm that need not be induced from an inner product?

Before we move on, it should be noted that if the inner product term is modified from an inner product, then we are working with a different optimization method called the *proximal method*.

---
## Riemannian gradient descent
Note that I specify our task here as *Riemannian* as we are working with a manifold with a metric. This might no longer be the case if we work with steepest descent over a manifold equipped only with a *norm* and not an inner product (metric).

Given a manifold \\(\mathcal{M}\\) and a loss function \\(f:\mathcal{M}\rightarrow\mathbb{R}\\). The gradient descent algorithm at \\(x_{t} \in \mathcal{M}\\) is defined as
<p>

$$
x_{t+1} = \mathrm{Exp}_{x_t}(-\eta g),
$$
</p>
where \\(\mathrm{Exp}_{x}(th)\\) is the geodesic emanating from \\(x\in\mathcal{M}\\) with velocity \\(h\in T_x\mathcal{M}\\) at time \\(t\in\mathbb{R}\\). The *Riemannian* gradient vector \\(g\in T_x\mathcal{M}\\) is the unique tangent vector that satisfies the relation
<p>

$$
\mathrm{D} f(x)[h] \equiv \frac{\partial f(x)}{\partial x} [h] = \langle g,h\rangle _x
$$
</p>
for all \\(h\in T_x\mathcal{M}\\), with \\(\langle\cdot,\cdot\rangle _x\\) being the metric endowed onto the manifold.

### Retraction
In application, computing the geodesics is often a daunting task. Instead, one might use a *retraction* map in place of the geodesic map.

By definition, a *retration* on a manifold \\(\mathcal{M}\\) is a smooth mapping \\(R\\) from the tangent bundle \\(T\mathcal{M} = \cup_{x\in\mathcal{M}} T_x\mathcal{M}\\) onto \\(\mathcal{M}\\) with the following properties. Let \\(R_x\\) denote the restriction of \\(R\\) to \\(T_x\mathcal{M}\\), then
- \\(R_x(0) = x\\), where \\(0\\) denotes the zero element on \\(T_x\mathcal{M}\\).
- With the canonical identification \\(T_0T_x\mathcal{M} \cong T_x\mathcal{M}\\), \\(R_x\\) satisfies \\(\mathrm{D} R_x(0) = \mathbb{I}_{T_x\mathcal{M}}\\), which is the identity map on \\(T_x\mathcal{M}\\).

Given a retraction \\(R\\), the descent
<p>

$$
x_{t+1} = R_{x_{t}}(-\eta g)
$$
</p>
is equally valid to be a gradient descent algorithm.

### Riemannian manifold optimization as a minimization task
#### Euclidean case revisited
Let us separate the descent into two steps: (1) computing the descent direction, and (2) applying the descent.

For the Euclidean case, step (1) is to let the descent direction be \\(h\in T_{x_{t}}V \cong V\\) and let there be a dual vector \\(g\in V^\*\\), which is a function of \\(x_t\in V\\). The dual vector applies to a vector via the product \\(\langle\cdot,\cdot\rangle: V^\* \times V \rightarrow \mathbb{R}\\), not to be confused with the Euclidean inner product used above. Then, by noting that \\(x _{t+1} = x _{t} + h\\),
<p>

$$
h = \arg\min_{h\in V} \left\{\langle g,h\rangle + \frac{1}{2\eta} \|h\|^2\right\}.
$$
</p>
After obtaining the descent direction, the descent of step (2) is written as
<p>

$$
x_{t+1} = x_{t} - \eta g = x_{t} + h.
$$
</p>

#### Riemannian case
As for the Riemannian manifold optimization, similar results can be established.

Step (1), again, is to find the descent direction \\(h \in T_x\mathcal{M}\\). Notice that by definition of the notations, we have \\(\partial f/\partial x \in T_x^\*\mathcal{M}\\), and for all \\(k \in T_x\mathcal{M}\\),
<p>

$$
\frac{\partial f(x)}{\partial x}[k] = \left\langle \frac{\partial f(x)}{\partial x} , k\right\rangle.
$$
</p>
We want \\(h\\) to be the scaled negative *Riemannian gradient* \\(-\eta\mathrm{grad}f(x)\\), i.e.,
<p>

$$
-\eta \frac{\partial f(x)}{\partial x}[k] = -\eta \langle \mathrm{grad}f(x),k\rangle _x = \langle h, k\rangle _x
$$
</p>
for all \\(k\in T_x\mathcal{M}\\), where \\(\langle\cdot,\cdot\rangle_x\\) is the inner product of the manifold at \\(x\\).

The result is that
<p>

$$
\boxed{
    h = \arg\min_{h\in T_{x_t}\mathcal{M}} \left\{ \frac{\partial f(x_{t})}{\partial x}[h] + \frac{1}{2\eta} \langle h,h \rangle _{x_{t}}\right\}.
}
$$
</p>
The proof is as follows:
<p>

$$
\begin{align*}
    h &= \arg\min_{h\in T_{x_t}\mathcal{M}} \left\{ \frac{\partial f(x_{t})}{\partial x}[h] + \frac{1}{2\eta} \langle h,h \rangle _{x_{t}}\right\} \\
    &= \arg\min_{h\in T_{x_t}\mathcal{M}} \left\{ \langle \mathrm{grad}f(x_{t}), h \rangle _{x_t} + \frac{1}{2\eta} \langle h,h \rangle _{x_{t}}\right\} \\
    &\Leftrightarrow \frac{\partial}{\partial h} \langle \mathrm{grad}f(x_{t}), h \rangle _{x_t} + \frac{1}{2\eta} \langle h,h \rangle _{x_{t}} = 0 \\
    &\Leftrightarrow h = -\eta\cdot \mathrm{grad}f(x_{t}).
\end{align*}
$$
</p>
Thus it is shown.

Step (2) is to apply the retraction map as
<p>

$$
    x_{t+1} = R_{x_t}(h).
$$
</p>

A more standard form will be to replace the step-size by the sharpness parameter \\(\lambda = 1/\eta\\):
<p>

$$
\boxed{\begin{aligned}
    h_t &= \arg\min_{h\in T_{x_{t}}\mathcal{M}} \left\{ \frac{\partial f(x_{t})}{\partial x}[h] + \frac{\lambda}{2} \langle h,h \rangle _{x_{t}}\right\}, \\
    x_{t+1} &= R_{x_t}(h_t).
\end{aligned}}
$$
</p>

> ##### NOTE
> The goal of this section is to establish the boxed equation above, showing that for Riemannian manifold optimization: The "product" between a dual vector and the descent direction is simply the pushforward differential map applied onto the descent direction, and it should be written that way to avoid misinterpretations. The squared distance term is replaced by the norm induced by the Riemannian metric on the manifold.
> 
> This also explained a misconception I had a few days ago. The term \\(\langle g,x\rangle\\) is NOT an inner product. I should disentangle the descent direction from the iteration point, as the former lives in the tangent space while the latter resides on the manifold itself. With them disentangled, one immediately identifies that \\(\langle g,h\rangle\\) is simply a pushforward map on the tangent space. By writing the product as a pushforward map, there will be no need in explicitly stating the dual vector.
{: .block-warning}

---
## Normed vector space
This is from the paper "[Modular Duality in Deep Learning](https://arxiv.org/pdf/2410.21265#:~:text=Modular%20dualization%20involves%20first%20assigning%20operator%20norms%20to,the%20weight%20space%20of%20the%20full%20neural%20architecture.)", discussing how we can apply steepest descent method under a norm. Consider the iteration \\(x_{t+1} = x_t + \Delta x\\), what is the value of \\(\Delta x\\) given a *sharpness* \\(\lambda\\) and gradient \\(g\\)?

From the minimization formulation above, we see that a reasonable choice will be
<p>

$$
\Delta x = \arg\min_{\Delta x} \left\{ \langle g,\Delta x\rangle + \frac{\lambda}{2} \|\Delta x\|^2 \right\}.
$$
</p>

Why the use of a different norm? The use of a non-Euclidean norm allows us to give different *weighting* to different coordinate directions of the change in value \\(\Delta x\\) with respect to the gradient \\(g\\).

The numerical value of \\(g\\) might be large for a certain direction. But by using a different norm, the change \\(\Delta x\\) will favor a different direction.

### Solving the minimization problem
The solution to the minimization program above is
<p>

$$
\arg\min_{\Delta x\in V} \left\{ \langle g,\Delta x\rangle + \frac{\lambda}{2} \|\Delta x\|^2 \right\} = -\frac{\|g\|_*}{\lambda} \cdot \mathrm{dualize}_{\|\cdot\|}(g),
$$
</p>
where \\(\\|\cdot\\|_\*:V^\*\rightarrow\mathbb{R}\\) is the dual norm defined as
<p>

$$
\|g\|_* = \max_{x\in V,\|x||=1} \langle g,x\rangle = \max_{x\in V,\|x||=1} g^\mathsf{T} x
$$
</p>
and 
<p>

$$
\mathrm{dualize}_{\|\cdot\|}(g) = \arg\max_{x\in V,\|x||=1} \langle g,x\rangle
$$
</p>
is the duality map mapping a dual vector to a vector.

Let us prove this from scratch, the proof is from the work "[Old Optimizer, New Norm: An Anthology](https://arxiv.org/abs/2409.20325v1)": let the change \\(\Delta x = ct\\) where \\(c \ge 0\\) is a constant and \\(t\\) is a vector of length 1 in \\(\\|\cdot\\|\\). Then,
<p>

$$
\begin{align*}
    \arg\min_{\Delta x\in V} \left\{ \langle g,\Delta x\rangle + \frac{\lambda}{2} \|\Delta x\|^2 \right\} &= \arg\min_{\Delta x\in V} \left\{ c \langle g,t\rangle + \frac{\lambda}{2} c^2 \right\} \\
    &= \arg \min_{c\ge 0} \left\{ c \min_{t\in V, \|t\|=1} \langle g,t\rangle + \frac{\lambda}{2} c^2 \right\} \\
    &= \arg\min_{c\ge 0} \left\{-c \|g\|_* + \frac{\lambda}{2}c^2\right\} \cdot \mathrm{dualize}_{\|\cdot\|}(g) \\
    &= -\frac{\|g\|_*}{\lambda} \cdot \mathrm{dualize}_{\|\cdot\|}(g).\;\;\;\;\;\blacksquare
\end{align*}
$$
</p>
Thus we have shown.

### Origin of a Normed Space
This type of question naturally arises when optimizing a neural network. Consider an input space \\(x\in X\\) with norm \\(\\|\cdot\\| _\alpha\\) and an output space \\(y\in V\\) with norm \\(\\|\cdot\\| _\beta\\). The two spaces are related by a linear transform \\(y = Mx\\). Then there is a naturally induced norm on the weights \\(M\\) in the weight space defined as
<p>

$$
\|M\|_{\alpha\rightarrow\beta} = \max_{x} \frac{\|Mx\|_\beta}{\|x\|_\alpha}.
$$
</p>

In fact, by adopting the viewpoint of steepest descent on a normed space, one can interpret the Adam optimizer differently from that of the convex optimization theory. That will be a thing for me to learn in the future. These can be found from the paper "[Old Optimizer, New Norm: An Anthology](https://arxiv.org/abs/2409.20325v1)". Definitely worth a read.

---
## Finsler manifold
I included this section after reading the works from [this site](https://docs.modula.systems/algorithms/manifold/). I do not like their formulation and introduction there. Hence, I decide to derive similar results from ground up in my own words.

From last post, I have established that to minimize a function defined on a manifold \\(f:\mathcal{M} \rightarrow \mathbb{R}\\), we apply the following two steps:
<p>

$$
{\begin{aligned}
    h_t &= \arg\min_{h\in T_{x_{t}}\mathcal{M}} \left\{ \frac{\partial f(x_{t})}{\partial x}[h] + \frac{\lambda}{2} \langle h,h \rangle _{x_{t}}\right\}, \\
    x_{t+1} &= R_{x_t}(h_t).
\end{aligned}}
$$
</p>
The function \\(R\\) is a retraction chosen.

### Steepest descent on normed manifolds
The [post](https://leloykun.github.io/ponder/steepest-descent-non-riemannian/) by Franz Louis Cesista explained really well on this topic. My post is heavily influenced by it.

Consider on the tangent bundle \\(T\mathcal{M} = \cup_{x\in\mathcal{M}} T_x\mathcal{M}\\), instead of having an inner product \\(\langle\cdot,\cdot\rangle_x\\) associated to each tangent space \\(T_x\mathcal{M}\\), we have a norm \\(\|\|\cdot\|\|_x\\) on it. If the norm is induced by an inner product, we are doing Riemannian optimization; else, we are doing non-Riemannian optimization.

The descent direction \\(h\\) will then be
<p>

$$
\boxed{
    h = \arg\min_{h\in T_{x_{t}}\mathcal{M}} \left\{ \frac{\partial f(x_{t})}{\partial x}[h] + \frac{\lambda}{2} \|h\|_x^2 \right\}.
}
$$
</p>
Solving this optimization then applying the retraction map allows us to do steepest descent algorithms on normed manifolds.

Another name for a normed manifold is *a manifold with Finsler structure*, or simply, a *Finsler manifold*. This is different from the usual Riemannian manifold that I had dealt with before.

### The descent direction
Furthermore, by adopting the dualization operation (I have discussed this in [a previous post](https://wenperng.github.io/posts/2025/09/blog-post-07/)) which is from the paper "[Modular Duality in Deep Learning](https://arxiv.org/pdf/2410.21265#:~:text=Modular%20dualization%20involves%20first%20assigning%20operator%20norms%20to,the%20weight%20space%20of%20the%20full%20neural%20architecture.)", we have the solution to the descent direction as

<p>

$$
h = -\frac{1}{\lambda} \left\|\frac{\partial f(x_t)}{\partial x}\right\|_* \cdot \mathrm{dualize}_{\|\cdot\|}\left(\frac{\partial f(x_t)}{\partial x}\right).
$$
</p>

If one uses the more *differential-geometry*-inclined notation of the differential map, where \\(\partial f/\partial x = \mathrm{D}f = \mathrm{d}f = f_\*\\) is equivalent to the pushforward map, then we can also write the descent direction simply as
<p>

$$\boxed{
h = -\frac{\|f_*(x_t)\|_*}{\lambda} \cdot \mathrm{dualize}_{\|\cdot\|}(f_*(x_t)).
}$$
</p>
Note that the pushforward map \\(f _\*(x _{t}) : T _{x _t} \mathcal{M} \rightarrow \mathbb{R}\\). Hence, \\(f _\*(x _{t}) \in T _{x _t} ^\* \mathcal{M}\\) is a dual vector.

The steepest descent update can then be written as
<p>

$$
\boxed{\begin{aligned}
    x_{t+1} &= R_{x_t}\left( - \eta \|f_*(x_t)\|_* \cdot \mathrm{dualize}_{\|\cdot\|}(f_*(x_t))\right) \\
    &= R_{x_t}\left( - \frac{1}{\lambda} \|f_*(x_t)\|_* \cdot \mathrm{dualize}_{\|\cdot\|}(f_*(x_t))\right).
\end{aligned}}
$$
</p>
The sharpness parameter and step-size are related by \\(\lambda = 1/\eta\\).

### Why normed?
Here I give another example as to when we will meet an optimization problem over the Finsler manifold as opposed to treating the formulation above merely as a play of symbols.

Suppose our loss function \\(f\\) can be locally bounded by the quadratic function
<p>

$$
f(R_x(h)) \le f(x) + \frac{\partial f(x)}{\partial x}[h] + \frac{\lambda}{2} \|h\|^2.
$$
</p>
Then a simple way to upper bound \\(f\\) is to find the minima of the right hand side, which results in the minimization problem
<p>

$$
\begin{aligned}
    h &= \arg\min_{h\in T_x\mathcal{M}} \left\{f(x) + \frac{\partial f(x)}{\partial x}[h] + \frac{\lambda}{2} \|h\|^2\right\} \\
    &= \arg\min_{h\in T_x\mathcal{M}} \left\{\frac{\partial f(x)}{\partial x}[h] + \frac{\lambda}{2} \|h\|^2\right\}.
\end{aligned}
$$
</p>
The minimization scheme proposed at the start of the post naturally appears.

### Notes on notation
Note that if \\(\mathcal{M}\\) is a matrix manifold, then we can rewrite

<p>

$$
\frac{\partial f(x)}{\partial x}[h] = \mathrm{Tr}\{g^{\mathsf{T}}h\} = \langle g,h\rangle _F,
$$
</p>
where \\(g\\) is some *gradient-like* matrix, and \\(\langle\cdot,\cdot\rangle_F\\) is the Frobenius inner product.

Such form must exist as the pushforward is a linear map \\(T_x\mathcal{M}\rightarrow \mathbb{R}\\), and any linear map mapping matrices to scalars can always be written as a Frobenius inner product.