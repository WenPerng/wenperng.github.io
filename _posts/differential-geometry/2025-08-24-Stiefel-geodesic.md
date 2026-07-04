---
layout: post
title: "Paper review: Geodesics of Stiefel Manifold"
date: 2025-08-24
description: "This post is a review on the paper \"The Geoemtry of Algorithms with Orthogonality Constraints\" by Edelman et al."
tags: math geometry
categories: differential-geometry
toc:
    sidebar: left
---

> This post is a review on the paper "[The Geoemtry of Algorithms with Orthogonality Constraints](https://arxiv.org/abs/physics/9806030)" by Edelman et al. This is a lengthy paper. The goal of this review is not to go through the entire paper, but to focus on deriving the explicit form of geodesics on the Stiefel manifold with respect to a given inner product.

I have always wanted to know how the geodesics equation to the Stiefel manifold is obtained since I took the course "Manifold Optimization for Representation Learning" from professor [Hao Shen](https://www.researchgate.net/profile/Hao-Shen-15) from the Technische Universität München, 2024.

Thanks to a friend of mine (郭庭愷) who introduced me to this paper, I am finally able to understand the details.

## Basics on the Geometry of the Stiefel Manifold
Most of this section is established in my talk on [manifold optimization, 2024](/talks/2024-10-01-talk). If you are not sure of the details, be sure to check the slides.

<br><img src='/assets/img/blog/2025-08-24-stiefel-geodesic.png' width="60%">

### Definition
The Stiefel manifold is a generalization to the orthogonal matrices, defined as
<p>
$$
\boxed{\begin{equation*}
	\mathrm{St}(m,k) = \left\{ X \in \mathbb{R}^{m \times k} \middle\vert X^{\mathsf{T}} X = \mathbb{I}_k\right\}
\end{equation*}},
$$
</p>
where \\(m\ge k\\) and \\(\mathbb{I}_k\\) is the \\(k \times k\\) identity matrix. Its dimension is
<p>
$$
	\dim\left( \mathrm{St}(m,k) \right) = mk - \frac{k(k+1)}{2}.
$$
</p>
This is easily obtained from the regular value level set theorem[^Tu].

[^Tu]: See: Tu, Loring W., "An introduction to manifolds." (2007).

### Tangent space
The tangent space to the Stiefel manifold at \\(X \in \mathrm{St}(m,k)\\) is
<p>
$$
\boxed{\begin{equation}\begin{aligned}
	T_{X} \mathrm{St}(m,k) &= \left\{ H \in \mathbb{R}^{m \times k} \middle\vert H^{\mathsf{T}} X + X^{\mathsf{T}} H = 0 \right\} \\
	&= \left\{ X \Omega + X_{\perp} Z \middle\vert \Omega \in \mathrm{Skew}(k), Z \in \mathbb{R}^{(m-k) \times k} \right\}
\end{aligned}\end{equation}},
$$
</p>
where \\(X_{\perp} \in \mathbb{R}^{m \times (m-k)}\\) is the orthogonal complement to \\(X\\) such that their column vectors form a basis of \\(\mathbb{R}^{m}\\) and \\(X^{\mathsf{T}} X_{\perp} = 0\\).

The orthogonal projection from \\(\mathbb{R}^{m \times k}\\) onto \\(T_{X} \mathrm{St}(m,k)\\) with respect to the Frobenius inner product \\(\langle X,Y\rangle = \mathrm{Tr}\\\{X^{\mathsf{T}} Y\\\}\\) is
<p>
$$
\boxed{\begin{equation}\begin{aligned}
	\Pi_X(H)
	&= H - X \cdot \mathrm{sym}\left(X^{\mathsf{T}} H\right) \\
	&= X \cdot \mathrm{skew}\left(X^{\mathsf{T}} H\right) + \left(\mathbb{I}_{m} - XX^{\mathsf{T}}\right) H
\end{aligned}\end{equation}}.
$$
</p>

<details>
	<summary>In the paper, a really nice derivation of the orthogonal projection is given, without invoking the regular value theorem. Hence I provide it here in details.</summary>

	Consider the metric of the Stiefel manifold being induced from the Frobenius inner product from the ambiant space. The normal space to the tangent space \(T_{X} \mathrm{St}(m,k)\) is denoted by \((T_{X} \mathrm{St}(m,k))^{\perp}\), consisting of matrices \(N\) that satisfies
	<p>
	$$
	\langle H, N\rangle = \mathrm{Tr}\left\{ H^{\mathsf{T}} N\right\} = 0
	$$
	</p>
	for all tangent vectors \(H \in T_{X} \mathrm{St}(m,k)\). From the second description of the tangent space, by assuming \(N = XS + X^{\perp} Z\) we can deduce that \(Z=0\) and \(S\) is symmetric. I.e., the normal space at \(X\) must be of the form
	$$
		\left\{ N \in \mathbb{R}^{m\times k} \middle\vert N = XS, S\text{ is symmetric} \right\}.
	$$
	Since we have the unique decomposition \(\mathbb{R}^{m \times k} = T_{X} \mathrm{St}(m,k) \oplus (T_{X} \mathrm{St}(m,k))^\perp\), there exists unique matrices \(\Omega\) (skew-symmetric), \(Z\), and \(S\) (symmetric) that satisfy
	$$
		H = X \Omega + X_{\perp} Z + XS.
	$$
	Henceforth, we obtain \(S = \mathrm{sym}(X^{\mathsf{T}} H)\), and
	$$
		\Pi_X(H) = H - XS = H - X \cdot \mathrm{sym}(X^{\mathsf{T}} H). \;\;\;\;\; \blacksquare
	$$
</details>

<br>

## Geodesic equation
This paper by Edelman et al. focuses at optimization over the orthogonally constrained sets of Stiefel manifolds or the Grassmanian manifolds. In manifold optimization, it is crucial to obtain the geodesics on the manifold so as to obtain second order or higher order derivatives. These are the main motivations of this work.

In differential geometry, the geodesics is defined with respect to a connection \\(\nabla\\) on the manifold. For our case, we consider the unique *Levi-Civita connection* induced by the Frobenius inner product.

Let \\(X(t)\\) be the geodesic curve on \\(\mathrm{St}(m,k)\\), its covariant derivative is zero with respect to itself. That it to say, it is of constant velocity on the manifold:
<p>
$$
\nabla_{\dot{X}} \dot{X} = 0.
$$
</p>
Since we consider the Stiefel manifold to be embedded within \\(\mathbb{R}^{m \times k}\\), we can equivalently say that the acceleration of the geodesic must be in the normal direction:
<p>
$$\begin{align*}
&\nabla_{\dot{X}} \dot{X} = \left(\ddot{X}\right)_{\mathrm{tangent}}= 0 \\
&\Rightarrow \ddot{X} \in \left(T_{X}\mathrm{St}(m,k)\right)^{\perp} \\
&\Rightarrow \ddot{X}(t) = X(t) S(t),
\end{align*}$$
</p>
where \\(S\\) is a symmetric matrix that depends on \\(t\\) as well. Furthermore, since \\(X^{\mathsf{T}}(t) X(t) = \mathbb{I}_m\\) for all \\(t\\),
<p>
$$
\begin{align*}
	&\frac{\mathrm{d}^2}{\mathrm{d}t^2} X^{\mathsf{T}} X = \ddot{X}^{\mathsf{T}} X + 2 \dot{X}^{\mathsf{T}} \dot{X} + X \ddot{X}^{\mathsf{T}} = 0 \\
	&\Rightarrow S X^{\mathsf{T}} X + 2 \dot{X}^{\mathsf{T}} \dot{X} + X^{\mathsf{T}} X S = 0 \\
	&\Rightarrow S = - \dot{X}^{\mathsf{T}} \dot{X}.
\end{align*}
$$
</p>
We have thus obtained the geodesic equation on the Stiefel manifold:
<p>
$$
\boxed{
	\ddot{X} + X \dot{X}^{\mathsf{T}} \dot{X} = 0
}.
$$
</p>
It should be noted that unlike in differential geometry, we like to express our equations under an extrinsic coordinate (\\(\mathbb{R}^{m \times k}\\)) when analyzing the geometry of a matrix manifold. The expressions beomce clean and coordinate-free.

Let us solve the geodesic equation! Instead of just giving you the answer and spoiling the fun, we will derive the solution from the geodesic equation step by step. Let us first state our initial conditions: we will be deriving a geodesic \\(\Gamma_{X,H}(t)\\) (abbreviated as \\(\Gamma\\))emanating from \\(X \in \mathrm{St}(m,k)\\) in the direction of \\(H \in T_X \mathrm{St}(m,k)\\). For an illustration, see the figure at the top of the post.

### The solution in the paper
Within the paper, they solved the geodesic equations by noticing the invariants of motion. The two invariants are
\\(\Gamma^{\mathsf{T}}(t) \Gamma(t) = \mathbb{I}\\) and \\(\Gamma^{\mathsf{T}}(t) \dot{\Gamma}(t) = A \\). The first one is trivial, and the second is obtained by fiddling around with the geodesic equation:
<p>
$$
\begin{align*}
	0 &= \ddot{\Gamma} + \Gamma \dot{\Gamma}^{\mathsf{T}} \dot{\Gamma} \\
	\Rightarrow 0 &= \Gamma^{\mathsf{T}} \ddot{\Gamma} + \dot{\Gamma}^{\mathsf{T}} \dot{\Gamma} \\
	&= \frac{\mathrm{d}}{\mathrm{d}t} \Gamma^{\mathsf{T}} \dot{\Gamma}.
\end{align*}
$$
</p>
Since \\(\dot{\Gamma}\\) is a tangent vector, we have \\(A\\) is skew-symmetric. Considering \\(t=0\\), we immediately see that \\(A = X^{\mathsf{T}} H\\). From these invariants, and from an observation[^Lippert] made by Ross Lippert, they reduced the second-order geodesic equation into a first-order differential equation that is easily solvable.

[^Lippert]: It is a stroke of genius in my opinion, as this definition of a state variable came out of the blue.

In detail: he considered a function \\(S(t) = \dot{\Gamma}^{\mathsf{T}} \dot{\Gamma}\\), satisfying
<p>
$$
\begin{align*}
	\dot{S}(t) &= \ddot{\Gamma}^{\mathsf{T}} \dot{\Gamma} + \dot{\Gamma}^{\mathsf{T}} \ddot{\Gamma} \\
	&= - \dot{\Gamma}^{\mathsf{T}} \dot{\Gamma} \Gamma^{\mathsf{T}} \dot{\Gamma} - \dot{\Gamma}^{\mathsf{T}} \Gamma \dot{\Gamma}^{\mathsf{T}} \dot{\Gamma} \\
	&= -S(t) A - A^{\mathsf{T}} S(t) \\
	&= AS - SA \\
	&= [A,S].
\end{align*}
$$
</p>
The solution to the differential equation above is
<p>
$$
	S(t) = \mathrm{e}^{tA} S_{0} \mathrm{e}^{-tA}
$$
</p>
with the initial state being \\(S_{0} = H^{\mathsf{T}} H\\).

Finally, consider the following equations:
<p>
$$
\begin{align*}
	\frac{\mathrm{d}}{\mathrm{d}t} \left[\begin{matrix}
		\Gamma \mathrm{e}^{tA} & \dot{\Gamma} \mathrm{e}^{tA}
	\end{matrix}\right] &= \left[\begin{matrix}
		\dot{\Gamma} \mathrm{e}^{tA} + \Gamma \mathrm{e}^{tA} A & -\Gamma \dot{\Gamma}^{\mathsf{T}} \dot{\Gamma} \mathrm{e}^{tA} + \dot{\Gamma} \mathrm{e}^{tA} A
	\end{matrix}\right] \\
	&= \left[\begin{matrix}
		\dot{\Gamma} \mathrm{e}^{tA} + \Gamma \mathrm{e}^{tA} A & -\Gamma \mathrm{e}^{tA} S_0  + \dot{\Gamma} \mathrm{e}^{tA} A
	\end{matrix}\right] \\
	&= \left[\begin{matrix}
		\Gamma & \dot{\Gamma}
	\end{matrix}\right] \left[\begin{matrix}
		A & -S_0 \\ \mathbb{I}_k & A
	\end{matrix}\right] \\
	\Rightarrow \left[\begin{matrix}
		\Gamma(t) \mathrm{e}^{tA} & \dot{\Gamma}(t) \mathrm{e}^{tA}
	\end{matrix}\right] &= \left[\begin{matrix}
		\Gamma(0) & \dot{\Gamma}(0)
	\end{matrix}\right] \cdot \exp\left(t \left[\begin{matrix}
		A & -S_0 \\ \mathbb{I}_k & A
	\end{matrix}\right]\right).
\end{align*}
$$
</p>

Thus, we have identified the geodesic to be
<p>
$$
\boxed{\begin{equation*}
	\Gamma_{X,H}(t) = \left[\begin{matrix}
		X & H
	\end{matrix}\right] \cdot \exp\left(t \left[\begin{matrix}
		X^{\mathsf{T}}H & -H^{\mathsf{T}}H \\
		\mathbb{I}_k & X^{\mathsf{T}}H
	\end{matrix}\right]\right) \cdot \mathbb{I}_{2k,k} \cdot \mathrm{e}^{-tX^{\mathsf{T}}H}
\end{equation*}},
$$
</p>
where \\(\mathbb{I}_{2k,k}\\) is the first \\(k\\) columns of \\(\mathbb{I} _{2k}\\).

### My solution
A different approach is given here. 

Inspired by how in control theory, the state space model allows us to transform high-order linear ODEs (ordinary differential equations) into a first order ODE, I introduce the state vector \\([\Gamma,\dot{\Gamma}]\\) and analyzed its derivative:
<p>
$$
\begin{align*}
	\frac{\mathrm{d}}{\mathrm{d}t} \left[\begin{matrix}
		\Gamma & \dot{\Gamma}
	\end{matrix}\right] &= \left[\begin{matrix}
		\dot{\Gamma} -\Gamma \dot{\Gamma}^{\mathsf{T}} \dot{\Gamma}
	\end{matrix}\right] = \left[\begin{matrix}
		\Gamma & \dot{\Gamma}
	\end{matrix}\right] \left[\begin{matrix}
		0 & -S(t) \\ \mathbb{I}_{k} & 0
	\end{matrix}\right], \\
	&= \lim_{\mathrm{d}t\rightarrow 0} \frac{1}{\mathrm{d}t} \left(\left[\begin{matrix}
		\Gamma(t+\mathrm{d}t) & \dot{\Gamma}(t+\mathrm{d}t)
	\end{matrix}\right] - \left[\begin{matrix}
		\Gamma(t) & \dot{\Gamma}(t)
	\end{matrix}\right]\right)\\	
	\Rightarrow \left[\begin{matrix}
		\Gamma & \dot{\Gamma}
	\end{matrix}\right] &= \left[\begin{matrix}
		\Gamma(0) & \dot{\Gamma}(0)
	\end{matrix}\right] \cdot \lim_{N\rightarrow\infty}\overrightarrow{\prod_{k=0}^{N-1}} \left(\mathbb{I} + \frac{t}{N} \left[\begin{matrix}
		0 & -S(tk/N) \\ \mathbb{I} & 0
	\end{matrix}\right]\right),
\end{align*}
$$
</p>
where \\(\overrightarrow{\prod}\\) is the product ordered from left to right and \\(\mathrm{d}t = t/N\\).

The infinite product can be further analysed. Note that since I am not a mathematician, I will describe what I did in each step in details, but not rigorously. First off, the infinite product reminds me of the (one of the) definition to the matrix exponential:
<p>
$$
\begin{align*}
	&\mathbb{I} + \frac{t}{N} \left[\begin{matrix}
		0 & -S(tk/N) \\ \mathbb{I} & 0
	\end{matrix}\right] \\
	&= \mathbb{I} + \frac{t}{N} \left[\begin{matrix}
		0 & -\mathrm{e}^{tkA/N} S_0 \mathrm{e}^{-tkA/N} \\ \mathbb{I} & 0
	\end{matrix}\right] \\
	&= \left[\begin{matrix}
		\mathrm{e}^{tkA/N} & 0 \\ 0 & \mathrm{e}^{tkA/N}
	\end{matrix}\right] \left(\mathbb{I} + \frac{t}{N}\left[\begin{matrix}
		0 & -S_0 \\ \mathbb{I} & 0
	\end{matrix}\right]\right) \left[\begin{matrix}
		\mathrm{e}^{-tkA/N} & 0 \\ 0 & \mathrm{e}^{-tkA/N}
	\end{matrix}\right].
\end{align*}
$$
</p>
The infinite product then becomes
<p>
$$
\begin{align*}
	&\lim_{N\rightarrow \infty} \left(\overrightarrow{\prod_{k=0}^{N-1}} \left(\mathbb{I} + \frac{t}{N} \left[\begin{matrix}
		0 & -S_0 \\ \mathbb{I} & 0
	\end{matrix}\right]\right) \left[\begin{matrix}
		\mathrm{e}^{tA/N} & 0 \\ 0 & \mathrm{e}^{-tA/N}
	\end{matrix}\right]\right) \left[\begin{matrix}
		\mathrm{e}^{-t(N-2)A/N} & 0 \\ 0 & \mathrm{e}^{-t(N-2)A/N}
	\end{matrix}\right] \\
	&= \lim_{N\rightarrow \infty} \left(\left(\mathbb{I} + \frac{t}{N}\left[\begin{matrix}
		0 & -S_0 \\ \mathbb{I} & 0
	\end{matrix}\right]\right) \left[\begin{matrix}
		\mathbb{I} + \frac{tA}{N} & 0 \\ 0 & \mathbb{I} + \frac{tA}{N}
	\end{matrix}\right]\right)^N \left[\begin{matrix}
		\mathrm{e}^{-tA} & 0 \\ 0 & \mathrm{e}^{-tA}
	\end{matrix}\right] \\
	&= \lim_{N\rightarrow \infty} \left(\mathbb{I} + \frac{t}{N} \left[\begin{matrix}
		A & -S_0 \\ \mathbb{I} & A
	\end{matrix}\right]\right)^N \left[\begin{matrix}
		\mathrm{e}^{-tA} & 0 \\ 0 & \mathrm{e}^{-tA}
	\end{matrix}\right] \\
	&= \exp\left(t \left[\begin{matrix}
		A & -S_0 \\
		\mathbb{I} & A
	\end{matrix}\right]\right) \cdot \left[\begin{matrix}
		\mathrm{e}^{-tA} & 0 \\ 0 & \mathrm{e}^{-tA}
	\end{matrix}\right].
\end{align*}
$$
</p>

The rest of the derivation is the same as in the paper and I'll not repeat them here. Hence, we obtain the same result as above.

To made the argument more rigorous, one should also check the convergence of the infinite product, and the approximations used do not affect the final product.

### Sanity check
As a small check for correctness, let us restrict our attention to the orthogonal matrices \\(\mathrm{O}(m) = \mathrm{St}(m,m)\\), with the tangent direction of the form \\(H = X\Omega\\), where \\(\Omega\\) is skew-symmetric. Then the geodesic will be
<p>
$$
\begin{align*}
	\Gamma_X(tH) &= \left[\begin{matrix}
		X & X\Omega \\
	\end{matrix}\right] \cdot \exp\left(t \left[\begin{matrix}
		\Omega & \Omega^2 \\ \mathbb{I}_k & \Omega
	\end{matrix}\right]\right) \left[\begin{matrix}
		\mathbb{I}_k \\ 0
	\end{matrix}\right] \cdot \exp\left(-\Omega t\right).
\end{align*}
$$
</p>
This can be greatly simplified. Notice that
<p>
$$
\begin{align*}
	\Gamma_X(tH) &= \left[\begin{matrix}
		X & X\Omega \\
	\end{matrix}\right] \left[\begin{matrix}
		\Omega & \Omega^2 \\ \mathbb{I}_k & \Omega
	\end{matrix}\right] \\
	&= \left[\begin{matrix}
		2X\Omega & 2X\Omega^2 \\
	\end{matrix}\right] \\
	&= \left[\begin{matrix}
		X & X\Omega \\
	\end{matrix}\right] \left[\begin{matrix}
		2\Omega & 0 \\ 0 & 2\Omega
	\end{matrix}\right].
\end{align*}
$$
</p>
Therefore, since
<p>
$$
\begin{align*}
	\left[\begin{matrix}
		2\Omega & 0 \\ 0 & 2\Omega
	\end{matrix}\right] \cdot \left[\begin{matrix}
		\Omega & \Omega^2 \\ \mathbb{I}_k & \Omega
	\end{matrix}\right] = \left[\begin{matrix}
		\Omega & \Omega^2 \\ \mathbb{I}_k & \Omega
	\end{matrix}\right] \cdot \left[\begin{matrix}
		2\Omega & 0 \\ 0 & 2\Omega
	\end{matrix}\right],
\end{align*}
$$
</p>
we have
<p>
$$
\begin{align*}
	\Gamma_X(tH) &= \left[\begin{matrix}
		X & X\Omega \\
	\end{matrix}\right] \cdot \exp\left(t \left[\begin{matrix}
		2\Omega & 0 \\ 0 & 2\Omega
	\end{matrix}\right]\right) \left[\begin{matrix}
		\mathbb{I}_k \\ 0
	\end{matrix}\right] \cdot \exp\left(-\Omega t\right) \\
	&= \left[\begin{matrix}
		X & X\Omega \\
	\end{matrix}\right] \cdot \left[\begin{matrix}
		\exp(2\Omega t) & 0 \\ 0 & \exp(2\Omega t)
	\end{matrix}\right] \left[\begin{matrix}
		\mathbb{I}_k \\ 0
	\end{matrix}\right] \cdot \exp\left(-\Omega t\right) \\
	&= X \exp(\Omega t) = X \exp(t X^{\mathsf{T}} H).
\end{align*}
$$
</p>
This is indeed the geodesic on the orthogonal matrices under the Frobenius norm.

### Other forms of geodesic solution
Besides writing the geodesic originating at \\(X\in\mathrm{St}(m,k)\\) with tangential velocity \\(H \in T_X\mathrm{St}(m,k)\\) as
<p>
$$
\boxed{\begin{equation*}
	\Gamma_{X,H}(t) = \left[\begin{matrix}
		X & H
	\end{matrix}\right] \cdot \exp\left(t \left[\begin{matrix}
		X^{\mathsf{T}}H & -H^{\mathsf{T}}H \\
		\mathbb{I}_k & X^{\mathsf{T}}H
	\end{matrix}\right]\right) \cdot \mathbb{I}_{2k,k} \cdot \exp\left(-tX^{\mathsf{T}}H\right)
\end{equation*}},
$$
</p>
two other forms are also common.

The second form is
<p>
$$
\boxed{\begin{equation*}
	\Gamma_{X,H}(t) = \overline{X} \cdot \exp\left(t \left[\begin{matrix}
		2X^{\mathsf{T}} H & -H^{\mathsf{T}} X_{\perp} \\
		X_{\perp}^{\mathsf{T}} H & 0
	\end{matrix}\right]\right) \cdot \mathbb{I}_{m,k} \cdot \exp\left(-tX^{\mathsf{T}}H\right)
\end{equation*}},
$$
</p>
where \\(\overline{X} = [X, X_{\perp}]\\) is an orthogonal matrix. To obtain this second form from the first, one simply observe that: If the tangential velocity is written as \\(H = X\Omega + X_{\perp}Z\\) with \\(\Omega\\) being skew-symmetric, then
<p>
$$
\left[\begin{matrix}
    X & H
\end{matrix}\right] = \left[\begin{matrix}
    X & X_\perp
\end{matrix}\right] \left[\begin{matrix}
    \mathbb{I} & \Omega \\ 0 & Z
\end{matrix}\right]
$$
</p>
and
<p>
$$
\left[\begin{matrix}
    \mathbb{I} & \Omega \\ 0 & Z
\end{matrix}\right] \left[\begin{matrix}
    X^{\mathsf{T}} H & -H^{\mathsf{T}} H \\ \mathbb{I} & X^{\mathsf{T}} H
\end{matrix}\right] = \left[\begin{matrix}
    2X^{\mathsf{T} H} & -H^{\mathsf{T}} X_{\perp} \\ X_{\perp}^{\mathsf{T}} H & 0
\end{matrix}\right] \left[\begin{matrix}
    \mathbb{I} & \Omega \\ 0 & Z
\end{matrix}\right]
$$
</p>
holds. The relation between the two equations then trivially follows.

The third form to the geodesic is
<p>
$$
\boxed{\begin{equation*}
	\Gamma_{X,H}(t) = \exp\left(t \left(HX^{\mathsf{T}} - XH^{\mathsf{T}}\right)\right) \cdot X \cdot \exp\left(-tX^{\mathsf{T}}H\right)
\end{equation*}}.
$$
</p>
From this form, we can also obtain the first derivative, second derivative, and parallel transport as
<p>
$$
\boxed{\begin{align*}
	\dot{\Gamma}_{X,H}(t) &= \exp\left(t \left(HX^{\mathsf{T}} - XH^{\mathsf{T}}\right)\right) \cdot H \cdot \exp\left(-tX^{\mathsf{T}}H\right), \\
    \ddot{\Gamma}_{X,H}(t) &= \exp\left(t \left(HX^{\mathsf{T}} - XH^{\mathsf{T}}\right)\right) \cdot (-XH^{\mathsf{T}}X) \cdot \exp\left(-tX^{\mathsf{T}}H\right), \\
    \tau_{\Gamma_{X,H}(t)}[K] &= \exp\left(t \left(HX^{\mathsf{T}} - XH^{\mathsf{T}}\right)\right) \cdot K \cdot \exp\left(-tX^{\mathsf{T}}H\right).
\end{align*}}.
$$
</p>
The parallel transport of a tangent vector \\(K \in T_X\mathrm{St}(m,k)\\) to another tangent vector \\(K \in T_{\Gamma_{X,H}(t)}\mathrm{St}(m,k)\\) is denoted by \\(\tau_{\Gamma_{X,H}(t)}[K]\\). It is defined as the solution \\(\tau(t)\\) to the differential equation
<p>
$$
\nabla_{\dot{\Gamma}_{X,H}(t)} \tau = 0.
$$
</p>
Luckily, since we already have the equation to the geodesic, the parallel transport can easily be derived as
<p>
$$
\tau_{\Gamma_{X,H}(t)}[K] = \left.\frac{\mathrm{d}}{\mathrm{d}s}\right|_{s=0}\Gamma_{X,H+sK}(t).
$$
</p>

One can notice that the three boxed equations are all very much similar, with the only difference being changing the term at the middle, which is their values when evaluated at \\(t=0\\). The left and right multiplication by the two exponentials seem to transport the term in the middle across the Stiefel manifold along a geodesic.

This third form can be obtained from the second by noticing that
<p>
$$
\overline{X} \cdot \exp\left(t \left[\begin{matrix}
		2X^{\mathsf{T}} H & -H^{\mathsf{T}} X_{\perp} \\
		X_{\perp}^{\mathsf{T}} H & 0
	\end{matrix}\right]\right) \cdot \overline{X}^{\mathsf{T}} = \exp\left(t(HX^{\mathsf{T}} - XH^\mathsf{T})\right).
$$
</p>

Of course, these so-called "derivation" of mine proposed above actually gives no further insight as to *why* they are written so. The works from which these are first proposed are organized in "[Computing the Riemannian Logarithm on the Stiefel Manifold: Metrics, Methods and Performance](https://arxiv.org/abs/2103.12046)." For example, the third form is derived in "[Real Stiefel Manifolds: An Extrinsic Point of View](https://ieeexplore.ieee.org/abstract/document/8514292)" by Hüper and Ullrich. I'll perhaps go over these recent[^1] works in the future.

[^1]: Yes, 2018 is really recent in these areas of research as of when I wrote this post, which is 2025.

Which formula is the best? Well, for aesthetics, I will definitely choose the third one as its formula is the simplest. However, if \\(m\gg 2k\\), the first formula is way faster for computation. This is especially important when working on an optimization of a large system.

## The canonical metric and the \\(\alpha\\)-metric
A geodesic is determined by the connection chosen. And if we choose the connection to be the unique Levi-Civita (Riemannian) connection associated with a metric, the geodesic is then determined by the metric used.

In the [previous post]((/posts/2025/08/blog-post-4/)), we only considered the Forbenius inner product of the form: for \\(H_1,H_2\in T_X\mathrm{St}(m,k)\\),
<p>
$$
g_{e}(H_1,H_2) = \langle H_1,H_2 \rangle_F = \mathrm{Tr}\left\{H_1^\mathsf{T} H_2\right\}.
$$
</p>
The symbol \\(g\\) is the metric, the inner product used -- or in a fancier differential geometrical term: the *first fundamental form* of the manifold. The subscript \\(e\\) denotes it is derived from the ambient Euclidean metric.

However, as pointed out in the work by Edelman, this norm treats the degrees of freedom on the tangent space with unequal weightings: let \\(H = X\Omega + X_{\perp}Z\\), then
<p>
$$
g_e(H,H) = \mathrm{Tr}\left\{\Omega^{\mathsf{T}} \Omega + Z^{\mathsf{T}} Z\right\} = 2 \sum_{i<j} \Omega_{ij} + \sum_{i,j} Z_{ij}.
$$
</p>
The degrees of freedom in \\(\Omega\\) have double the weights as those in the matrix \\(Z\\).

For this reason, the *canonical metric* is introduced:
<p>
$$
g_{c}(H,H) = \mathrm{Tr}\left\{H^\mathsf{T} \left(\mathbb{I} - \frac{1}{2} XX^{\mathsf{T}}\right) H\right\} = \frac{1}{2} \mathrm{Tr}\left\{\Omega^{\mathsf{T}} \Omega\right\} + \mathrm{Tr}\left\{Z^{\mathsf{T}} Z\right\}.
$$
</p>
giving equal weightings to all degrees of freedom. As this metric satisfies the parallelogram law, we can use the polarization identity to convert it into an inner product.

This metric in turn induces a different (but a simpler!) formula for the geodesic.

In the work "[A Lagrangian approach to extremal curves on Stiefel manifolds](https://www.researchgate.net/publication/347034260_A_Lagrangian_approach_to_extremal_curves_on_Stiefel_manifolds)", they even considered a one-parameter family of inner products of the form
<p>
$$
g_{\alpha}(H_1,H_2) = \frac{1}{2(\alpha+1)} \mathrm{Tr}\left\{\Omega_1^{\mathsf{T}} \Omega_2\right\} + \mathrm{Tr}\left\{Z_1^{\mathsf{T}} Z_2\right\}.
$$
</p>
If \\(\alpha = -0.5\\), this is the Euclidean metric; while if \\(\alpha = 0\\), this is the canonical metric.

For the \\(\alpha\\)-metric \\(g_\alpha\\), the induced geodesic is
<p>

$$
\boxed{\begin{equation*}
	\Gamma_{X,H}(t) = \exp\left(t \left(-\frac{2\alpha + 1}{\alpha + 1} XX^{\mathsf{T}}HX^{\mathsf{T}} + HX^{\mathsf{T}} - XH^{\mathsf{T}}\right)\right) \cdot X \cdot \exp\left(t\cdot \frac{\alpha}{\alpha+1}X^{\mathsf{T}}H\right)
\end{equation*}}.
$$
</p>
Crazy formula, right? To know all the secrets and geometry (besides the boring algebra) lurking within, one should definitely read the papers above.

## Obtaining the geodesic equation

In terms of the intrinsic local coordinates of a manifold, one can express the geodesic equation of a curve \\(x(t)\in\mathcal{M}\\) as
<p>

$$
\ddot{x}^{k} + \Gamma_{ij}^{k} \dot{x}^{i} \dot{x}^{j} = 0,
$$
</p>
where \\(x^i\\) is the \\(i\\)th coordinate of \\(x\\), \\(\Gamma _{ij}^{k}\\) is the *Christoffel symbol*, and the Einstein summation convention is used.

In the study of matrix manifolds, however, we like to express things extrinsically as the manifold is embedded in a larger Euclidean space (the metric can be other than Euclidean though). So for a curve \\(X(t)\\) over a matrix manifold \\(\mathcal{M}\\), the geodesic equation can be written in the form of
<p>

$$
\ddot{X} + \Gamma(\dot{X},\dot{X}) = 0.
$$
</p>

One can then immediately interpret the effect of the Christoffel symbols as removing the "normal" components.

### Intrinsic viewpoint
When parallel transporting a vector \\(K _0 \in T _{X _0}\mathcal{M}\\) over a geodesic \\(X(t)\\) with initial velocity \\(H _0 \in T _{X _0}\mathcal{M}\\), a procedure one can take is to iteratively remove the normal component to \\(K(t)\\) as it is moving along \\(X(t)\\).
 
We again start our discussion from the intrinsic viewpoint well established in differential geometry. For the vector \\(K _0\\) to be parallel transported, we require that it is *parallel* along \\(\dot{X}\\). I.e., we have that \\(K(t)\\), the parallel transport of \\(K _0\\) as time \\(t\\) varies, must satisfy the differential equation
<p>

$$
\nabla_{\dot{X}}K = 0.
$$
</p>

Expanding using the intrinsic local coordinates, let the coordinates of \\(K\\) be \\\(y^i\\). Then, one has the relation
<p>

$$
\dot{y}^k + \Gamma_{ij}^k \dot{x}^i \dot{y}^j = 0.
$$
</p>
This suggest the extrinsic form to the parallel transport equation to be
<p>

$$
\boxed{
    \dot{K} + \Gamma(\dot{X},K) = 0
},
$$
</p>
where the bilinear form \\(\Gamma(\dot{X},K)\\) is induced from the symmetric form \\(\Gamma(\dot{X},\dot{X})\\) point-wise. Let us verify the above from an extrinsic point of view. (I will not check the smoothness as I am an engineer.)

### Extrinsic viewpoint
Consider the manifold being embedded in an external space. Using the same arguments as in the [first post](/posts/2025/08/blog-post-4/), we have
<p>

$$
\begin{align*}
    &\nabla_{\dot{X}}K = \left(\dot{K}\right)_{\mathrm{tangent}} = 0, \\
    &\Rightarrow \dot{K} \in (T_X\mathcal{M})^\perp.
\end{align*}
$$
</p>

What is the form of the normal component, then, that we need to remove?

Consider time going from \\(t=0\\) to \\(t=\varepsilon\\), the point \\(X(t)\\) moves from \\(X(0) = X _0\\) to \\(X(\varepsilon)\\). Then, by directly moving \\(K _0\\) from \\(X _0\\) to \\(X(\varepsilon)\\), it is required that we remove the normal component to \\(K _0\\) so that the transported vector remains on the tangent space. The normal component is
<p>

$$
\Pi^\perp_{X(\varepsilon)}(K_0).
$$
</p>
This is the projection onto the normal space. Thus,
<p>

$$
\begin{aligned}
    K(\varepsilon) &= K_0 - \Pi^\perp_{X(\varepsilon)}(K_0), \\
    \Rightarrow \dot{K}(0) &= \lim_{\varepsilon \rightarrow 0} \frac{K(\varepsilon) - K_0}{\varepsilon} \\
    &= -\lim_{\varepsilon \rightarrow 0} \frac{1}{\varepsilon} \cdot \Pi^\perp_{X(\varepsilon)}(K_0) \\
    &= -\lim_{\varepsilon \rightarrow 0} \frac{1}{\varepsilon} \cdot \left(K_0 - \Pi_{X(\varepsilon)}(K_0)\right) \\
    &= \lim_{\varepsilon \rightarrow 0} \frac{1}{\varepsilon} \cdot \left(\Pi_{X(\varepsilon)}(K_0) - \Pi_{X_0}(K_0)\right), \\
    \Rightarrow \dot{K}(t) &= \lim_{\varepsilon \rightarrow 0} \frac{1}{\varepsilon} \left(\Pi_{X(t+\varepsilon)}(K(t)) - \Pi_{X(t)}(K(t))\right) \\
    &= \left.\frac{\mathrm{d}}{\mathrm{d}s}\right|_{s=t} \Pi_{X(s)}(K(t)).
\end{aligned}
$$
</p>
We thus have the parallel transform equation
<p>

$$
\boxed{
    \dot{K}(t) - \left.\frac{\mathrm{d}}{\mathrm{d}s}\right|_{s=t} \Pi_{X(s)}(K(t)) = 0
}.
$$
</p>
The function \\(X(t)\\) is the geodesic, and the \\(X, K\\) without \\(t\\) behind it are constants evaluated at \\(t=0\\) (they are the initial conditions).

### Comparing the two viewpoints...
Comparing the two viewpoints, we see that
<p>

$$
\boxed{
    \Gamma(\dot{X}(t),K(t)) = - \left.\frac{\mathrm{d}}{\mathrm{d}s}\right|_{s=t} \Pi_{X(s)}(K(t))
}.
$$
</p>

Consider the Stiefel manifold \\(\mathrm{St}(m,k)\\) as an example, we have
<p>

$$
\Pi_{X}(K) = K - X \cdot \mathrm{sym}(X^\mathsf{T} K).
$$
</p>
From the arguments given by Edelman, we also have
<p>

$$
\Gamma(\dot{X},K) = X \cdot \mathrm{sym}(\dot{X}^\mathsf{T} K).
$$
</p>
The validity of the boxed equation can be immediately seen.

Whether or not the equivalence of the left and right side of the boxed equation can be directly obtained is yet unknown.

### If the geodesic equation is solved...
In the previous section, I introduced the formula for the parallel transport \\(\tau\\) given the geodesic \\(\gamma\\) as
<p>

$$
\boxed{
    K(t) \equiv \tau_{\gamma_{X_0,H_0}(t)}[K_0] = \left.\frac{\mathrm{d}}{\mathrm{d}s}\right|_{s=0}\gamma_{X_0,H_0+sK_0}(t)
}.
$$
</p>
The parallel transport map is \\(\tau _{\gamma _{X _0,H _0}(t)}: T _{X _0}\mathcal{M} \rightarrow T _{\gamma _{X _0,H _0}(t)}\mathcal{M}\\).

The immediate question will be asking whether the two parallel transport equations compatible? Sadly, I have yet figure out how to show their equivalence.