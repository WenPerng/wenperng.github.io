---
layout: post
title: "On Mirror Descent"
date: 2025-08-23
description: "This is a simple blog post on what mirror descent is."
tags: math
categories: optimization
toc:
    sidebar: left
---

> This is a simple blog post on what mirror descent is. I learned this from a friend of mine, Zoya, who I met during my stay at ASL, EPFL in the summer of 2025.

## Descent methods revisited
A usual descent method is described by a recursion of the form
<p>
$$x_{t} = x_{t-1} - \eta g_{t},$$
</p>
where \\(\eta\\) is the step-size, and \\(g_{t}\\) is the descent direction. If the descent direction \\(g_{t}\\) is the gradient at \\(x_{t-1}\\), then the recursion is the gradient descent algorithm; if the direction is a subgradient, then the recursion is a subgradient descent; if the direction is the gradient multiplied by the inverse Hessian, then the recursion is the Newton's method.

Now, we can rewrite the recursion as an optimization problem of the form
<p>
$$\boxed{
    x_{t} = \arg\min_{x\in\mathbb{R}^n} \left\{ \langle g_{t},x\rangle + \frac{1}{2\eta} \left\| x - x_{t-1} \right\|_2^2 \right\}
}.$$
</p>
This can be readily checked via a simple differentiation. The minimization problem above can be seen as weighting between "being in the gradient direction" (the inner product term in the front) and "staying close to the previous point" (the norm term at the back).

What happens if we change the quadratic norm term at the back, also known as the *proximity term* with other forms of squared distances? This is the premise of mirror descent.

## What is mirror descent?
Let us consider a class of squared distances that can replace the  Euclidean squared distance we have above. These are called the Breman divergences.

