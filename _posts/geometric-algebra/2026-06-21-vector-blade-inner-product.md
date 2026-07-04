---
layout: post
title: Inner Product of Vectors and Blades
date: 2026-06-21
description: "This post provides a proof to the identity of the inner product between a vector and an r-grade blade."
tags: math
categories: geometric-algebra
toc:
    sidebar: left
---

> This post provides a proof to the identity of the inner product between a vector and an \\(r\\)-grade blade.


This post provides a proof to the important identity

$$
\boxed{
    \boldsymbol{v} \cdot (\boldsymbol{a}_1 \wedge \cdots \wedge \boldsymbol{a}_r) = \sum_{i=1}^{r} (-1)^{i-1} (\boldsymbol{v} \cdot \boldsymbol{a}_i) (\boldsymbol{a}_1 \wedge \cdots \wedge \breve{\boldsymbol{a}}_i \wedge \cdots \wedge \boldsymbol{a}_r)
}.
$$

I came up this proof by myself, though [other authors](https://share.google/RIXUCf9pVHoTmJhhp) have given a cleaner proof using grade projections. Before we go over the proof, let us see some application of this identity.

## Examples
For vectors $$\boldsymbol{a}$$, $$\boldsymbol{b}$$, $$\boldsymbol{c}$$, and $$\boldsymbol{d}$$, we immediately have

$$
\begin{align*}
    \boldsymbol{a} \cdot (\boldsymbol{b} \wedge \boldsymbol{c}) &= (\boldsymbol{a} \cdot \boldsymbol{b}) \boldsymbol{c} - (\boldsymbol{a} \cdot \boldsymbol{c}) \boldsymbol{b}, \\
    \boldsymbol{a} \cdot (\boldsymbol{b} \wedge \boldsymbol{c} \wedge \boldsymbol{d}) &= (\boldsymbol{a} \cdot \boldsymbol{b}) (\boldsymbol{c} \wedge \boldsymbol{d}) - (\boldsymbol{a} \cdot \boldsymbol{c}) (\boldsymbol{b} \wedge \boldsymbol{d}) + (\boldsymbol{a} \cdot \boldsymbol{d}) (\boldsymbol{b} \wedge \boldsymbol{c}).
\end{align*}
$$

The first one is actually just the familiar vector triple product in disguise:

$$
\boldsymbol{a} \times (\boldsymbol{b} \times \boldsymbol{c}) = (\boldsymbol{a} \cdot \boldsymbol{b}) \boldsymbol{c} - (\boldsymbol{a} \cdot \boldsymbol{c}) \boldsymbol{b}.
$$

This can be easily shown by noting that we have

$$
\boldsymbol{a} \times \boldsymbol{b} := -(\boldsymbol{a} \wedge \boldsymbol{b})I
$$

and the duality relation

$$
(\boldsymbol{a} \cdot \boldsymbol{b}) I = \boldsymbol{a} \wedge (\boldsymbol{b}I),
$$

where $$I$$ is the pseudoscalar in $$\mathbb{R}^3$$, satisfying $$I^2 = -1$$.

## The Proof
First, we consider an orthonormal basis $$\{\boldsymbol{e}_i\}$$ satisfying

$$
V := \mathrm{span}\{\boldsymbol{a}_{i}\}_{i=1}^{r} = \mathrm{span}\{\boldsymbol{e}_{i}\}_{i=1}^{r}.
$$

Let $$\boldsymbol{v} = \boldsymbol{v}_{\perp} + \sum_{i=1}^{r} v_{i} \boldsymbol{e}_{i}$$, where $$\boldsymbol{v}_{\perp} \perp V$$. Let the $$r$$-blade be $$A_{r} := \boldsymbol{e}_{1} \wedge \cdots \wedge \boldsymbol{e}_{r} = \boldsymbol{e}_{1} \cdots \boldsymbol{e}_{r}$$. Then,

$$
\begin{align*}
    \boldsymbol{v} \cdot A_{r} &= \left\langle \boldsymbol{v} A_{r} \right\rangle_{r-1} \\
    &= \left\langle \boldsymbol{v}_{\perp} A_{r} + \sum_{i=1}^{r} v_{i} \boldsymbol{e}_{i} A_r \right\rangle_{r-1}.
\end{align*}
$$

The first term vanishes since it is of grade $$r+1$$. Thus,

$$
\begin{align*}
    \boldsymbol{v} \cdot (\boldsymbol{e}_{1} \cdots \boldsymbol{e}_{r}) &= \sum_{i=1}^{r} v_{i} \boldsymbol{e}_{i} (\boldsymbol{e}_{1} \cdots \boldsymbol{e}_{r}) \\
    &= \sum_{i=1}^{r} (\boldsymbol{v} \cdot \boldsymbol{e}_i) (-1)^{i-1} (\boldsymbol{e}_{1}\cdots \breve{\boldsymbol{e}}_{i} \cdots \boldsymbol{e}_{r}).
\end{align*}
$$

Next, let us turn to the RHS of the target equation. We can expand the blade term as

$$
\begin{align*}
    &\boldsymbol{a}_1 \wedge \cdots \wedge \breve{\boldsymbol{a}}_i \wedge \cdots \wedge \boldsymbol{a}_r \\
    &= \left(\sum_{j_{1} = 1}^{r} a_{1j_{1}} \boldsymbol{e}_{j_1}\right) \wedge \cdots \wedge \breve{\left(\sum_{j_{i} = 1}^{r} a_{ij_{i}} \boldsymbol{e}_{j_i}\right)} \wedge \cdots \left(\sum_{j_{r} = 1}^{r} a_{rj_{r}} \boldsymbol{e}_{j_r}\right) \\
    &= \sum_{j_1,\ldots,j_r} (a_{1j_1} \cdots \breve{a}_{ij_i} \cdots a_{rj_r})(\boldsymbol{e}_{j_1} \cdots \breve{\boldsymbol{e}}_{j_i} \cdots \boldsymbol{e}_{j_r}) \\
    &= \sum_{j_1,\ldots,j_r} (a_{1j_1} \cdots \breve{a}_{ij_i} \cdots a_{rj_r}) \epsilon^{j_1\ldots j_r}_{1\ldots r}(\boldsymbol{e}_{1} \cdots \breve{\boldsymbol{e}}_{j_i} \cdots \boldsymbol{e}_{r}) \\
    &= \sum_{j_i = 1}^{r} (-1)^{j_i-1} \det(M_{ij_i}) (\boldsymbol{e}_{1} \cdots \breve{\boldsymbol{e}}_{j_i} \cdots \boldsymbol{e}_{r}),
\end{align*}
$$

where $$\epsilon_{1\ldots r}^{j_1\ldots j_r}$$ is the Levi-Civita symbol and $$M_{ij}$$ is the $$(i,j)$$-minor of the matrix $$a_{ij}$$. Plug this back into the RHS of our target equation,

$$
\begin{align*}
    \mathrm{RHS} &= \sum_{i=1}^{r} (-1)^{i-1} (\boldsymbol{v} \cdot \boldsymbol{a}_i) \sum_{j = 1}^{r} (-1)^{j-1} \det(M_{ij}) (\boldsymbol{e}_{1} \cdots \breve{\boldsymbol{e}}_{j} \cdots \boldsymbol{e}_{r}) \\
    &= \sum_{i,j=1}^{r} (-1)^{i-1} \left(\sum_{k=1}^{r} a_{ik} \boldsymbol{v} \cdot \boldsymbol{e}_k\right) (-1)^{j-1} \det(M_{ij}) (\boldsymbol{e}_{1} \cdots \breve{\boldsymbol{e}}_{j} \cdots \boldsymbol{e}_{r}) \\
    &= \sum_{j,k=1}^{r} \left(\sum_{k=1}^{r}(-1)^{i-1} a_{ik} \det(M_{ij}) \right) (-1)^{j-1} (\boldsymbol{v} \cdot \boldsymbol{e}_k) (\boldsymbol{e}_{1} \cdots \breve{\boldsymbol{e}}_{j} \cdots \boldsymbol{e}_{r}) \\
    &= \sum_{j,k=1}^{r} (-1)^{j-1} \left(\det(a_{ij}) \delta_{kj}\right) (\boldsymbol{v} \cdot \boldsymbol{e}_k) (\boldsymbol{e}_{1} \cdots \breve{\boldsymbol{e}}_{j} \cdots \boldsymbol{e}_{r}) \\
    &= \det(a_{ij}) \sum_{j=1}^{r} (-1)^{j-1} (\boldsymbol{v} \cdot \boldsymbol{e}_j) (\boldsymbol{e}_{1} \cdots \breve{\boldsymbol{e}}_{j} \cdots \boldsymbol{e}_{r}).
\end{align*}
$$

By the relation we have earlier proven, we finally obtain the identity:

$$
\begin{align*}
    \mathrm{RHS} &= \det(a_{ij}) \boldsymbol{v} \cdot (\boldsymbol{e}_1 \cdots \boldsymbol{e}_{r}) \\
    &= \boldsymbol{v} \cdot (\boldsymbol{a}_1 \wedge \cdots \wedge \boldsymbol{a}_r) = \mathrm{LHS}.
    \;\;\;\;\; \blacksquare
\end{align*}
$$

---
## Conclusions
Although this theorem seems obvious if you interpret it as finding the component of the blade along the direction of \\(\boldsymbol{v}\\), while keeping the anti-commutativity of the wedge product in mind, it is not at all trivial.

In the [notes](https://wenperng.github.io/projects/2023-09-GA-note) to the previous geometric algebra study group I have held, we have actually never proven this identity, but instead treated it as true. Finally, after almost three years, I came back and filled in the gaps.