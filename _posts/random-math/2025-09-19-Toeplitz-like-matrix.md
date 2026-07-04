---
layout: post
title: Linear Recurrence Relations and the Spectrum of Toeplitz-Like Matrices
date: 2025-09-19
description: "This post discusses how the solution to linear recurrence relations relates to the spectrum of certain Toeplitz-like matrices."
tags: math
categories: random-math
toc:
    sidebar: left
---

> This post discusses how the solution to linear recurrence relations relates to the spectrum of certain Toeplitz-like matrices. This observation connects to solving for the normal mode of spring-mass systems

---
## Linear Recurrence Relations
A linear (homogeneous) recurrence relation of order $$k$$ is of the form

$$
\boxed{
    x_n = a_{1} x_{n-1} + a_2 x_{n-2} + \cdots + a_{k} x_{n-k}
}
$$

can be efficiently rewritten as a matrix equation

$$
\left[\begin{matrix}
    \textcolor{cyan}{x_{n}} \\ x_{n-1} \\ x_{n-2} \\ \ldots \\ x_{n-k+1}
\end{matrix}\right] =
\left[\begin{array}{cccc:c}
    \textcolor{cyan}{a_1} & \textcolor{cyan}{a_2} & \textcolor{cyan}{\cdots} & \textcolor{cyan}{a_{k-1}} & \textcolor{cyan}{a_k} \\ \hdashline
    1 \\
    & 1 \\
    && \ddots \\
    &&& 1 & 0
\end{array}\right] 
\left[\begin{matrix}
    x_{n-1} \\ x_{n-2} \\ x_{n-3} \\ \ldots \\ x_{n-k}
\end{matrix}\right].
$$

Writing the equation above as $$\mathbf{x}_n = A \mathbf{x}_{n-1}$$, we can solve for any $$x_n$$ given the initial condition $$\mathbf{x}_0$$ by finding $$A^n$$ for arbitrary $$n$$.

> ##### TIP
> From the theory of linear algebra, for a ***diagonalizable*** matrix $$A$$, one can easily see that the elements of $$A^n$$ are linear combinations of $$\lambda^n$$'s, where the $$\lambda$$'s are the eigenvalues of $$A$$.
>
> For non-diagonalizable matrices, on the other hand, its eigenvalues have geometric multiplicity larger than one. Suppose $$\lambda$$ has a geometric multiplicity of $$3$$, then still, the resulting matrix $$A^n$$ is a linear combination of $$\lambda^n$$, $$n\lambda^n$$, and $$n^2\lambda^n$$.
{: .block-tip }

From the tip above, we see that the elements of $$\mathbf{x}_n$$ are linear combinations of $$\lambda^n$$, and so is $$x_n$$ (here we assume the diagonalizability of $$A$$, but the same idea applies for non-diagonalizable ones). This is the method of ***characteristic equation***, useful for solving linear recurrence relations.

<!-- ### Möbius-Transform-Type Recurrence Relations
Möbius transform is defined as the fractional linear transformation

$$
f(z) = \frac{az + b}{cz + d}.
$$

The Möbius-transform-type recurrence relations are of the form

$$
\boxed{
    x_n = \frac{a x_{n-1} + b}{c x_{n-1} + d}.
}
$$

> ##### TIP
> The Möbius transform satisfies the following property: if
> 
> $$
> \left[\begin{matrix}
>   a_k & b_k \\ c_k & d_k
> \end{matrix}\right] = \left[\begin{matrix}
>   a & b \\ c & d
> \end{matrix}\right]^k,
> $$
> 
> then
> 
> $$
> \underbrace{(f \circ f \circ \cdots \circ f)}_{\times k} (z) = \frac{a_k z + b_k}{c_k z + d_k}.
> $$
{: .block-tip}

### Fraction-Type Recurrence Relations
Similar to the idea above, we now consider the recurrence relation -->

---
## Spectrum of Toeplitz-Like Matrices
A Toeplitz matrix is a matrix with diagonals identified, i.e.,

