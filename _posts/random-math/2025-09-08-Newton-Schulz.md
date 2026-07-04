---
layout: post
title: Newton-Schulz Iteration
date: 2025-09-09
description: "This post talks about the Newton-Schulz iteration method, which induces a fast iteration method for inverting or orthogonalizing a matrix using only matrix multiplication."
tags: math
categories: random-math
toc:
    sidebar: left
---

> This post talks about the Newton-Schulz iteration method which uses only matrix multiplications (no inverses or other decomposition method) to perform a polynomial transform on the singular values of a matrix. This induces a fast iteration method for inverting or orthogonalizing a matrix with only matrix multiplication.

## Polynomial transform on singular values
Consider a matrix $$X$$ with the singular value transform $$U\Sigma V^\mathsf{H}$$. Observe the polynomial relation below:

$$
X (X^\mathsf{H}X)^n = U\Sigma V^\mathsf{H} \left(V \Sigma^\mathsf{T}\Sigma V^\mathsf{H}\right)^n = U f_{x^{2n+1}}(\Sigma) V^{\mathsf{H}},
$$

where $$f_{x^{2n+1}}(\Sigma)$$ performs the function $$x^{2n+1}$$ on the singular values on the diagonal of $$\Sigma$$.

Using this idea, we can perform polynomials of odd orders $$f(x) = a_0 x + a_1 x^3 + a_2 x^5 + \cdots$$ on any matrix by the polynomial transform

$$
f(X) = U f(\Sigma) V^\mathsf{H} = \sum_{n=0}^{\infty} a_n X (X^\mathsf{H} X)^n.
$$

## Orthogonalizing a matrix
Let us define what I mean by orthogonalizing a matrix: I want to find the solution to

$$
\arg\min_{M} \|M-X\|_F \text{ s.t. } MM^\mathsf{H} = \mathbb{I} \text{ or } M^\mathsf{H}M = \mathbb{I}.
$$

This is known as the ***orthogonal Procrustes problem***, often seen in tasks such as alignment. The solution to this optimization problem is simple, one can see that the optimal $$M$$ is

$$
M = UV^\mathsf{H} \text{ where } X = U\Sigma V^\mathsf{H}.
$$

I.e., the orthogonalization is equal to applying the function $$f(x) = 1$$ on the matrix.

> ##### TIP
> The optimality is established by noting that
>
> $$
> \begin{align*}
>   \|M - X\|_F^2 &= \mathrm{Tr}\left\{(M-X)^\mathsf{H} (M-X)\right\} \\
>   &= \|M\|_F^2 + \|X\|_F^2 - 2\mathrm{Tr}\left\{M^\mathsf{H}X\right\}. 
> \end{align*}
> $$
>
> Therefore, the minimization of the Frobenius norm is equivalent to the maximization of the inner product
> 
> $$
> \begin{align*}
>   \arg\max_{M} \mathrm{Tr}\left\{M^\mathsf{H}X\right\} &= \arg\max_{M} \mathrm{Tr}\left\{ M^\mathsf{H} (U\Sigma V^\mathsf{H}) \right\} \\
> &= \arg\max_{M} \mathrm{Tr}\left\{ (U^\mathsf{H}MV)^\mathsf{H} \Sigma \right\}
> \end{align*}
> $$
>
> The matrix $$R = U^\mathsf{H}MV$$ is also orthogonal. Hence, the inner product is obviously maximized when $$R$$ is the identity matrix.
{: .block-tip}

However, with finite terms of the series applied, we can never create the function $$f(x) = 1$$. Nevertheless, we can approximate it. We consider a function $$g$$ that is a polynomial with finite terms, and perform the composition $$g\circ g\circ \cdots\circ g = g^{\circ n}$$ and have $$g^{\circ n }\xrightarrow{n\rightarrow\infty} f$$ for a small range of inputs. This is the ***Newton-Schulz method***.

### Example
For example, let us consider a third order transform

$$
M_{t+1} = 2 M_{t} - 1.5 M_t(M_t^\mathsf{T}M_t) + 0.5 M_t(M_t^\mathsf{T}M_t)^2
$$

with $$M_0 = X$$. This is equivalent to applying the polynomial $$g(x) = 2x - 1.5x^3 + 0.5x^5$$ on the singular values. By iterating $$g$$ (see the figure below), we see that it maps all singular values in $$(0,\sqrt{2})$$.

<br/><img src='/assets/img/posts/2025-09-08-orthogonalization.png' width="70%">

