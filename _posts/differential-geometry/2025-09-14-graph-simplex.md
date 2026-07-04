---
layout: post
title: Simplices in Graphs
date: 2025-09-14
description: "This is the start of posts on connecting techniques of differential geometry and signal processing over graphs. This post specifically addresses the notion of simplex in graphs."
tags: math geometry
categories: differential-geometry
toc:
    sidebar: left
---


> This is the start of posts on connecting techniques of differential geometry and signal processing over graphs. This post specifically addresses the notion of simplex in graphs. For more details, one can refer to the paper "[Topological Signal Processing Over Simplicial Complexes](https://ieeexplore.ieee.org/document/9044758)" by S. Barbarossa and S. Sardellitti.

This first post of the series starts off by introducing the geometric primitives over graphs -- a \\(k\\)-simplex.

## Simplex
A graph contains a finite collection of points \\(V = \\\{v _0,\ldots,v _{N-1}\\\}\\). These points are also called *vertices*.

<br/><img src='/assets/img/blog/2025-09-14-simplex.png' width="60%">

- A \\(k\\)-simplex, denoted by \\(\sigma^k _i\\) is an *unordered* set \\(\\\{v _{i _0}, \ldots, v _{i _{k}}\\\}\\) of \\(k+1\\) vertices.

- A simplicial complex \\(\mathcal{X}\\) is a finite collection of simplices that is closed under inclusion of faces. I.e. if \\(\sigma^k \in \mathcal{X}\\), then its faces \\(\sigma^{k-1} \in \mathcal{X}\\).

- An *oriented* \\(k\\)-simplex is an *ordered* set \\([v _{i _0}, \ldots, v _{i _{k}}]\\) of \\(k+1\\) vertices.

- A face of a simplex \\(\sigma^k\\) is denoted by \\(\sigma^{k-1} _j \subset \sigma^k\\) with \\(j\in[0:k]\\). It is obtained by the removal of a vertex within \\(\sigma^k\\).

- A face of an oriented simplex inherits an orientation by
<p>

$$
\sigma^{k-1}_j = (-1)^j [v_{i_0}, \ldots, v_{i_{j-1}}, v_{i_{j+1}}, \ldots, v_{i_k}].
$$
</p>

- We say that the face obtained by the sign above is coherent, denoted by \\(\sigma^{k-1} _{j} \sim \sigma^k\\).

Note that the notion of "directed" and "oriented" are different. The establishment of orientation over a simplex allows "signals" on it to be denoted as positive or negative. Whereas directed signals on the graph restrict the values to be either positive or negative, but not both. In topological signal processing, one considers oriented and undirected simplices.

## Boundary
The boundary of a \\(k\\)-simplex is a \\((k-1)\\)-chain, i.e., an integer combination of \\((k-1)\\)-simplices. It is defined as
<p>

$$
\partial_k \sigma^k = \sum_{j=0}^{k} (-1)^j [v_{i_0}, \ldots, v_{i_{j-1}}, v_{i_{j+1}}, \ldots, v_{i_k}].
$$
</p>

From the above formulation, one can immediately see that the boundary operation forms a homology as \\(\partial _{k-1}\partial _k = 0\\).

<br/><img src='/assets/img/blog/2025-09-14-boundary.png' width="70%">

---
By building our language of topological signal processing from the simplices, one can immediately smell how differential geometry comes into play.