---
layout: post
title: Notes on (Anti-)Derivations over Forms
date: 2025-09-04
description: "This is my notes on \"Introduction to Manifolds\" by Loring Tu -- especially on the Lie derivatives of forms."
tags: math
categories: differential-geometry
toc:
    sidebar: left
---

> This is my notes on "[Introduction to Manifolds](https://link.springer.com/book/10.1007/978-1-4419-7400-6)" by Loring Tu -- especially on the Lie derivatives of forms.

## Forms
For some vector space \\(V\\), the set of all \\(k\\)-covectors (also known as the alternating \\(k\\)-tensors) are denoted by
<p>

$$ A_k(V) \text{ or } \Lambda^k(V^*),$$
</p>
where \\(V^\*\\) is the dual space of \\(V\\).

A \\(k\\)-covector *field* over a manifold \\(\mathcal{M}\\) is called a (differential) \\(k\\)-form.

For the \\(k\\)th exterior power of the cotangent bundle
<p>

$$\Lambda^k(T^*\mathcal{M}) = \bigcup_{p\in\mathcal{M}} \Lambda^k(T^*_p\mathcal{M}),$$
</p>
we have it as a vector bundle \\(\pi:\Lambda^k(T^*\mathcal{M}) \rightarrow \mathcal{M}\\). A \\(k\\)-form is then a section of this bundle.

The vector space of all \\(C^{\infty}\\) \\(k\\)-forms are then denoted by
<p>

$$
\Omega^k(\mathcal{M}) = \Gamma(\mathcal{M}, \Lambda^k(T^*\mathcal{M})) = \Gamma(\Lambda^k(T^*\mathcal{M})).
$$
</p>
Note that the different meanings for \\(A^k\\), \\(\Lambda^k\\), \\(\Omega^k\\), and \\(\Gamma\\).

The language of bundles and sections are really interesting. Furthermore, by generalizing these relations via the language of category theory with functors, more cool stuff can be introduced in the future.

## Lie derivative
The Lie derivative is a derivation. Consider a \\(C^\infty\\) vector field \\(X\\) on \\(\mathcal{M}\\). Then we have an integral curve \\(\varphi_t:\mathcal{M}\rightarrow\mathcal{M}\\) induced by \\(X\\). The Lie derivative of another vector field \\(Y\\) by \\(X\\) is
<p>

$$
\mathcal{L}_X Y = \left.\frac{\mathrm{d}}{\mathrm{d}t}\right|_{t=0} \varphi_{-t*}(Y).
$$
</p>

This definition above is defined pointwise, basically meaning to use \\(\varphi_{-t*}\\) to push a the vector \\(Y_{\varphi_t(p)}\\) back to the point \\(p\\) and perform the derivative at \\(p\\).

This definition can be extend to forms. Since
<p>

$$\omega(F_*X) = \langle \omega, F_* X\rangle = \langle (F_*)^*\omega,X\rangle = \langle F^*\omega, X\rangle = (F^*\omega)(X),$$
</p>
we have the adjoint map to the pushforward \\(F_\*\\) as the pullback \\((F_\*)^\*\\). For simplicity of notation, we write \\((F_\*)^\*\\) as \\(F^\*\\).

The Lie derivative on the \\(k\\)-form \\(\omega\\) will then be
<p>

$$
\mathcal{L}_X \omega = \left.\frac{\mathrm{d}}{\mathrm{d}t}\right|_{t=0} \varphi_t^*(\omega)
$$
</p>
The definition is again made pointwise.

From the above, we can see that the Lie derivative is essentially equivalent to a *time derivative*. This view point of the Lie derivative explains a lot of its properties.

## Cartan \\(\mathrm{d}\\)-operator and interior multiplication
The Cartan \\(\mathrm{d}\\)-operator and the interior multiplication (contraction) are both *anti-derivations* as for \\(\omega \in \Omega^k(\mathcal{M})\\) and \\(\tau\in\Omega^{\ell}(\mathcal{M})\\),
<p>

$$
\mathrm{d}(\omega \wedge \tau) = \mathrm{d}\omega \wedge \tau + (-1)^k \omega \wedge \mathrm{d}\tau
$$
</p>
and
<p>

$$
\iota_X(\omega \wedge \tau) = \iota_X\omega \wedge \tau + (-1)^k \omega \wedge \iota_X\tau.
$$
</p>

These two anti-derivations follows a skewed Leibniz rule and are of degree \\(+1\\) and \\(-1\\), respectively. I.e., \\(\mathrm{d}\omega\\) and \\(\iota_X\omega\\) have grade \\(k+1\\) and \\(k-1\\), respectively.

### Examples
Consider in a three-dimensional manifold and \\(\omega = f \mathrm{d}x^1 \wedge \mathrm{d}x^2\\). Represented using the tensor product, we have
<p>

$$\begin{aligned}
\omega(v_1,v_2) &= \frac{1}{1!\cdot 1!}\sum_{\sigma\in S_2} \mathrm{sgn}(\sigma) \,\mathrm{d}x^1\otimes\mathrm{d}x^2 (v_{\sigma(1)},v_{\sigma(2)}) \\
&= \left(\mathrm{d}x^1\otimes\mathrm{d}x^2 - \mathrm{d}x^2 \otimes \mathrm{d}x^1\right) (v_1,v_2).
\end{aligned}$$
</p>

Its exterior derivative will be
<p>

$$
\mathrm{d}\omega = \sum_{i}\partial_i f \,\mathrm{d}x^i \wedge \mathrm{d}x^1 \wedge \mathrm{d}x^2 = (-1)^2 \partial_3f \, \mathrm{d}x^1 \wedge \mathrm{d}x^2 \wedge \mathrm{d}x^3.
$$
</p>

The interior multiplication will be
<p>

$$
\iota_X\omega = \omega(X,\cdot) = \mathrm{d}x^1(X) \,\mathrm{d}x^2 - \mathrm{d}x^2(X) \, \mathrm{d}x^1.
$$
</p>

## Properties of Lie derivative
The first property is that
- The Lie derivative is a derivation.

This means that the Lie derivative satisfies the Leibniz rule. This is also easily verifiable as the Lie derivative is simply a time derivative.

The second property is
- \\(\mathcal{L}_X\\) and \\(\mathrm{d}\\) commutes.

Again, since the Lie derivative is essentially a time derivative, it commutes with the exterior derivative \\(\mathrm{d}\\).

The third property is:
- Cartan homotopy formula: \\(\mathcal{L}_X = \mathrm{d}\iota _X + \iota _X \mathrm{d}\\).

This can be proven by first noting that both sides are derivations. Then if the formula works for \\(\omega\\) and \\(\tau\\), then it also works for \\(\mathrm{d}\omega\\) and \\(\omega\wedge\tau\\). Hence we only need to verify the formula for \\(\omega = f\in C^\infty(\mathcal{M})\\) which is trivial.

The fourth property is:
- For vector fields \\(X\\) and \\(Y\\), we have \\(\mathcal{L}_XY = [X,Y]\\).

The last property is the "product" rule:
- We have, for \\(k\\)-form \\(\omega\\),
<p>

$$
\mathcal{L}_{X}\left(\omega(Y_1,\ldots,Y_k)\right) = (\mathcal{L}_X\omega)(Y_1,\ldots,Y_k) + \sum_{i=1}^{k} \omega(Y_1,\ldots,\mathcal{L}_XY_i,\ldots,Y_k).
$$
</p>