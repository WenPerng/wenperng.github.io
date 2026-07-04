---
layout: post
title: Discrete Hodge Decomposition
date: 2025-09-18
description: "This post discusses the discrete-equivalent of Hodge decomposition."
tags: math geometry
categories: differential-geometry
toc:
    sidebar: left
---

> This post discusses the discrete-equivalent of Hodge decomposition from the paper \"[Topological Signal Processing Over Simplicial Complexes](https://ieeexplore.ieee.org/document/9044758)\" by S. Barbarossa and S. Sardellitti.

This post continues introducing properties of graph Laplacians from the paper "[Topological Signal Processing Over Simplicial Complexes](https://ieeexplore.ieee.org/document/9044758)" by S. Barbarossa and S. Sardellitti. Note that the presentation below is highly non-rigorous.

In the [last post](/blog/2025/graph-Laplacian), we have introduced the definition of the graph Laplacian on signals over \\(k\\)-simplices via the incidence matrices:
<p>

$$
\boxed{
    L_k = B_k^{\mathsf{T}} B_k + B_{k+1} B_{k+1}^{\mathsf{T}}
}.
$$
</p>

This equation seems a bit hard to remember, but it is in fact really simple if you remember what the domain and range of \\(B _k\\) is. Denote all the signals over \\(k\\)-simplices as \\(\mathcal{S} _k\\) (it is a vector space). Then,
<p>

$$
\begin{aligned}
&B_k : \mathcal{S}_k \rightarrow \mathcal{S}_{k-1},\\
&L_k:\mathcal{S}_k \rightarrow \mathcal{S}_k.
\end{aligned}
$$
</p>

## Homology
We can construct the following chain \\(\mathcal{S}\\):
<p>

$$
\cdots\rightarrow \mathcal{S}_{k+1} \xrightarrow{B_{k+1}} \mathcal{S}_{k} \xrightarrow{B_{k}} \mathcal{S}_{k-1} \rightarrow \cdots,
$$
</p>
with
<p>

$$
\mathrm{im}(B_{k+1}) \subseteq \mathrm{ker}(B_{k})
$$
</p>
since \\(B _{k} B _{k+1} = 0\\).

## Hodge decomposition
This chain structure naturally admits a decomposition on any signal \\(s^k \in \mathcal{S} _k\\).
<p>

$$
\boxed{
    \mathcal{S}_k \cong \mathrm{im}(B_k^\mathsf{T}) \oplus \mathrm{ker}(L_k) \oplus \mathrm{im}(B_{k+1})
}.
$$
</p>

The derivation is as below: by utilizing the linear algebra identity
<p>

$$
\mathrm{ker}(A)^\perp = \mathrm{row}(A) = \mathrm{col}(A^\mathsf{T}) = \mathrm{im}(A^\mathsf{T}),
$$
</p>
we have
<p>

$$
\begin{align*}
    \mathcal{S}_k &= \mathrm{ker}(B_k) \oplus \mathrm{ker}(B_k)^\perp \\
    &= \mathrm{ker}(B_k) \oplus \mathrm{im}(B_k^\mathsf{T}) \\
    &= \mathrm{im}(B_{k+1}) \oplus \left(\mathrm{im}(B_{k+1})^\perp \cap \mathrm{ker}(B_k)\right) \oplus \mathrm{im}(B_k^\mathsf{T}) \\
    &\cong \mathrm{im}(B_{k+1}) \oplus \frac{\mathrm{ker}(B_k)}{\mathrm{im}(B_{k+1})} \oplus \mathrm{im}(B_k^\mathsf{T}) \\
    &= \mathrm{im}(B_{k+1}) \oplus H^k(\mathcal{S}) \oplus \mathrm{im}(B_k^\mathsf{T}),
\end{align*}
$$
</p>
where \\(H^k(\mathcal{S})\\) is the \\(k\\)th [homology](/posts/2025/09/blog-post-06/) of \\(\mathcal{S}\\). The isomorphism \\(\cong\\) is used as it implies the existence of a natural mapping between \\(H^k(\mathcal{S})\\) and \\(\mathrm{im}(B _{k+1})^\perp \cap \mathrm{ker}(B _k)\\).

Next, we need to connect the homology with the kernel of the Laplacian and show that they are isomorphic. Specifically, we want to establish
<p>

