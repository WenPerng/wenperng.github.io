---
layout: post
title: Cohomology
date: 2025-09-06
description: "Some notes on cochain complexes cohomology lest I forget the details."
tags: math
categories: differential-geometry
toc:
    sidebar: left
---

> Some notes on cochain complexes cohomology lest I forget the details.

## Homology
Consider a chain of simplexes \\(\mathcal{S}\\) containing elements of dimension \\(n\\) denoted by \\(S_n\\), \\(n\in\mathbb{N}\cup\\\{0\\\}\\). The boundary operation \\(\partial_n\\) acts as
<p>

$$
\cdots \leftarrow S_{n-1} \xleftarrow{\partial_{n}} S_{n} \xleftarrow{\partial_{n+1}} S_{n+1} \leftarrow \cdots
$$
</p>
on this chain complex of simplexes as taking the boundary decreases the dimension by 1. The boundary operation satisfies \\(\partial_{n} \circ \partial_{n+1} = 0\\).

This is not necessary an exact sequence since \\(\mathrm{ker}\partial_{n} \neq \mathrm{im} \partial_{n+1}\\). The measurement of the discrepancy between the top sequence with an exact sequence is measured by the quotient between the kernel and the image. The \\(n\\)-th homology of the sequence is denoted by
<p>

$$
H_n(\mathcal{S}) = \frac{\mathrm{ker}(\partial_n)}{\mathrm{im}(\partial_{n+1})}.
$$
</p>
Furthermore, the elements in \\(\mathrm{ker}(\partial_n) \subseteq S_n\\) are *cycles*, we hence denote the set of \\(n\\)-cycles as \\(Z_n(\mathcal{S}) = \mathrm{ker}(\partial_n)\\). The letter "z" is chosen because of the german word for cycle which is "Zyklus". Similarly, the elements \\(\mathrm{im}(\partial_{n+1}) \subseteq S_n\\) are *boundaries*, we hence denote the set of \\(n\\)-boundaries as \\(B_n(\mathcal{S}) = \mathrm{im}(\partial_{n+1})\\).


## Cohomology
The directions in the *co*homology is opposite to that of the homology. Consider the cochain complex \\(\mathcal{A}\\) of, for example, \\(n\\)-forms \\(A^n\\) with differential \\(d_n\\) defined as
<p>

$$
\cdots \rightarrow A^{n-1} \xrightarrow{d_{n-1}} A^n \xrightarrow{d_n} A^{n+1} \rightarrow \cdots.
$$
</p>
The differential operators increase the degree of the forms by 1 when acted on. They satisfy the relation: \\(d_{n} \circ d_{n-1} = 0\\).

Similarly, we have the \\(n\\)-cocycles defined as \\(Z^n(\mathcal{A}) = \mathrm{ker}(d_{n})\\). The \\(n\\)-coboundaries are defined as \\(B^n(\mathcal{A}) = \mathrm{im}(d_{n-1})\\). The \\(n\\)-th cohomology thus represent the deviation of this sequence from an exact sequence by the quotient
<p>

$$
H^{n}(\mathcal{A}) = \frac{Z^n(\mathcal{A})}{B^n(\mathcal{A})} = \frac{\mathrm{ker}(d_n)}{\mathrm{im}(d_{n-1})}.
$$
</p>
