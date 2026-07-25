---
layout: post
title: Poset and Möbius Inversion
date: 2026-07-25
description: "This post presents the theory of Möbius inversion in its full glory via the language of posets."
# thumbnail: assets/img/blog/2026-07-22-permutation-torus1-square.png
tags: combinatorics
categories: random-math
toc:
    sidebar: left
---

> I have never really enjoyed combinatorics. Compared to geometry or linear algebra, the results in combinatorics always seem to be pulled out of thin air. I can prove that the results are correct, yet, I can never derive them from an obvious and intuitive point of view. Recently, with the [blog post](/blog/2026/counting-permutation-cycles/) relating cycles in permutations with the Euler characteristics of their embeddings, I have finally found a link from basic geometry to combinatorics! This post is similar, where we have linked linear algebra to combinatorics. These allow for systematic ways to study results from combinatorics.

## What is the Möbius Inversion?
### Partitions
While reading through the book "Free Probability and Random Matrices" by J. A. Mingo and R. Speicher, I was introduced to the following relations in Chapter 1:

$$
\boxed{
\begin{aligned}
    \alpha_n &= \sum_{\pi \in \mathcal{P}(n)} k^\pi \\
    \Leftrightarrow k_n &= \sum_{\pi \in \mathcal{P}(n)} (-1)^{\#(\pi)-1} \left(\#(\pi) - 1\right)!\cdot \alpha^\pi
\end{aligned}
},
$$

where $$\alpha_n$$ and $$k_n$$ are respectively the $$n$$th moment and cumulant of a distribution, $$\mathcal{P}(n)$$ is the set of all partitions of $$n$$ elements. We say a partition $$\pi \in \mathcal{P}(n)$$ is of type $$(r_1,r_2,\ldots,r_n)$$ if it has $$r_i$$ blocks of size $$i$$. Then,

$$
\begin{aligned}
\alpha^\pi &= \alpha_1^{r_1} \cdot \ldots \cdot \alpha_n^{r_n}, \\
k^\pi &= k_1^{r_1} \cdot \ldots \cdot k_n^{r_n},
\end{aligned}
$$

and $$\#(\pi) = r_1 + \cdots + r_n$$.

Obviously, the formula for $$k_n$$ is far more complicated then that of $$\alpha_n$$. Yet, the difference seems to be merely of a different coefficient in the summands.

The relation of $$k_n$$ is called the ***Möbius inversion*** of the relation of $$\alpha_n$$. This not only appears here in the summation over partitions, but also in many other areas.

### Set Functions
In the [course note](https://wenperng.github.io/projects/2025-06-MCTT-note/) to "Modern Coding Theory and Technology", I have provided an alternate proof to the MacWilliams' identity by utilizing the following relations on set functions $$f$$ and $$g$$:

$$
\boxed{
\begin{aligned}
    g(S) &= \sum_{T \subseteq S} f(T) \\
    \Leftrightarrow f(S) &= \sum_{T \subseteq S} (-1)^{|S| - |T|} \cdot g(T)
\end{aligned}
}.
$$

This is the principle of inclusion-exclusion pivotal in combinatorics.

Interestingly, these relations on the summation over subsets is quite similar in their structures to the relations on the summation over partitions we have just introduced. In fact, they are also called the ***Möbius inversion***. This was my first experience with Möbius inversion. But wait, there are more examples besides these two!

### Number Theory
In number theory, we denote $$a|b$$ if the integer $$a$$ divides the integer $$b$$, i.e., there exists an integer $$n$$ such that $$b = na$$.

The Möbius inversion formula is a relation between pairs of arithmetic functions (functions defined on integers) $$f$$ and $$g$$

$$
\boxed{
\begin{aligned}
    g(n) &= \sum_{d|n} f(d) \\
    \Leftrightarrow f(n) &= \sum_{d|n} \mu(d) \cdot g\left(\frac{n}{d}\right)
\end{aligned}
}
$$

for integers $$n\ge1$$, where $$\mu(n)$$ is the ***Möbius function*** defined by:

$$
\mu(n) = \begin{cases}
    1, &n = 1; \\
    0, &n \text{ is divisble by a square}; \\
    (-1)^k, &n \text{ is the product of } k \text{distinct primes}.
\end{cases}
$$


### GSP over DAGs
This example of the Möbius inversion comes from the paper "[Orthogonal Fourier Analysis on Directed Acyclic Graphs via Möbius Total Variation](https://ieeexplore.ieee.org/document/11145920)" by Vedran Mihal and Markus Püschel. I came across this work during my time at ICASSP 2026.

This work comes up with an orthogonal basis for Fourier transform and graph signal processing (GSP) on directed acyclic graphs (DAGs). Normally for undirected graph, we have the Laplacian matrix as symmetric and invertible, resulting in the graph Fourier basis simply be the eigenbasis of the Laplacian matrix. However, things break down for DAGs.

The author of this work came up with the detour of defining the graph Fourier basis as the eigenbasis of $$M^\mathsf{T}M$$, where $$M$$ is the difference (differentiation) operator over the DAG. This is in direct parallel to the definition of the Laplacian via the incidence matrix. To obtain the difference matrix, we can define it to be the inverse to the integration matrix $$Z$$ defined via

$$
(Z \boldsymbol{x})_i = \sum_{v_j \preceq v_i} x_j,
$$

where $$\boldsymbol{x}$$ is a signal over the DAG and $$v_j \preceq v_i$$ means that the node $$v_j$$ is a predecessor of $$v_i$$. The matrix $$Z$$ is termed the Zeta matrix.

Then, we have

$$
M_{ij} = \begin{cases}
1, & i=j; \\
-\sum_{v_j \preceq v_k \prec v_i} M_{kj}, & \text{otherwise}.
\end{cases}
$$

The matrix $$M$$ is termed the Möbius matrix.

This example actually demonstrates quite vividly what the Möbius inversion is about. But no worries if things are still clear for you (I was in the same state as well), the next few sections will clarify the concepts.

---
---
Can I, someone whose brain is not hardwired to spot the inverse relation out of thin air, be able to derive these relations by myself? This is the motivation for writing this post, and I hope you who read this can also find this subject enlightening.

We begin our journey by introducing the language of poset and incidence algebra. Then, the Möbius inversion is introduced as the inverse matrix to an upper triangular matrix. We use what we learned to systematically derive the Möbius inversion relation of the above examples. Lastly, some links between our discussions and the properties of Fourier transform are raised.

## Poset
All the examples above can be explained elegantly in a unified fashion using the language and theory of ***incidence algebra*** and ***partially ordered sets***, or simply, ***posets***.

The following discussions mainly follows the foundational work "[On the Foundations of Combinatorial Theory: I. Theory of Möbius Functions](https://webhomes.maths.ed.ac.uk/~v1ranick/papers/rota1.pdf)" by Gian-Carlo Rosa in 1964.

A partially ordered set $$(P,\preceq)$$ is a lattice $$P$$ with a partial ordering $$\preceq$$. A partial ordering satisfies reflection ($$a\preceq a$$), antisymmetry (if $$a\preceq b$$ and $$b\preceq a$$ then $$a = b$$), and transitivity (if $$a\preceq b$$ and $$b \preceq c$$ then $$a\preceq c$$). We say that $$b$$ is ***coarser*** than $$a$$ or that $$a$$ is ***finer*** than $$b$$ if $$a\preceq b$$.

Another notation for $$a \preceq b$$ is $$b \succeq a$$. If the ordering is strict, i.e. $$a \neq b$$, then we have $$a \prec b$$ and $$b \succ a$$.

To illustrate, I believe the figure below on the subset poset (formally known as the ***Boolean algebra of all subsets of a finite set***) is enough, where we write $$T\preceq S$$ iff $$T\subseteq S$$.

<br/><img src='/assets/img/blog/2026-07-24-subset-lattice.png' width="100%">

Similarly, we can have the partitioning poset where $$\pi \preceq \sigma$$ if the blocks of $$\pi$$ are all contained in the blocks of $$\sigma$$, the division poset where $$d\preceq n$$ if $$d \vert n$$, and the DAGs poset which we have already defined.

For any two elements $$a$$ and $$b$$ in the lattice, we can define their join $$a\vee b$$ as the finest element that is coarser than both $$a$$ and $$b$$. Similarly, we define their meet $$a\wedge b$$ as the coarsest element that is finer than both $$a$$ and $$b$$.

Looking it at this way, we can see that all these problems we have listed above are enumerations over posets:

$$\sum_{a \preceq b} (\ldots).$$

### Greatest, least, maximal, and minimal element
Before we go on, some extremal values to the poset needs to be defined.

1. The greatest element in a poset $$P$$ is the unique element that is coarser than all elements in $$P$$.

2. The least element in a poset $$P$$ is the unique element that is finer than all elements in $$P$$.

In the example of the Boolean algebra of all subsets of $$\{1,2,3,4\}$$, the greatest element is $$\{1,2,3,4\}$$ and the least element is $$\varnothing$$. However, sometimes they might not exist.

3. An element $$m \in P$$ is maximal if there is no other element $$a \in P$$ such that $$a\succ m$$.

3. An element $$m \in P$$ is minimal if there is no other element $$a \in P$$ such that $$a\prec m$$.

Note that maximal and minimal elements can be more than one.

## Möbius Inversion
The Möbius Inversion is, in essence, equivalent to the "Fundamental Theorem of Calculus." We introduce here two functions, the Zeta function and the Möbius function, they are to each other the same as the integration to the differentiation.

Before further discussions, we must discuss the ***convolution*** operation: Consider real-valued functions of two variables $$f$$ and $$g$$ over the poset $$(P,\preceq)$$, we restrict $$f(x,y)=g(x,y)=0$$ for all $$x\not\preceq y$$. We define the convolution of $$f$$ and $$g$$ as

$$
\boxed{
    (f*g)(x,y) = \sum_{x \preceq z \preceq y} f(x,z) g(z,y)
}.
$$

These functions and the convolution operation form the ***incidence algebra*** of this poset over the reals. This algebra has the Kronecker delta $$\delta(x,y)$$ as its identity:
$$
(f*\delta)(x,y) = \sum_{x \preceq z \preceq y} f(x,z) \delta(z,y) = f(x,y).
$$

### Zeta Function
The ***zeta function*** $$\zeta(x,y)$$ is an element in the incidence algebra defined as

$$
\boxed{
    \zeta(x,y) = \begin{cases}
        1, &x \preceq y; \\
        0, &\text{else}.
    \end{cases}
}
$$

Any enumerative sum over the poset that we have seen thus far can be rewritten using the incidence algebra and the zeta function as

$$
g(y) = \sum_{x \preceq y} f(x) = \sum_{x \in P} f(x) \zeta(x,y).
$$

With an abuse of notation, we write $$g = f * \zeta$$.

> ##### NOTE
> Why is the operation $$*$$ defined above called convolution? It looks nothing like the convolution we have over $$\mathbb{R}$$, $$\mathbb{T}$$, $$\mathbb{Z}$$, or $$\mathbb{Z}_N$$.
>
> If we consider the poset of $$(P,\preceq) = (\mathbb{R},\le)$$, with elements in the incidence algebra be translational invariant $$f(x,y) = f(y-x)$$. Then the convolution becomes
> 
> $$
> (f*g)(x) := (f*g)(0,x) = \sum_{y} f(0,y) g(y,x) = \sum_{y} f(y) g(y-x).
> $$
> 
> This is exactly the convolution operation. Note that we have remove the constraint on the algebra that $$f(x,y) = 0$$ for $$x \le y$$. Nevertheless, this still forms an algebra.
{: .block-warning}

### Möbius Function
We define the inverse to the zeta function as the Möbius function $$\mu(x,y)$$ such that

$$
\zeta * \mu = \mu * \zeta = \delta.
$$

Therefore, the Möbius inversion formula simply states that

$$
f(y) = \sum_{x \preceq y} g(x) \mu(x,y).
$$

Naively, we see this as an immediate consequence to the definition of $$\mu$$:

$$
f = g * \mu = (f * \zeta) * \mu = f * (\zeta * \mu) = f * \delta = \delta.
$$

However, we have yet shown the invertibility of $$\zeta$$ and the associativity of $$*$$. We will not derive these properties in a rigorous fashion, instead, I will give a more linear-algebraic point of view that makes these results seem trivial.

### Linear algebraic point of view
We can visualize $$\zeta$$ as a matrix, with its elements indexed by $$\zeta(x,y)$$ with $$x$$, $$y\in P$$. Immediately by its definition, we see that $$\zeta$$ is an ***upper-triangular matrix*** with $$1$$ on its diagonal: 

$$\begin{aligned}
&\hspace{2.5cm}\;y\\
&\hspace{2.5cm}\downarrow\\
\zeta &= \left[\begin{matrix}
1 & * & * & *\\
& 1 & \boxed{*} & *\\
& & \ddots &* \\
& & & 1
\end{matrix}\right] \begin{matrix}\\ \leftarrow x\\ \\ \\\end{matrix}.
\end{aligned}
$$

The boxed element is $$\zeta(x,y)$$ with $$x \preceq y$$.

Since $$\zeta$$ has determinant $$1$$, it is invertible, and its inverse $$\mu$$ is also an upper-triangular matrix! This is a classic result from linear algebra. From this matrix notation, we also see that convolution is simply matrix multiplication, therefore it is associative.

Furthermore, if we assume that there is a least element $$0 \in P$$, then we can justify our abuse of notation of $$g = f * \zeta$$ and $$f = g * \mu$$ seen earlier via our incidence algebra:

$$\boxed{
\begin{aligned}
g(y) &:= g(0,y) = \sum_{0 \preceq x \preceq y} f(x) \zeta(x,y), \\
f(y) &:= f(0,y) = \sum_{0 \preceq x \preceq y} f(x) \mu(x,y).
\end{aligned}
}
$$

### Inversion relation
There are two ways to calculate the inverse of the zeta matrix. 

The first is in a recurrence fashion. Since the main relation defining $$\mu$$ is

$$
\sum_{x \preceq z \preceq y} \mu(x,z) = \sum_{x \preceq z \preceq y} \mu(x,z) \zeta(z,y) = \begin{cases}
1, &x=y ; \\
0, &x\prec y,
\end{cases}
$$

we can isolate the term $$z = y$$ to obtain

$$
\boxed{
    \mu(x,y) = - \sum_{x \preceq z \prec y} \mu(x,z)
}.
$$

Then, using the initial condition $$\mu(x,x) = 1$$, we will be able to iteratively derive all values to the Möbius function. Note that this is exactly the inversion formula seen in the [GSP over DAGs](/blog/2026/poset-moebius-inversion/#gsp-over-dags).

The second is by a power series method. Since the zeta is upper-triangular with $$1$$ on its diagonal. Therefore, we can define the ***incidence function*** as $$n(x,y) = \zeta(x,y) - \delta(x,y)$$, the corresponding incidence matrix is nilpotent! Immediately, we have that

$$
\boxed{
    \mu = \zeta^{-1} = (\delta + n)^{-1} = \delta - n + n^2 - n^3 + \cdots
}.
$$

The analytic formula to each element of $$\mu$$ can be obtained by interpreting physical meaning to the elements of $$n^k$$.

## Examples of Incidence Algebra
Let us see how the previous examples can be reframed in the language of incidence algebra.

### Boolean algebra
Given a set $$S$$, we define the poset $$(P,\preceq) = (2^S, \subseteq)$$. 

Here we give the Möbius function via the recurrence relation.

<details>
<summary>
The derivation of the Möbius inversion via the recurrence relation is simple.
</summary>

Consider a set $$T$$ and another set $$U_1$$ that is a singleton larger than $$T$$, the corresponding value of the Möbius function is

$$
\mu(T,U_1) = - \sum_{T \preceq U \prec U_1} \mu(T,U) = - \mu(T,T) = -1.
$$

Next for $$U_2$$ that is two elements larger than $$T$$, say $$U_2 = T \cup \{a,b\}$$, we have

$$
\mu(T,U_2) = - \sum_{T \preceq U \prec U_2} \mu(T,U) = - \mu(T,T\cup\{a\}) - \mu(T,T\cup\{b\}) - \mu(T,T)= 1.
$$

For $$U_3$$, we have

$$
\begin{aligned}
    \mu(T,U_3) &= - \sum_{T \preceq U \prec U_3} \mu(T,U) \\
    &= - \binom{3}{2} \mu(T,U_2) - \binom{3}{1} \mu(T,U_1) - \binom{3}{0}\mu(T,T) \\
    &= -3 + 3 - 1 = -1.
\end{aligned}
$$

Next, for $$U_k$$ that is $$k$$ elements larger than $$T$$, we see from the calculations above that the value is independent of the specific $$U_k$$ but instead only on $$k$$. In fact, we suspect it to be $$(-1)^k$$. Thus, by mathematical induction

$$
\begin{aligned}
\mu(T,U_k) &= - \binom{k}{k-1} \mu(T,U_{k-1}) - \binom{k}{k-2} \mu(T,U_{k-2}) - \cdots - \binom{k}{0} \mu(T,T) \\
&= -\sum_{\ell=0}^{k-1} \binom{k}{\ell} (-1)^\ell \\
&= - \left[\left(1 + (-1)\right)^k - (-1)^k\right] = (-1)^k.
\end{aligned}
$$

Hence, it is shown that

$$\mu(T,S) = (-1)^{|S| - |T|}. \;\;\;\;\;\blacksquare$$
</details>


<details>
<summary>
On the other hand, if one tries to use the power series expansion, the mathematics soon gets out of hand.
</summary>

The incidence function $$n(x,y) = 1$$ only if $$x \subset y$$. Then, the $$(x,y)$$th element of $$n^2$$ is equal to

$$
\begin{aligned}
    (n*n)(x,y) &= \sum_{x \subseteq z \subseteq y} n(x,z) n(y,z) \\
    &= \#\left\{z\, \middle\vert\, x\subset z \subset y\right\} \\
    &= \sum_{m=1}^{k-1} \binom{k}{m} \\
    &= 2^{k} - 2,
\end{aligned}
$$

where we let $$k = |y| - |x|$$ for brevity. The third equality can be easily seen as choosing to include $$m$$ elements in $$y\backslash x$$ with $$1 \le m \le k-1$$. Similarly, for $$n^\ell$$ with $$1 \le \ell \le k-1$$ (the nilpotency of $$n$$):

$$
\begin{aligned}
    (\underbrace{n*\ldots*n}_{\times \ell})(x,y) &= \#\left\{(z_1,\ldots,z_{\ell-1})\, \middle\vert\, x\subset z_1 \subset \cdots \subset z_{\ell-1} \subset y\right\} \\
    &= \sum_{m=\ell}^{k-1} \binom{k}{m} \cdot S(m,\ell-1) \cdot (\ell-1)!,
\end{aligned}
$$

where $$S(m,k)$$ is the Stirling number of the second kind, counting the number of ways to put $$m$$ different objects into $$k$$ unlabeled non-empty sets. It is defined by

$$
k! S(m,k) = \sum_{i=0}^{k} (-1)^{i} \binom{k}{i} (k-i)^m.
$$

Plug this back in, we have

$$
\begin{aligned}
(\underbrace{n*\ldots*n}_{\times \ell})(x,y) &= \sum_{m=\ell}^{k-1} \sum_{i=0}^{\ell-1} (-1)^{i} \binom{k}{m} \binom{\ell - 1}{i} (\ell - 1 -i)^m.
\end{aligned}
$$

What next? I don't know and I don't want to dig further down into this algebraic nonsense. Ask AI, that's gonna be way simpler and time efficient.
</details>

Obviously, one method is way simpler than the other. However, I do not have any method beyond intuition yet that can help us decide a priori which method to approach the inversion problem with. I do have a rule of thumb, and that is if the expressions for the convolutions of the incidence matrices get out of hand, try the other method instead.

### Partitions
Given $$n$$ elements, we consider the lattice $$P = \mathcal{P}(n)$$ as all the partitions of the elements equipped with the partial order $$\pi \preceq \sigma$$ such that the blocks of $$\pi$$ are contained in the blocks of $$\sigma$$. For example, for $$n=3$$, we have $$\{(12)(3)\} \preceq \{(123)\}$$, and $$\{(12)(3)\} \not\preceq \{(1)(23)\}$$.

For a partition $$\pi$$ of type $$\{r_1,\ldots,r_n\}$$, we previously defined the values $$\alpha^\pi$$ and $$k^\pi$$. Therefore, we have $$\alpha_n = \alpha^\sigma$$ and $$k_n = k^\sigma$$ where $$\sigma$$ is of type $$\{0,0,\ldots,r_n=1\}$$. It is now much more evident that $$\sigma$$ is the greatest element in the poset $$\mathcal{P}(n)$$. Hence, we have

$$
\alpha_n = \alpha^\sigma = \sum_{\pi \preceq \sigma} k^\pi = \sum_{\pi \in \mathcal{P}(n)} k^\pi.
$$

This is of the exact form of a enumeration over the poset with $$\zeta(\pi,\gamma) = 1$$ if $$\pi \preceq \gamma$$ and $$0$$ otherwise. We can utilize the Möbius inversion to find the inverse relation.

### Divisor algebra
We can let the lattice be $$P = \mathbb{N}$$ with $$d \preceq n$$ if $$d\vert n$$.

---
The proof to the Möbius function in each case can be found in the paper by Gian-Carlo Rosa mentioned above.