### Bregman Divergence
Consider a strictly convex function \\(f:X\rightarrow\mathbb{R}\\), then the Bregman divergence associated with \\(f\\) for points \\(x\\) and \\(x' \in X\\) is defined to be
<p>
$$\boxed{ B_f(x, x') = f(x) - f(x') - \langle \nabla f(x') , x-x'\rangle} .$$
</p>

The Bregman divergence acts like a squared distance although being asymmetric. The discussions to the motivation of such a definition and what that previous sentence means are deferred to future posts on some basics of information geometry. So for the mean time, just bare with me here.

### Mirror descent
Now, replacing the proximity term in the first recursion with the Bregman divergence, we obtain
<p>
\begin{align*}
    \boxed{x_{t} = \arg\min_{x\in\mathbb{R}^n} \langle g_t,x\rangle + \frac{1}{\eta} B_f(x, x_{t-1})}.
\end{align*}
</p>

The choice of \\(f\\) is important as it changes the dynamic of the algorithm.

## Example of a mirror descent
### Euclidean distance
Consider the convex function as \\(f(x) = \frac{1}{2} || x ||_2^2\\), the scaled Euclidean \\(2\\)-norm. Then the Bregman divergence is
<p>
\begin{align*}
    B_f(x,x')
    &= \frac{1}{2} || x ||_2^2 - \frac{1}{2} \left\| x' \right\|_2^2 - \langle x', x - x' \rangle \\
    &= \frac{1}{2} \langle x + x', x - x'\rangle - \langle x', x - x'\rangle \\
    &= \frac{1}{2} \left\|x - x'\right\|^2.
\end{align*}
</p>
Under this choice of \\(f\\), we have obtained the usual descent method as introduced at the start of this post.

### KL divergence
Consider the convex function as the negative entropy:
<p>
$$
  f(x) = - H(x) = \sum_{k=1}^{n} x_k \log x_k
$$
</p>
defined over the probability simplex \\(X = \Delta([n])\\), i.e., \\(x\\) has non-negative components, \\(x_1 + \cdots + x_n = 1\\), and can be viewed as a distribution over a support of size \\(n\\). Here we choose the base to the logarithm as \\(e\\), but it does not really matter as it only contributes to a scaling in \\(\eta\\).

Next, let us compute the corresponding Bregman divergence:
<p>
$$\begin{aligned}
    B_f(x, x')
    &= \sum_{k=1}^{n} x_k \log x_k - \sum_{k=1}^{n} x'_k \log x'_k - \sum_{k=1}^{n} \left(x_k - x'_k\right) \left(1 + \log x'_k \right) \\
    &= \sum_{k=1}^{n} x_k \log \frac{x_k}{x'_k} \\
    &= D_{\mathrm{KL}}( x \| x' ).
\end{aligned}$$
</p>
This last function \\(D_{\mathrm{KL}}( x \\| x' )\\) is the Kullback-Leibler divergence between the discrete distributions \\(x\\) and \\(x'\\).

Plugging this into the mirror descent recursion, we see that
<p>
$$
    x_{t+1} = \arg\min_{x \in \Delta([n])} \left\{ \langle x,g_{t} \rangle + \frac{1}{\eta} D_{\mathrm{KL}}( x \| x_{t-1} ) \right\}.
$$
</p>
The minimizer is found by applying the method of Lagrange multipliers:
<p>
$$\begin{aligned}
    0 &= \frac{\mathrm{d}}{\mathrm{d} x_k} \langle x_{t}, g_{t} \rangle + \frac{1}{\eta} D_{\mathrm{KL}}( x_{t} \| x_{t-1} ) + \lambda \left(\sum_{k=1}^{n} x_{t,k} -1\right) \\
    &= g_{t,k} + \frac{1}{\eta} \left( 1 + \log x_{t,k} - \log x'_{t-1,k}\right) + \lambda \\
    \Rightarrow x_{t,k} &\propto \mathrm{e}^{-\eta g_{t,k}} x_{t-1,k}
\end{aligned}
$$
</p>
The Lagrange multplier \\(\lambda\\) is chosen such that \\(x\\) is a valid distribution. Henceforth, we arrive at
\\[
    x_{t,k} = \frac{\mathrm{e}^{-\eta g_{t,k}} x_{t-1,k}}{\sum_{\ell=1}^{n} \mathrm{e}^{-\eta g_{t,\ell}} x_{t-1,\ell}}.
\\]
This is, in fact, a *Bayesian update with exponential weighting*!

---
But why do we call it "*mirror*" descent?

## The gradient is NOT a vector
Consider \\(g_t\\) as the gradient of our target loss function (to be minimized) evaluated at the point \\(x_{t-1}\\). In the usual gradient descent over \\(\mathbb{R}^n\\), we write the next iterate point as \\(x_t = x_{t-1} - \eta g_t\\). However, as we have seen in [manifold optimization](/talks/2024-10-01-Manifold-Optimization/), more often then not, \\(x_{t-1}\\) and \\(g_t\\) does not live in the same space where their addition makes sense! But for now, we will only consider mirror descent over a subset \\(\mathfrak{X}\\) of a vector space \\(V\\) to make matters simple.

Recall that for a given function \\(\ell : \mathfrak{X} \rightarrow \mathbb{R}\\) defined on a convex set \\(\mathfrak{X} \subseteq V\\), we define its gradient at a point \\(x\in \mathfrak{X}\\) to be a *linear functional* \\(\langle g , \cdot \rangle\\) that satisfies
\\[
    \frac{\mathrm{d} \ell}{\mathrm{d} x} [h] = \langle g , h \rangle
\\]
for all tangent vectors \\(h \in T_x V\\). The tangent space \\(T_x V\\) of a vector space is identical to itself, hence we have \\(T_x V = V\\). All linear functionals defined on a vector space \\(V\\) constitute its *dual space* \\(V^\*\\) (sometimes[^1] also denoted as \\(V^\vee\\)). In the case of the dual space to a tangent space, we often denote it as \\(T^\*_xV\\), \\( (T_xV)^\* \\), or \\( (T_xV)^\vee \\), and call it the *cotangent space* of \\(V\\). Note that since \\(T_x V = V\\), we have \\(T_x^\* V = V^\*\\).

[^1]: Tu, Loring W., "An introduction to manifolds." (2007).

|            | Vector Space  | Dual Space              |
| :--------- | :-----------: | :---------------------: |
| Notation   | \\(V\\)       | \\(V^\*\\)              |
| Vector     | vectors       | dual vectors, covectors |
| Components | contravariant | covariant               |

The table above shows that the usual *vectors* are those that reside in the vector space, while we call those that reside in the dual space the *covectors*. A gradient is a covector, it lives in a different space as the point \\(x\\), hence it cannot be added onto the point[^Riesz].

[^Riesz]: For a finite dimensional vector space, it is *isomorphic* to its dual space. Hence for any covector, by the Reisz representation theorem, we can always associate with it a vector that, under a given inner product, acts equivalently under the said inner product.

The mirror descent, then, is to apply descent methods in the dual space, also known as the mirror space in this context.

## Mirror map
consider a differentiable strictly convex closed function \\(F : \mathfrak{X} \rightarrow \mathbb{R}\\) defined over the same domain as the loss function \\(\ell\\), we will use it to create a *mirror map* that maps a point in the primal space, a subset of the original vector space \\(V\\), to the mirror space, a subset of the dual space \\(V^\*\\).

For a function to be strictly convex, it means that for any \\(x, x'\in \mathfrak{X}\\) and \\(\lambda\in[0,1]\\), we have \\(F(\lambda x + (1-\lambda)x') < \lambda F(x) + (1-\lambda) F(x')\\). For a function to be [closed](https://en.wikipedia.org/wiki/Closed_convex_function), its sublevel set is closed.

### Convex conjugate
The *convex conjugate* (also known as the *Fenchel conjugate* or the *Fenchel dual*) of a convex function \\(F\\) is denoted as \\(F^\*\\) and defined as
<p>
$$\boxed{
    F^*(y) = \sup_{x\in V} \left\{\langle y,x\rangle - F(x)\right\}
}.$$
</p>
This map basically finds the "largest gap" between the linear approximation of \\(F\\)  at \\(x\\). The inspiration behind such a definition is a lengthy one, and one should refer other works to understand them.

As \\(F\\) is strictly convex and closed, the convex conjugation acts as an [involution](https://en.wikipedia.org/wiki/Involution_(mathematics)) on it, i.e., \\((F^\*)^\* = F\\).

### Mirror map
Furthermore, as \\(F\\) is differentiable, we can actually compute the optima above as satisfying the relationship
<p>
$$\boxed{
    y = \nabla F(x)
}.$$
</p>
Interestingly enough, we also have its inverse function as
<p>
$$\boxed{
    x = \nabla F^*(y)
}.$$
</p>

Now we can see that \\(\nabla F\\) is a map from the primal space to the mirror space, THIS is the mirror map. We can now use this notion to continue on with our explaining of the mirror descent algorithm.

<br/><img src='/assets/img/blog/2025-08-22-mirror-map.png' width="60%">

## Mirror descent
Recall the definition to the mirror descent:
<p>
$$\begin{aligned}
    x_{t}
    &= \arg\min_{x\in \mathfrak{X}} \langle g_t, x\rangle + \frac{1}{\eta} B_f(x, x_{t-1}) \\
    \Rightarrow 0 &= \eta g_{t} + \left.\nabla_{x} \left[ F(x) - F(x_{t-1}) - \left\langle \nabla F(x_{t-1}), x - x_{t-1}\right\rangle \right] \right|_{x=x_{t}} \\
	&= \eta g_{t} + \nabla F(x_{t}) - \nabla F(x_{t-1}) \\
	\Rightarrow \nabla F(x_{t}) &= \nabla F(x_{t-1}) - \eta g_{t} \\
	\Rightarrow x_{t} &= \nabla F^* \left(\nabla F(x_{t-1}) - \eta g_{t}\right).
\end{aligned}$$
</p>
We can see that in the mirror space, \\(\nabla F(x_{t-1})\\) performs a usual descent method to obtain \\(\nabla F(x_{t})\\). We finally obtain \\(x_{t}\\) by applying the inverse of the mirror map, viz., \\(\nabla F^\* = (\nabla F)^{-1}\\).

Hence the name "mirror descent". Voilà.