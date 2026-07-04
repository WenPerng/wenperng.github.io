---
layout: post
title: "Robbins-Monro Step-Size Condition"
date: 2025-09-17
description: "This post discusses a result on the Robbins-Monro step-size condition which guarantees convergence under a noisy gradient descent."
tags: math
categories: optimization
toc:
    sidebar: left
---

> This post discusses a result on the Robbins-Monro step-size condition which guarantees convergence under a noisy gradient descent.

In dealing with iterations of the form
<p>

$$
x_{t+1} = x_{t} - \mu \boldsymbol{g}_t,
$$
</p>
the iteration might not converge given a fixed step-size \\(\mu\\) and a gradient with noise denoted by \\(\boldsymbol{g} _t\\).

The Robbins-Monro condition on an iteration-dependent scheme ensures the convergence of the iteration above. Let the step-size on iteration \\(t\\) be \\(\mu_t\\), then the condition reads
<p>

$$
\boxed{
\begin{aligned}
    \sum_{t=1}^{\infty} \mu_t =\infty, \\
    \sum_{t=1}^{\infty} \mu_t^2 < \infty.
\end{aligned}
}
$$
</p>

## Result
For this post specifically, it is to proof Lemma F.5 in the book "[Adaptation, Learning, and Optimization over Networks](https://asl.epfl.ch/asl-book/adaptation-learning-and-optimization-over-networks/)" by Ali H. Sayed. This lemma can be used to show the convergence of the noisy gradient descent recursion above under Robbins-Monro condition by a few change of variables. The lemma is stated as:

---

Let \\(x_t \ge 0\\) denote a scalar deterministic sequence that satisfies the inequality recursion:
<p>

$$
x_{t+1} \le \left(1 - a_t\right) x_t + b_t\;\;\;\;\;(t\ge 0).
$$
</p>

When the scalar sequences \\(\\\{a _t, b _t\\\}\\) satisfy the four conditions:
<p>

$$
\begin{aligned}
    &0 \le a_t < 1, &&b_t \ge 0, \\
    &\sum_{t=1}^{\infty} a_t = \infty, &&\lim_{t\rightarrow\infty} \frac{b_t}{a_t} = 0,
\end{aligned}
$$
</p>
it holds that \\(\lim _{t\rightarrow\infty} x _t = 0\\).

When the scalar sequences \\(\\\{a _t, b _t\\\}\\) are of the form
<p>

$$
\begin{aligned}
    &a_t = \frac{c}{t}, &&b_t = \frac{d}{t^{p+1}}
\end{aligned}
$$
</p>
for \\(c, d, p > 0\\), it holds that for large \\(t\\), the sequence \\(x _t\\) converges to \\(0\\) at one of the following rates:
<p>

$$
\begin{cases}
    x_t \le \left(\frac{d}{c-p}\right) \frac{1}{t^p} + o\left(\frac{1}{t^p}\right), & c>p; \\
    x_t = O\left(\frac{\log t}{t^p}\right), & c=p; \\
    x_t = O\left(\frac{1}{t^c}\right), & c<p.
\end{cases}
$$
</p>

---

This result is an excerpt from "Introduction to Optimization" by B. Poljak. This post is to adapt the proof of the first part there to a more clear version. The second part is already pretty clearly written, so I'll not include it.

## Proof
Expand the recursion out:
<p>

$$
\begin{aligned}
    x_{t+1} &\le (1 - a_t) (1 - a_{t-1}) x_{t-1} + b_t + (1 - a_t) b_{t-1} \\
    &\le \prod_{k=1}^{t} (1 - a_k) x_1 + \sum_{k=1}^{t} b_k \prod_{\ell=k+1}^{t} (1 - a_\ell).
\end{aligned}
$$
</p>
Note the abuse of notation where
<p>

$$
\prod_{\ell=t+1}^{t} (1-a_\ell) = 1.
$$
</p>

Next, let us bound the two terms. For the first term:
<p>

$$
\begin{align*}
    0 \le \prod_{k=1}^{t} (1 - a_k) &= \exp\left(\sum_{k=1}^{t} \log (1 - a_k)\right) \\
    &\le \exp\left( - \sum_{k=1}^{t} a_k\right) \\
    &\xrightarrow{t\rightarrow\infty} \exp(-\infty) = 0.
\end{align*}
$$
</p>

The second term is: let \\(\beta _k = b _k / a _k\\), with \\(\beta _k\rightarrow 0\\). Then,
<p>

$$
\begin{align*}
    \sum_{k=1}^{t} b_k \prod_{\ell=k+1}^{t} (1 - a_\ell) &= \sum_{k=1}^{t} \beta_k a_k \prod_{\ell = k+1}^{t} (1-a_\ell) \\
    &= \sum_{k=1}^{t} \beta_k (1-(1-a_k)) \prod_{\ell = k+1}^{t} (1-a_\ell) \\
    &= \sum_{k=1}^{t} \beta_k \left(\prod_{\ell=k+1}^{t} (1-a_\ell) - \prod_{\ell =k}^{t} (1-a_\ell)\right).
\end{align*}
$$
</p>
For all \\(\varepsilon > 0\\) there exists some \\(N>0\\) such that \\(\beta_k < \varepsilon\\) for all \\(k > N\\). Then,
<p>

$$
\begin{align*}
    0 &\le \sum_{k=1}^{t} b_k \prod_{\ell=k+1}^{t} (1 - a_\ell) \\
    &= \sum_{k=1}^{N} b_k \prod_{\ell=k+1}^{t} (1 - a_\ell) + \sum_{k=N+1}^{t} b_k \prod_{\ell=k+1}^{t} (1 - a_\ell) \\
    &= \sum_{k=1}^{N} b_k \prod_{\ell=k+1}^{t} (1 - a_\ell) + \sum_{k=N+1}^{t} \beta_k \left(\prod_{\ell=k+1}^{t} (1 - a_\ell) - \prod_{\ell=k}^{t} (1 - a_\ell)\right) \\
    &\le \max_{1\le k\le N}b_k \cdot \prod_{\ell = N+1}^{t} (1-a_\ell) + \max_{N < k\le t} \beta_k \sum_{k=N+1}^{t} \left(\prod_{\ell=k+1}^{t} (1 - a_\ell) - \prod_{\ell=k}^{t} (1 - a_\ell)\right) \\
    &= \max_{1\le k\le N}b_k \cdot \prod_{\ell = N+1}^{t} (1-a_\ell) + \max_{N < k\le t} \beta_k \cdot \left(1 - \prod_{\ell=N+1}^{t} (1 - a_\ell)\right) \\
    &\xrightarrow{t\rightarrow\infty} 0 + \varepsilon.
\end{align*}
$$
</p>
Hence, we have successfully bounded the series.