$$
\begin{matrix}
    A = \left[\begin{matrix}
        a_0 & a_1 & \cdots & \cdots & a_k \\
        a_{-1} & a_0 & a_1 & & \vdots \\
        \vdots & a_{-1} & a_0 & \ddots & \vdots \\
        \vdots & & \ddots & \ddots & a_{1} \\
        a_{-k} & \cdots & \cdots & a_{-1} & a_0 \\ 
    \end{matrix}\right]
\end{matrix}.
$$

Although finding the exact spectrum to an arbitrary Toeplitz matrix is a daunting task, we will be analyzing a few specific matrices and obtain their exact spectrum. Furthermore, out of the four examples given, the last two are not exactly Toeplitz. In fact, I termed them Toeplitz-like as they are almost Toeplitz with sparse perturbations.

My exploration of these certain Toeplitz-like matrices stemmed from the analysis of the normal mode frequency of a spring-mass system. Given a system of differential equations describing the motion of such spring-mass system, one can turn it into a recurrence relation by plugging in an Ansatz. The Ansatz is parameterized by the normal mode frequency. Then, the difference equations can be rewritten into a matrix equation of the form $$(A - \lambda I)x=0$$ with the existence of non-trivial solutions relying on the $$\lambda$$'s being the eigenvalues to $$A$$. The $$\lambda$$'s are related to the normal mode frequencies.

### Spring-mass ring

<br/><img src='/assets/img/blog/2025-09-19-ring.png' width="50%">

The first example we consider is an $$N$$ particle spring-mass chain forming a ring. This example naturally gives rise to a Toeplitz matrix that is also ***circulant***. The equation of motion for the $$n$$th particle is

$$
m \ddot{x}_n = -k(x_{n} - x_{n-1}) - k(x_{n} - x_{n+1}).
$$

Plugging in the normal mode Ansatz $$x _n = a _n \cos(\omega t)$$ and setting $$\lambda = \omega^2 m / k$$, we have

$$
\left[\begin{matrix}
    2-\lambda & -1 & 0 & \cdots & 0& -1 \\
    -1 & 2-\lambda & -1 & \cdots & 0 & 0 \\
    0 & -1 & 2-\lambda & \cdots & 0 & 0 \\
    \vdots & \vdots & \vdots & \ddots & \vdots & \vdots \\
    0 & 0 & 0 & \cdots & 2-\lambda & -1 \\
    -1 & 0 & 0 & \cdots & -1 & 2-\lambda
\end{matrix}\right] \left[\begin{matrix}
    a_1 \\ a_2 \\ a_3 \\ \vdots \\ a_{N-1} \\ a_N
\end{matrix}\right]
$$

We can see that in this scenario, it is required that the $$\lambda$$'s be the eigenvalues of the matrix $$A$$ defined as

$$
A = \left[\begin{matrix}
    2 & -1 & 0 & \cdots & 0& -1 \\
    -1 & 2 & -1 & \cdots & 0 & 0 \\
    0 & -1 & 2 & \cdots & 0 & 0 \\
    \vdots & \vdots & \vdots & \ddots & \vdots & \vdots \\
    0 & 0 & 0 & \cdots & 2 & -1 \\
    -1 & 0 & 0 & \cdots & -1 & 2
\end{matrix}\right]_{N\times N}.
$$

To find the spectrum of $$A$$, there will be two methods: one utilizes the circulant structure, and the other utilizes our knowledge of linear recurrence relations while incorporating the implicit boundary condition $$a_0 = a_{N}$$. We will explore the latter one later.

We first notice that

$$
A = 2 I_N - J_N - J_N^\mathsf{T}
$$

where $$J_N$$ is the permutation matrix

$$
J_N = \left[\begin{matrix}
    0 & 1 & & & 0 \\
    & 0 & 1 \\
    & & \ddots & \ddots \\
    & & & \ddots & 1 \\
    1 & & & & 0
\end{matrix}\right].
$$

Since $$J_N^{-1} = J_N^\mathsf{T}$$, if the former has the eigenvalue-eigenvector pair $$(\mu,v)$$, then the latter has the eigenvalue-eigenvector pair $$(1/\mu,v)$$. Altogether, the eigenvalue of $$A$$ will be $$\lambda = 2 - \mu - \mu^{-1}$$. It can be easily found by induction that the characteristic polynomial to $$J_N$$ is $$\mu^N - 1$$. Thus, we have the eigenvalues to $$A$$ being

