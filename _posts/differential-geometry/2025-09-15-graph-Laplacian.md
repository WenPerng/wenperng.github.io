---
layout: post
title: Graph Laplacian
date: 2025-09-15
description: "This is a series of posts on connecting techniques of differential geometry and signal processing over graphs. This post specifically addresses the notion of differential operator over graphs and graph Laplacians."
tags: math geometry
categories: differential-geometry
toc:
    sidebar: left
---

> This is a series of posts on connecting techniques of differential geometry and signal processing over graphs. This post specifically addresses the notion of differential operator over graphs and graph Laplacians. For more details, one can refer to the paper "[Topological Signal Processing Over Simplicial Complexes](https://ieeexplore.ieee.org/document/9044758)" by S. Barbarossa and S. Sardellitti.

In the [previous post](/blog/2025/graph-simplex), we addressed the basic notations to simplices over graphs.
This second post of the series

## Incidence matrix
Next, we consider signals on the simplices. A signal on \\(k\\)-simplices is denoted by \\(s^k\\). Assume there are \\(n\\) \\(k\\)-simplices, then \\(s^k \in \mathbb{C}^{n\times1}\\).

Next, let us introduce the incidence matrix \\(B_k\\) operating on signals on \\(k\\)-simplices, mapping them to signals on \\((k-1)\\)-simplices. The incidence matrix operates as the *boundary* operation, mapping \\(k\\)-chains to \\((k-1)\\)-chains.

Consider the one-hot vector \\(\boldsymbol{1} _{\sigma^k _i}\\) representing the \\(i\\)th \\(k\\)-simplex, we want
<p>

$$
B_k \boldsymbol{1}_{\sigma^k_i} = \boldsymbol{1}_{\partial_k\sigma^k_i}.
$$
</p>

Formally, the entries to \\(B_k\\) are defined as
<p>

$$
\boxed{
    [B_k]_{ij} = \begin{cases}
        +1, & \sigma^{k-1}_i \subset \sigma^k_j \text{ and } \sigma^{k-1}_i \sim \sigma^k_j \\
        -1, & \sigma^{k-1}_i \subset \sigma^k_j \text{ and } \sigma^{k-1}_i \not\sim \sigma^k_j \\
        0, & \sigma^{k-1}_i \not\subset \sigma^k_j.
    \end{cases}
}
$$
</p>

From the [property](/posts/2025/09/blog-post-14/) of the boundary operation, we have that
<p>

$$
B_{k-1} B_{k} = 0.
$$
</p>

The incidence matrix represents the *adjacency* information between the simplices.

## Graph Laplacian
The combinatorial Laplacian matrix acting on signals over \\(k\\)-simplices is defined as
<p>

$$
\boxed{
    L_k = B_k^{\mathsf{T}} B_k + B_{k+1} B_{k+1}^{\mathsf{T}}
}.
$$
</p>
The first component \\(B _k^{\mathsf{T}} B _k\\) is the *lower Laplacian*, representing the *lower adjacency*; while the latter component \\(B _{k+1} B _{k+1}^{\mathsf{T}}\\) is the *upper Laplacian*, representing the *upper adjacency*.

I will postpone the discussion as to why it is defined so until I can present an easy to understand explanation. But for the mean time, I am simply surprised by the elegance and simplicity of the representation, as it greatly mirrors its differential geometrical counterpart -- the Laplace--Beltrami operator.

---
With the Laplacian, one can perform Fourier transform on the signals by a coordinate transform with respect to the eigenbasis of the Laplacian.

Moreover, the Hodge decomposition of differential forms may also be introduced. For a thorough discussion, however, some knowledge on differential geometry is required. So I guess I will postpone the related discussion to the far future.

---
I decided to learn about topological signal processing as I was preparing for the [talk on Fourier transform](https://wenperng.github.io/talks/2025-05-15-talk). This is such an interesting topic, but I have to find some applications to it so as to push myself in learning it.