> ##### NOTE
> My acquaintance with the Newton-Schulz method stemmed from my exploration of the neural network optimizer termed [Muon](https://kellerjordan.github.io/posts/muon/).
>
> In the link above, they discussed some ad-hoc methods for tuning the parameters to the polynomial $$g$$.
{: .block-warning}


## Inverting a matrix
To invert a matrix $$X$$, we perform the function $$f(x) = 1/x$$ on the singular values. Furthermore, the left and right singular-vector matrices have to be Hermitian conjugated as well. The polynomial transform will hence be modified to be

$$
f(X) = V f(\Sigma) U^\mathsf{H} = \sum_{n=0}^{\infty} a_n X^\mathsf{H}(XX^\mathsf{H})^n.
$$

How do we realize the function $$f$$ with finite terms? We can again consider an function $$g$$ that gives us a good enough approximation to $$f$$ as $$g^{\circ n} \xrightarrow{n\rightarrow\infty} f$$.

Note that, however,

$$
f(x) = \frac{1}{1-(1-x)} = 1 + (1-x) + (1-x)^2 + \cdots = \sum_{n=0}^{\infty} (1-x)^n,
$$

which is not an odd polynomial. A naive tuning of parameters may lead us nowhere. What can we do then?

### Newton-Schulz method
Here is an approach to incorporate both even and odd terms. 

By replacing the $$X^\mathsf{H}$$ above with a matrix $$Y_n$$ that approximates $$X^{-1}$$ in the limit, the function becomes a polynomial in $$Y_n$$ with both even and odd powers:

$$
g(Y_n) = \sum_{m=0}^{k} a_m Y_n (XY_n)^m = Y_n \sum_{m=0}^{k} a_m (XY_n)^m.
$$

Let $$Y_0$$ be a well-selected initial condition (this will be specified in the convergence analysis), with $$Y_{n+1} = g_k(Y_n)$$ defined as

$$
\boxed{
    Y_{n+1} = Y_{n} \sum_{m=0}^{k} (I - XY_{n})^m =: g_k(Y_n)
}.
$$

Note that as $$k\rightarrow\infty$$, we obtain that $$Y_{n+1} = Y_{n}(I - I + XY_{n})^{-1} = X^{-1}$$.

The iteration we obtained is the $$k$$th order Newton-Schulz iteration for finding matrix inverses!

For example, if we let $$k=1$$, then we have

$$
Y_{n+1} = Y_{n} \left(2I - XY_{n}\right).
$$

This is the most common version of Newton-Schulz iteration. If we let $$k=2$$, then we have

$$
Y_{n+1} = Y_{n} \left(3I - 3XY_{n} + (XY_{n})^2\right).
$$

The stability to the Newton-Schulz iteration for finding matrix inverses needs further examination.

### Convergence analysis
A fix point of the above iteration is $$Y_n = X^{-1}$$. Our task is to find the convergence rate of $$Y_n$$ to $$X^{-1}$$ and the range of suitable initial conditions.




Notice that as $$k\rightarrow\infty$$, a necessary and sufficient condition for the summation in the function $$g$$ to converge is to have $$\|I - XY_n\| < 1$$ for any matrix norm $$\|\cdot\|$$ satisfying $$\|I\| = 1$$. Henceforth, for the $$k$$th order Newton-Schulz algorithm to converge, a sufficient condition will also be to require

$$
\|I - XY_n\| < 1.
$$

Then, we see that

$$
\begin{align*}
    \|I - XY_{n+1} \| &= \left\| I - XY_{n} \sum_{m=0}^{k} (I - XY_{n})^m\right\| \\
    &= \left\| (I - XY_{n}) - XY_{n} \sum_{m=1}^{k} (I - XY_{n})^m\right\| \\
    &= \left\| (I - XY_{n}) \left(I - XY_{n} \sum_{m'=0}^{k-1} (I - XY_{n})^{m'}\right)\right\| \\
    &= \cdots \\
    &= \left\| (I - XY_{n})^{k+1} \right\| \\
    &\le \| I - XY_{n} \|^{k+1},
\end{align*}
$$

where the last step is by the sub-multiplicativity of matrix norms.

Finally, one can hence see that the convergence is geometric! With the $$k$$th order Newton-Schulz iteration following

$$
\boxed{
    \|I - XY_{n+1} \| \le \|I - XY_{n}\|^{k+1}
}.
$$

It's a really fast convergence. As long as the initial condition satisfies

$$
\boxed{
    \|I - XY_0\| < 1
},
$$

we have $$Y_n \rightarrow X^{-1}$$.