$$
\begin{aligned}
    \lambda_k &= 2 - \mathrm{e}^{\mathrm{i}\frac{2\pi}{N}k} - \mathrm{e}^{-\mathrm{i}\frac{2\pi}{N}k} &&(\mu_k = \mathrm{e}^{\mathrm{i}\frac{2\pi}{N}k}, k = 1\sim N) \\
    &= 2 - 2\cos\left(\frac{2\pi}{N}k\right) &&(k = 1\sim N) \\
    &= 4 \sin^2\left(\frac{\pi}{N}k\right) &&(k = 1\sim N).
\end{aligned}
$$

### Spring-mass chain between two walls

<br/><img src='/assets/img/blog/2025-09-19-2wall.png' width="60%">

The second scenario has both ends to a spring-mass chain fixed to walls. The particles satisfy the same equation of motion. However, the boundary conditions are now modified to

$$
x_0(t) = x_{N+1}(t) = 0.
$$

This means that we have the matrix $$A$$ as

$$
A = \left[\begin{matrix}
    2 & -1 \\
    -1 & 2 & -1 \\
    & -1 & 2 \\
    & & & \ddots & -1 \\
    & & & -1 & 2
\end{matrix}\right]_{N\times N}.
$$

This is again a Toeplitz matrix.

Unlike the previous case where the eigenvectors to the three matrix components are the same, the calculation for this case is much more intricate.

Instead of using the techniques from matrix algebra, let us instead refer back to the recurrence relations to find a solution. Using the same definition for $$\lambda$$, the recurrence relation $$a_n$$ satisfies is

$$
(2-\lambda) a_n = a_{n-1} + a_{n+1}
$$

with boundary condition

$$
a_0 = a_{N+1} = 0.
$$

Using the *characteristic method* for solving linear recurrence relations, we plug in the Ansatz of $$a_n = \alpha_1 r_1^n + \alpha_2 r_2^n$$ with $$r_1$$, $$r_2$$ satisfying

$$
r^2 - (2-\lambda) r + 1 = 0.
$$

There two solutions $$r _1$$ and $$r _2$$ satisfy $$r _1 + r _2 = 2 - \lambda$$ and $$r _1 r _2 = 1$$. For simplicity, denote $$r_1 = r$$ and $$r_2 = r^{-1}$$

Next, we plug in the initial conditions:

$$
\begin{align*}
    &\because a_0 = 0 = \alpha_1 + \alpha_2, \\
    &\therefore \alpha_1 = \alpha = -\alpha_2, \\
    &\because a_{N+1} = 0 = \alpha \left(r^{N+1} - r^{-(N+1)}\right), \\
    &\therefore r^{2N+2} = 1, \\
    &\Rightarrow r = \mathrm{e}^{\mathrm{i} \frac{\pi}{N+1}k} \;\;\;\;\;(k = 1\sim 2N+2).
\end{align*}
$$

However, note that $$r$$ and $$r^{-1}$$ may coincide, we can thus reduce the range of $$k$$ to $$k=1\sim N+1$$. Further, if $$k=N+1$$, $$r = r^{-1}$$, we will obtain $$a_n = 0$$ which is the trivial solution and is discarded. Hence, $$k=1\sim N$$. Lastly, we have

$$
\begin{align*}
    \lambda &= 2 - (r_1 + r_2) \\
    &= 2 - 2\cos\left(\frac{\pi}{N+1} k\right) \;\;\;\;\; (k = 1\sim N) \\
    &= 4\sin^2\left(\frac{\pi}{2(N+1)} k\right) \;\;\;\;\; (k = 1\sim N).
\end{align*}
$$

These are the $$N$$ eigenvalues to $$A$$.

> ##### NOTE
> Look how the tables have turned! In deriving the characteristic method for solving linear recurrence relations, we reformulate recurrence relations into a matrix equation and solve for the eigenvalues of the matrix.
>
> Now, however, in order to find the spectrum to a Toeplitz matrix, we instead convert it into a recurrence relation with specific boundary conditions.
{: .block-warning}

### Spring-mass chain with one end fixed and another end free

<br/><img src='/assets/img/blog/2025-09-19-1wall.png' width="60%">

