---
layout: post
title: Exponential Family
date: 2025-08-25
description: "This note gives a brief introduction to the exponential family and some of its properties."
tags: math geometry
categories: information-geometry
toc:
    sidebar: left
---

> This is my note learning from the book \"[Information Geometry and Its Applications](https://link.springer.com/book/10.1007/978-4-431-55978-8)\" by Amari. This note specifically gives a brief introduction to the exponential family and some of its properties.

Information geometry is the technique / study of viewing a *family* of probability distributions as a manifold, then tackling problems in information theory using the techniques from differential geometry.

This post will go over some of the basics of a very important family of distributions -- the *exponential family*. What's more, I also introduce the primal and dual coordinates to the distributions in the exponential family, this in turn links to the result stated back in a [past blog](/posts/2025/08/blog-post-3/). The things written here are mostly what I have learned from the book "[Information Geometry and Its Applications](https://link.springer.com/book/10.1007/978-4-431-55978-8)" by Shun'ichi Amari. This post also took reference of the [work by Frank Nielson](https://arxiv.org/abs/1808.08271).

## Definition
In tackling many problems, one often *assumes* a probability model defined by a set of parameters that the problem follows. Whether or not this assumption is valid is a problem for another time. However, one often choose a nice model that makes the mathematics clean and beautiful. The exponential family is one such model.

The (natural) exponential family, in its cleanest form, is defined as the set of distributions \\(\mathcal{M} = \{p(\cdot\vert\theta)\}\\), with each element being a probability density function of the form
<p>
$$
p(x\vert\theta) \,\mathrm{d}x = \exp\left\{\theta^{\mathsf{T}} x + k(x) - \psi(\theta)\right\} \mathrm{d}x.
$$
</p>
One can then see that the family is parameterized by the vector \\(\theta\\), it can also be seen as the coordinates on the manifold \\(\mathcal{M}\\).

Since the vector \\(x\\) might be restricted on a manifold as well, i.e., its coordinates are not mutually independent, we can rewrite the exponential family as
<p>
$$
\boxed{
	p(x\vert\theta) \,\mathrm{d}\mu(x)= \exp\left(\theta^{\mathsf{T}} x - \psi(\theta)\right) \mathrm{e}^{k(x)}\mathrm{d}x = \exp\left(\theta^{\mathsf{T}} x - \psi(\theta)\right) \mathrm{d}\mu(x)
},
$$
</p>
where \\(\mu(x)\\) is a measure on \\(x\\). This will be the form of the exponential family that we will continue to use throughout our discussion.

### The term \\(\psi\\)
The term \\(\psi\\) is of our utmost interest as many interesting properties and results are associated with it.

We often denote \\(Z(\theta) = \exp(\psi(\theta))\\) as the normalization constant, often also called the partition function.

Next, \\(\psi\\) can be represented as
<p>
$$\boxed{
\psi(\theta) = \log \int \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \,\mathrm{d}x = \log \int Z(\theta) \, p(x\vert\theta)\,\mathrm{d}\mu(x)
},
$$
</p>
where we used the natural logarithm, and the integral is taken over the domain of \\(x\\). We state a few properties of \\(\psi\\):

#### Its derivatives satisfy:
<p>
$$\boxed{
\begin{aligned}
	\nabla \psi(\theta) &= \mathbb{E}[x] \\
	\nabla^2 \psi(\theta) &= \mathbb{E}[xx^{\mathsf{T}}] - \mathbb{E}[x] \mathbb{E}[x]^{\mathsf{T}}
\end{aligned}
}.
$$
</p>

The proof is as follows:
<p>
$$
\begin{aligned}
	\nabla_i \psi(\theta) &= \frac{\partial}{\partial \theta^i} \log \int \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \,\mathrm{d}x \\
	&= \frac{\int x_i \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \, \mathrm{d}x}{\int \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \,\mathrm{d}x} \\
	&= \frac{\int x_i \cdot p(x\vert\theta)\,\mathrm{d}\mu(x)}{\int p(x\vert\theta)\,\mathrm{d}\mu(x)} = \mathbb{E}[x_i]. \;\;\;\;\;\blacksquare
\end{aligned}
$$
</p>
Do not mind my indexing of the components of \\(\theta\\) by superscripts \\(\theta^i\\), it is a good habit originating from differential geometry. Next, the second derivative
<p>
$$
\begin{aligned}
	\nabla^2_{ij} \psi(\theta) &= \frac{\partial}{\partial \theta^i} \frac{\int x_j \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \, \mathrm{d}x}{\int \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \,\mathrm{d}x} \\
	&= \frac{\int x_ix_j \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \, \mathrm{d}x}{\int \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \,\mathrm{d}x} \\
	&\hspace{1cm} - \frac{\int x_i \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \, \mathrm{d}x \cdot \int x_j \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \, \mathrm{d}x}{\left(\int \exp\left\{\theta^{\mathsf{T}} x + k(x)\right\} \,\mathrm{d}x\right)^2} \\
	&= \mathbb{E}[x_jx_j] - \mathbb{E}[x_i] \mathbb{E}[x_j]. \;\;\;\;\;\blacksquare
\end{aligned}
$$
</p>
Thus it is proven.

#### It is a convex function:
Since its Hessian is the covariance matrix of \\(x\\), which is positive semi-definite, the function \\(\psi\\) is convex.

### Examples of exponential family
#### Gaussian distribution
This is the most obvious of them all, consider the probability density function of a Gaussian distribution:
<p>
$$
\begin{aligned}
	p(t\vert\theta) &= \frac{1}{\sqrt{2\pi \sigma^2}} \exp\left(-\frac{(t-\mu)^2}{2\sigma^2}\right) \\
	&= \frac{1}{\sqrt{2\pi \sigma^2}} \exp\left(-\frac{1}{2\sigma^2}t^2 + \frac{\mu}{\sigma^2}t - \frac{\mu^2}{2\sigma^2}\right).
\end{aligned}
$$
</p>
If we define
<p>
$$
x = \left[\begin{matrix}
	x_1 \\ x_2
\end{matrix}\right] = \left[\begin{matrix}
	t \\ t^2
\end{matrix}\right],\; \theta = \left[\begin{matrix}
	\theta^1 \\ \theta^2
\end{matrix}\right] = \left[\begin{matrix}
	\frac{\mu}{\sigma^2} \\ -\frac{1}{2\sigma^2}
\end{matrix}\right],\; \mathrm{d}\mu(x) = \delta(x_2-x_1^2) \,\mathrm{d}t,
$$
</p>
where \\(\delta\\) is the delta function, then the Gaussian distribution can be seen to be in the exponential family, with
<p>
$$\begin{aligned}
	\psi(\theta) &= \frac{\mu^2}{2\sigma^2} + \frac{1}{2} \log(2\pi\sigma^2) \\
	&=- \frac{(\theta^1)^2}{4\theta^2} - \frac{1}{2}\log(-\theta^2) + \frac{1}{2}\log\pi.
\end{aligned}$$
</p>

#### Discrete random variables
A probability *density* function over \\(\\\{0,1,\ldots,n\\\}\\) is of the form
<p>
$$
\begin{align*}
	p(t\vert\theta) &= \sum_{k=0}^{n} p_k \delta(t-k) \\
	&= \exp\left(\sum_{k=0}^{n} \log p_k \delta(t-k)\right) \\
	&= \exp\left(\log p_0 + \sum_{k=1}^{n} \log\frac{p_k}{p_0} \delta(t-k)\right)
\end{align*}.
$$
</p>
Denote \\(x_k = \delta(t-k)\\), \\(\theta^k = \log(p_k/p_0)\\) for \\(k=1,\ldots,n\\), and \\(\mathrm{d}\mu(x) = \mathrm{d}t\\), we can see that any discrete distributions are in the exponential family. Furthermore,
<p>
$$
\psi(\theta) = -\log p_0 = \log \left(\frac{p_0 + p_1 + \cdots + p_n}{p_0}\right) = \log \left(1 + \sum_{k=1}^{n} \exp(\theta^k)\right).
$$
</p>

## Primal and dual coordinates of exponential family
For a distribution in the exponential family, we can describe it using the coordinates \\(\theta\\). We call this the *primal coordinate* of the distribution.

If there is a primal, there should also be a dual. Without any motivation, we scoute the whole post for the only convex function that we can find, \\(\psi\\), to construct a map
<p>
$$
\boxed{\eta = \nabla\psi(\theta) = \mathbb{E}[x]}
$$
</p>
that maps the primal coordinate \\(\theta\\) of a distribution \\(P\\) into the *dual coordinate* \\(\eta\\) of the same distribution. For a distribution \\(P\\), we hence denote its primal coordinate as \\(\theta(P)\\), and its dual coodinate as \\(\eta(P)\\).

Furthermore, from the definition of the convex conjugate (see my [previous post](/posts/2025/08/blog-post-2/)), we denote
<p>
$$
\begin{aligned}
\varphi(\eta) = \psi^*(\eta) &= \theta^{\mathsf{T}} \eta - \psi(\theta).
\end{aligned}
$$
</p>

From our discussion on Bregman divergences, we note that: given two distributions \\(P\\) and \\(Q\\) in the exponential family having the same parametric form,
<p>
$$
\begin{aligned}
	B_\psi(\theta(P),\theta(Q)) &= B_{\varphi}(\eta(Q),\eta(P)) \\
	&= \psi(\theta(P)) - \psi(\theta(Q)) - \langle \eta(Q),\theta(P) - \theta(Q)\rangle \\
	&= \log \frac{\int Z(\theta(P)) \, p(x\vert \theta(P)) \,\mathrm{d}\mu(x)}{\int Z(\theta(Q)) \, p(x\vert \theta(Q)) \,\mathrm{d}\mu(x)} - \langle \mathbb{E}_{Q}[x] ,\theta(P) - \theta(Q) \rangle \\
	&= \log \frac{Z(\theta(P))}{Z(\theta(Q))} - \mathbb{E}_Q\left[x^{\mathsf{T}} \theta(P) - x^{\mathsf{T}} \theta(Q)\right] \\
	&= \mathbb{E}_Q\left[\log p(x\vert\theta(Q)) - \log p(x\vert\theta(P))\right] \\
	&= \mathbb{E}_Q \left[\log\frac{Q}{P}\right] = D_{\mathrm{KL}}(Q\|P).
\end{aligned}
$$
</p>

Amazingly, the Bregman divergence derived from the convex function \\(\psi\\) associated to the exponential family is the [KL divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence) (but with the order of \\(P\\) and \\(Q\\) *inverted*)!
<p>
$$
\boxed{
	B_\psi(\theta(P),\theta(Q)) = B_\varphi(\eta(Q),\eta(P)) = D_{\mathrm{KL}}(Q\|P).
}
$$
</p>

### Examples of dual coordinates
#### Gaussian distribution
We have
<p>
$$\eta = \left[\begin{matrix}
	\eta_1 \\ \eta_2
\end{matrix}\right] = \nabla \psi(\theta) = \left[\begin{matrix}
	- \frac{\theta^1}{2\theta^2} \\
	\frac{(\theta^1)^2}{4(\theta^2)^2} + \frac{1}{2\theta^2}
\end{matrix}\right] = \left[\begin{matrix}
	\mu \\ \mu^2 + \sigma^2
\end{matrix}\right] = \left[\begin{matrix}
	\mathbb{E}[x_1] \\ \mathbb{E}[x_2]
\end{matrix}\right].$$
</p>
Note that since \\(\eta\\) is the dual coordinate, its components are indexed by a *subscript*.

The dual convex function is:
<p>
$$
\begin{align*}
	\varphi(\eta) &= \eta^{\mathsf{T}} \theta - \psi(\theta) \\
	&= -\frac{1}{2}\left(1 + \log(2\pi) + \log(\sigma^2)\right) \\
	&= -\frac{1}{2} \left(1 + \log(2\pi) + \log(\eta_2 - \eta_1^2)\right).
\end{align*}
$$
</p>

#### Discrete random variables
For \\(k=1,2,\ldots,n\\),
<p>
$$
	\eta_k = \frac{\partial}{\partial \theta^k} \psi(\theta) = p_0\mathrm{e}^{\theta^k} = p_k = \mathbb{E}[x_k].
$$
The dual convex function is then
<p>
$$
\begin{aligned}
	\varphi(\eta) &= \eta^{\mathsf{T}} \theta - \psi(\theta) \\
	&= \sum_{k=1}^{n} p_k \log \frac{p_k}{p_0} + \log p_0 \\
	&= \sum_{k=0}^{n} p_k \log p_k \\
	&= \sum_{k=1}^{n} \eta_k \log \eta_k + \left(1-\sum_{k=1}^{n}\eta_k\right) \log \left(1-\sum_{k=1}^{n}\eta_k\right),
\end{aligned}
$$
</p>
which is the negative entropy.
 