$$
\mathrm{ker}(B_k) = \mathrm{im}(B_{k+1}) \oplus \mathrm{ker}(L_k).
$$
</p>
This can be obtained by noticing that \\(\mathrm{im}(B _{k+1}) \perp \mathrm{im}(B _{k}^\mathsf{T})\\). Henceforth, there is NO such \\(s^k\\) that satisfies all \\(B _k s^k \neq 0\\), \\(B _{k+1}^\mathsf{T} s^k \neq 0\\), and \\(L_k s^k = 0\\).


The dimension of \\(\mathrm{ker}(L _k)\\) is known as the *Betti number* of order \\(k\\).

### Hodge decomposition of signals
For any signal \\(s^k \in \mathcal{S}_k\\), we can thus establish the following unique orthogonal decomposition of
<p>

$$
\boxed{
    s^k = B_{k}^{\mathsf{T}} s^{k-1} + s_{\mathrm{H}}^{k} + B_{k+1} s^{k+1},
}
$$
</p>
where \\(s^{k-1} \in \mathcal{S} _{k-1}\\), \\(s^{k} _{\mathrm{H}} \in \mathcal{S} _{k}\\), \\(s^{k+1} \in \mathcal{S} _{k+1}\\), and \\(L _k s^k _{\mathrm{H}} = 0\\).

The term \\(s^k _\mathrm{H}\\) satisfies the Laplace equation \\(L _k s^k _{\mathrm{H}} = 0\\). Henceforth, we term it the *harmonic component*.

### Example
The case in which we are most familiar with is \\(k=1\\). It has a lot of analogies with what we have learned in vector calculus. The space \\(\mathcal{S} _1\\) represents all the *edge* signals over a graph.

For edge signals over a graph, we can define the \\(\mathrm{curl}\\) and \\(\mathrm{div}\\) on them. They are defined respectively as
<p>

$$
\boxed{
\begin{align*}
    \mathrm{curl}(s^1) &= B_{2}^\mathsf{T} s^1, \\
    \mathrm{div}(s^1) &= B_{1} s^1.
\end{align*}
}
$$
</p>
Such definition matches our prior knowledge in vector calculus: the curl transforms a signal from edges to faces, while the divergence transforms a signal from edges to vertices.

By \\(B _1 B _2 = 0\\), we have
<p>

$$
\begin{align*}
    \mathrm{ker}(\mathrm{curl}) &= \mathrm{im}(B_1^{\mathsf{T}}), \\
    \mathrm{ker}(\mathrm{div}) &= \mathrm{im}(B_2).
\end{align*}
$$
</p>
Therefore,
<p>

$$
\mathcal{S}_1 = \mathrm{ker}(\mathrm{curl}) \oplus \mathrm{ker}(L_1) \oplus \mathrm{ker}(\mathrm{div}),
$$
</p>
it is an orthogonal decomposition into curl-less, harmonic, and divergence-less components:
<p>

$$
    s^1 = B_1^\mathsf{T}s^0 + s^1_\mathrm{H} + B_2 s^2.
$$
</p>
The term \\(B _1^\mathsf{T}s^0\\) is curl-less, it may be called an *irrotational* component, and can be viewed as the discrete gradient of \\(s^0\\). The harmonic component \\(s^1 _\mathrm{H}\\) is both curl-less and divergence-less. The term \\(B _2s^2\\) is divergence-less, it may be called a *solenoidal* component, and can be viewed as the curl of \\(s^2\\).

## Relation to differential geometry
The original Hodge theorem in differential geometry works with the cochain of differential forms over \\(\mathcal{M}\\)
<p>

$$
    \cdots \rightarrow \Omega^{k-1} \xrightarrow{\mathrm{d}_{k-1}} \Omega^k \xrightarrow{\mathrm{d}_{k}} \Omega^{k+1} \rightarrow \cdots
$$
</p>
instead.

Given the differential operator \\(\mathrm{d}\\), we define its adjoint operator as \\(\delta_{k+1} = \mathrm{d}_{k} ^ \*\\). The Laplacian is defined accordingly:
<p>

$$
    \Delta_k = \mathrm{d}_{k-1}\delta_{k} + \delta_{k+1}\mathrm{d}_{k} = \mathrm{d}\delta + \delta\mathrm{d}.
$$
</p>

The Hodge decomposition goes like
<p>

$$
    \Omega^k \cong \mathrm{im}(\delta_{k+1}) \oplus \mathrm{ker}(\Delta_k) \oplus \mathrm{im}(\mathrm{d}_{k-1}).
$$
</p>

The dimension of \\(\mathrm{ker}(\Delta _k)\\) is the \\(k\\)th *Betti number* of the manifold \\(\mathcal{M}\\). It is a topological invariance.