Suppose the first mass is the one with spring connected to the wall and the $$N$$th mass is the one on the free end. For this case, the matrix $$A$$ is 

$$
A = \left[\begin{matrix}
    2 & -1 \\
    -1 & 2 & -1 \\
    & -1 & \ddots \\
    & & & 2 & -1 \\
    & & & -1 & 1
\end{matrix}\right]_{N\times N}.
$$

and the boundary conditions are

$$
a_0 = 0, a_{N+1} = a_{N}.
$$

Note that $$A$$ is no longer a Toeplitz matrix. However, it is still Toeplitz-like and it is ***tridiagonal***. This allows us to convert it into a linear recurrence relation.

Similarly, using the characteristic method for linear homogeneous recurrence relations, the general solution will be $$a _n = \alpha _1 r^n + \alpha _2 r^{-n} $$. We can plug in the boundary conditions to obtain 

$$
\begin{align*}
    &\because a_0 = 0, \\
    &\therefore a_n = \alpha \left(r^n - r^{-n}\right), \\
    &\because a_{N+1} = \alpha \left(r^{N+1} - r^{-N-1}\right) = a_{N} = \alpha \left(r^N - r^{-N}\right), \\
    &\therefore r^{N+1} - r^N = - (r^{-N} - r^{-N-1}), \\
    &\Rightarrow r^{2N+1} = -1 \;\;\;\;\;(r\neq0), \\
    &\Rightarrow r = \mathrm{e}^{\mathrm{i} \frac{\pi}{2N+1}(2k-1)} \;\;\;\;\;(k = 1\sim N).
\end{align*}
$$

There should be $$2N+1$$ solutions for $$r$$. By the same argument as the last example, however, we can reduce it down to $$N$$. The eigenvalues $$\lambda$$ of $$A$$ are finally obtained as

$$
\begin{align*}
    \lambda 
    &= 2 - 2\cos\left(\frac{\pi}{2N+1} (2k-1)\right) &&(k = 1\sim N) \\
    &= 4\sin^2\left(\frac{\pi}{2(N+1)} \left(k-\frac{1}{2}\right)\right) &&(k = 1\sim N).
\end{align*}
$$



### Spring-mass chain with two ends free

<br/><img src='/assets/img/blog/2025-09-19-0wall.png' width="60%">

This last example is also Toeplitz-like and tridiagonal. For this case, the matrix $$A$$ is 

$$
A = \left[\begin{matrix}
    1 & -1 \\
    -1 & 2 & -1 \\
    & -1 & \ddots \\
    & & & 2 & -1 \\
    & & & -1 & 1
\end{matrix}\right]_{N\times N}.
$$

and the boundary conditions are

$$
a_0 = a_1, a_{N+1} = a_{N}.
$$

Similarly using the characteristic method for linear homogeneous recurrence relations, the general solution will be $$a _n = \alpha _1 r ^n + \alpha _2 r ^{-n} $$. We can plug in the boundary conditions to obtain 

$$
\begin{align*}
    &\because a_0 = \alpha_1 + \alpha_2 = \alpha_1 r + \alpha_2 r^{-1} = a_1, \\
    &\therefore \alpha_1 r = -\alpha_2, \\
    &\because a_{N+1} = \alpha_1 r^{N+1} + \alpha_2 r^{-N-1} = \alpha_1 r^{N} + \alpha_2 r^{-N} = a_N, \\
    &\therefore r^{N+1} - r^{-N} = r^N - r^{-N+1}, \\
    &\Rightarrow r^{N+1} - r^N = r^{-N} - r^{-N+1}, \\
    &\Rightarrow r^{2N} = -1, \\
    &\Rightarrow r = \mathrm{e}^{\mathrm{i} \frac{\pi}{N} k} \;\;\;\;\;(k=1\sim N).
\end{align*}
$$

The eigenvalues $$\lambda$$ of $$A$$ are

$$
\begin{align*}
    \lambda 
    &= 2 - 2\cos\left(\frac{\pi}{N} k\right) \;\;\;\;\; (k = 1\sim N) \\
    &= 4\sin^2\left(\frac{\pi}{2N} k\right) \;\;\;\;\; (k = 1\sim N).
\end{align*}
$$