<!---
layout: post
title: Poset and Möbius Inversion
date: 2026-07-29
description: "This post presents the theory of Möbius inversion in its full glory via the language of posets."
# thumbnail: assets/img/blog/2026-07-22-permutation-torus1-square.png
tags: combinatorics
categories: random-math
toc:
    sidebar: left
--->

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
k^\pi &= k_1^{r_1} \cdot \ldots \cdot k_n^{r_n}.
\end{aligned}
$$

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

A partially ordered set is a lattice



## Möbius Inversion


## Convolution and Fourier Transform