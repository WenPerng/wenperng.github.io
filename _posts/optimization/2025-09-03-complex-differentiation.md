---
layout: post
title: "Complex Gradient Descent and Lagrange Multipliers"
date: 2025-09-03
description: "This post applies the complex vector differentiation in the discussion to gradient descent algorithm for unconstrained optimization. I also discuss the corresponding Lagrange multiplier formalism for constrained optimization."
tags: math
categories: optimization
toc:
    sidebar: left
---

> This post applies the complex vector differentiation in the discussion to gradient descent algorithm for unconstrained optimization. I also discuss the corresponding Lagrange multiplier formalism for constrained optimization.

Before we start, we need to establish what complex vector differentiation is.

This can be seen as a continuation to the matrix differentiation I introduced in one of my [talks](/talks/2024-09-18-talk) in NTUEE into complex matrices. I elaborate on how one can differentiate with respect to complex vectors.

We will be considering scalar functions of complex variables: \\(g = g(z_1,\ldots,z_n,z_1^\*,\ldots,z_n^\*) \in \mathbb{C}\\), where \\(z_k\in\mathbb{C}\\). But first let us vectorize the complex variables: I use bold symbols to denote vectors and let \\(\boldsymbol{z} = [z_1,\ldots,z_n]^{\mathsf{T}}\\), then
<p>
$$
\boldsymbol{u} = \left[\begin{matrix}
  \boldsymbol{z} \\ \boldsymbol{z}^*
\end{matrix}\right] = \left[\begin{matrix}
  \boldsymbol{x} + \mathrm{i} \boldsymbol{y} \\ \boldsymbol{x} - \mathrm{i} \boldsymbol{y}
\end{matrix}\right] = \left[\begin{matrix}
	\mathbb{I}_n & \mathrm{i}\,\mathbb{I}_n \\ \mathbb{I}_n &-\mathrm{i}\,\mathbb{I}_n
\end{matrix}\right] \left[\begin{matrix}
  \boldsymbol{x} \\ \boldsymbol{y}
\end{matrix}\right] = D \boldsymbol{v},
$$
</p>
where \\(\boldsymbol{x}\\) and \\(\boldsymbol{y}\\) are real vectors of size \\(n\times1\\). The matrix \\(D\\) satisfies
<p>
$$DD^{\mathsf{H}} = 2\mathbb{I}_{2n}.$$
</p>
For a function \\(g(\boldsymbol{u})\\), we denote its realized version as \\(f\\):
<p>
$$g(\boldsymbol{u}) = f(\boldsymbol{v}).$$
</p>

## Complex Vector Differentiation
As we have already discussed the nuance to real vector differentiation, we can immediately borrow the results from there and extend to complex vector differentiation.

Again, the notation I used is partial differentiation \\(\partial / \partial \boldsymbol{u}\\) instead of the directional derivative \\(\mathrm{D}_{\boldsymbol{u}}\\).

First thing first, differentiation: since we require that
<p>
$$\begin{align*}
	\frac{\partial g}{\partial \boldsymbol{u}} [\mathrm{d}\boldsymbol{u}] &= \frac{\partial f}{\partial \boldsymbol{v}} [\mathrm{d}\boldsymbol{v}] \\
	&= \frac{\partial f}{\partial \boldsymbol{v}} [D^{-1}\mathrm{d}\boldsymbol{u}],
\end{align*}$$
</p>
we can rewrite in operator notation that
<p>
$$\boxed{
	\begin{aligned}
		\frac{\partial g}{\partial \boldsymbol{u}} &= \frac{\partial f}{\partial \boldsymbol{v}} \circ D^{-1} \\
		\frac{\partial f}{\partial \boldsymbol{v}} &= \frac{\partial g}{\partial \boldsymbol{u}} \circ D
	\end{aligned}
}.$$
</p>

Furthermore, by treating covectors as row vectors we can denote
<p>
$$
\frac{\partial g}{\partial \boldsymbol{u}} = \left[\begin{matrix}
	\frac{\partial g}{\partial \boldsymbol{z}} & \frac{\partial g}{\partial \boldsymbol{z}^*}
\end{matrix}\right], \frac{\partial f}{\partial \boldsymbol{v}} = \left[\begin{matrix}
	\frac{\partial f}{\partial \boldsymbol{x}} & \frac{\partial f}{\partial \boldsymbol{y}}
\end{matrix}\right].
$$
</p>
Since
<p>
$$
D^{-1} = \left[\begin{matrix}
	\frac{1}{2} \mathbb{I}_n & \frac{1}{2} \mathbb{I}_n \\ -\frac{\mathrm{i}}{2} \mathbb{I}_n & \frac{\mathrm{i}}{2} \mathbb{I}_n
\end{matrix}\right]
$$
</p>
we also obtain the famous *Wirtinger derivatives*:
<p>
$$\boxed{
\begin{align*}
	\frac{\partial g}{\partial \boldsymbol{z}} &= \frac{1}{2}\left(\frac{\partial f}{\partial \boldsymbol{x}} - \mathrm{i} \frac{\partial f}{\partial \boldsymbol{y}}\right) \\
	\frac{\partial g}{\partial \boldsymbol{z}^*} &= \frac{1}{2}\left(\frac{\partial f}{\partial \boldsymbol{x}} + \mathrm{i} \frac{\partial f}{\partial \boldsymbol{y}}\right).
\end{align*}
}$$
</p>

This can equally be checked by noticing that: for \\(\mathrm{d}\boldsymbol{u} = D \mathrm{d}\boldsymbol{v}\\)
<p>
$$
\begin{align*}
	\mathrm{d}g &= \frac{\partial g}{\partial \boldsymbol{u}}[\mathrm{d}\boldsymbol{u}] \\
	&= \frac{\partial g}{\partial \boldsymbol{z}}[\mathrm{d}\boldsymbol{z}] + \frac{\partial g}{\partial \boldsymbol{z}^*}[\mathrm{d}\boldsymbol{z}^*] \\
	&= \frac{1}{2}\left(\frac{\partial f}{\partial \boldsymbol{x}} - \mathrm{i} \frac{\partial f}{\partial \boldsymbol{y}}\right) [\mathrm{d}\boldsymbol{z}] + \frac{1}{2}\left(\frac{\partial f}{\partial \boldsymbol{x}} + \mathrm{i} \frac{\partial f}{\partial \boldsymbol{y}}\right) [\mathrm{d}\boldsymbol{z}^*] \\
	&= \frac{\partial f}{\partial \boldsymbol{x}} \left[\frac{\mathrm{d}\boldsymbol{z} + \mathrm{d}\boldsymbol{z}^*}{2}\right] + \frac{\partial f}{\partial \boldsymbol{y}} \left[\frac{\mathrm{d}\boldsymbol{z} - \mathrm{d}\boldsymbol{z}^*}{2 \mathrm{i}}\right] \\
	&= \frac{\partial f}{\partial \boldsymbol{x}} [\mathrm{d}\boldsymbol{x}] + \frac{\partial f}{\partial \boldsymbol{y}} [\mathrm{d}\boldsymbol{y}] \\
	&= \frac{\partial f}{\partial \boldsymbol{v}}[\mathrm{d}\boldsymbol{v}] = \mathrm{d}f.
\end{align*}
$$
</p>

### Real functions and gradient
If the function \\(g\in\mathbb{C}\\), and the induced inner product is the usual complex Euclidean inner product \\(\langle \boldsymbol{a},\boldsymbol{b}\rangle = \boldsymbol{a}^{\mathsf{H}} \boldsymbol{b}\\) (also known as the Hermitian inner product), then the gradient of \\(g\\) with respect to \\(u\\) will be the column vector
<p>
$$
	\nabla_{\boldsymbol{u}} g(\boldsymbol{u}) = \left(\frac{\partial g}{\partial \boldsymbol{u}}\right)^{\mathsf{H}} = D^{-\mathsf{H}} \left(\frac{\partial f}{\partial \boldsymbol{v}}\right)^{\mathsf{T}} = \frac{1}{2} D \nabla_{\boldsymbol{v}} f(\boldsymbol{v})
$$
</p>

Moreover, in optimization, we often have \\(g\in\mathbb{R}\\), then we have
<p>
$$
\left(\frac{\partial g}{\partial \boldsymbol{z}^*}\right)^* = \frac{\partial g}{\partial \boldsymbol{z}}.
$$
</p>
By using the real inner product on \\(\boldsymbol{z}\\) as \\(\langle \boldsymbol{a},\boldsymbol{b}\rangle = 2\mathrm{Re}\\\{\boldsymbol{a}^{\mathsf{H}} \boldsymbol{b}\\\}\\), we can restrict our discussion only to the \\(\boldsymbol{z}\\)-part and neglect \\(\boldsymbol{z}^\*\\). We have the gradient in this case as
<p>
$$
\boxed{\begin{aligned}
	&\mathrm{d}g = 2 \mathrm{Re}\left\{ \frac{\partial g}{\partial \boldsymbol{z}} \mathrm{d}\boldsymbol{z}\right\} = \left\langle \nabla_{\boldsymbol{z}} g, \mathrm{d}\boldsymbol{z}\right\rangle \\
	&\Rightarrow  \nabla_{\boldsymbol{z}}g = \left(\frac{\partial g}{\partial \boldsymbol{z}}\right)^{\mathsf{H}} = \left(\frac{\partial g}{\partial \boldsymbol{z}^*}\right)^{\mathsf{T}}
\end{aligned}}.
$$
</p>

A gradient descent algorithm with respect to the inner product \\(\langle \boldsymbol{a},\boldsymbol{b}\rangle = 2\mathrm{Re}\\\{\boldsymbol{a}^{\mathsf{H}} \boldsymbol{b}\\\}\\) can be easily implemented as \\(\boldsymbol{z}_{i+1} = \boldsymbol{z} _{i} + \mu \nabla _{\boldsymbol{u}}g(\boldsymbol{u} _{i})\\). The computation is also going to be faster because the dimension of \\(\boldsymbol{z}\\) is half as that of \\(\boldsymbol{u}\\).

---
One may question the inclusion of \\(\boldsymbol{z}^\*\\) from the initial start, after all, isn't it dependent on \\(\boldsymbol{z}\\) completely? Indeed, the two complex variables are complex conjugates to each other. The need for the inclusion of the conjugate part is so that we can use the usual *matrix-vector multiplication linear algebra* in the analysis. If the conjugate part is not included, one need to additionally introduce a *complex conjugation operator* that will be quite a nuisance to work with.

## Hessians
Here we consider the Hermitian inner product. Consider the second-order differential with \\(\mathrm{d}\boldsymbol{u}_1 = D\mathrm{d}\boldsymbol{u}_1\\) and \\(\mathrm{d}\boldsymbol{u}_2 = D\mathrm{d}\boldsymbol{u}_2\\), we have the bilinear operator
<p>
$$
\begin{align*}
	\frac{\partial^2 f}{\partial \boldsymbol{v}^2} [\mathrm{d} \boldsymbol{v}_1, \mathrm{d} \boldsymbol{v}_2] &= \mathrm{d} \boldsymbol{v}_1^{\mathsf{T}} \frac{\partial^2 f}{\partial \boldsymbol{v}^{\mathsf{T}} \partial \boldsymbol{v}} \mathrm{d} \boldsymbol{v}_2 \\
	&= \mathrm{d} \boldsymbol{v}_1^{\mathsf{T}} \frac{\partial}{\partial \boldsymbol{v}^{\mathsf{T}}} \left( \frac{\partial g}{\partial \boldsymbol{u}} D \mathrm{d} \boldsymbol{v}_2 \right) \\
	&= \mathrm{d} \boldsymbol{v}_1^{\mathsf{T}} D^{\mathsf{H}} \frac{\partial g}{\partial \boldsymbol{u}^{\mathsf{H}} \partial \boldsymbol{u}} D \mathrm{d} \boldsymbol{v}_2 \\
	&= \mathrm{d} \boldsymbol{u}_1^{\mathsf{H}} \frac{\partial g}{\partial \boldsymbol{u}^{\mathsf{H}} \partial \boldsymbol{u}} \mathrm{d} \boldsymbol{u}_2 = \frac{\partial^2 g}{\partial \boldsymbol{u}^2} [\mathrm{d} \boldsymbol{u}_1, \mathrm{d} \boldsymbol{u}_2].
\end{align*}
$$
</p>
we can thus define the real and complex Hessians matrices as
<p>
$$\boxed{
H_{\mathbb{R}} = \frac{\partial^2 f}{\partial \boldsymbol{v}^{\mathsf{T}} \partial \boldsymbol{v}}, H_{\mathbb{C}} = \frac{\partial^2 g}{\partial \boldsymbol{u}^{\mathsf{H}} \partial \boldsymbol{u}}
},$$
</p>
with \\(H_{\mathbb{R}}^{\mathsf{T}} = H_{\mathbb{R}}\\), \\(H_{\mathbb{C}}^{\mathsf{H}} = H_{\mathbb{C}}\\), and 
<p>
$$H_\mathrm{R} = D^{\mathsf{H}} H_\mathbb{C} D.$$
</p>

Note that we can also write out the submatrices explicitly as (again under the complex Euclidean inner product):
<p>
$$
H_\mathbb{R} = \nabla_{\boldsymbol{v}^{\mathsf{T}}} \nabla_{\boldsymbol{v}} f = \left[\begin{matrix}
	\partial_{\boldsymbol{x}^{\mathsf{T}}} \partial_{\boldsymbol{x}} f & \partial_{\boldsymbol{x}^{\mathsf{T}}} \partial_{\boldsymbol{y}} f \\
	\partial_{\boldsymbol{y}^{\mathsf{T}}} \partial_{\boldsymbol{x}} f & \partial_{\boldsymbol{y}^{\mathsf{T}}} \partial_{\boldsymbol{y}} f
\end{matrix}\right]
$$
</p>
and
<p>
$$
H_\mathbb{C} = \nabla_{\boldsymbol{u}^{\mathsf{T}}} \nabla_{\boldsymbol{u}} g = \left[\begin{matrix}
	\partial_{\boldsymbol{z}^{\mathsf{H}}} \partial_{\boldsymbol{z}} f & \partial_{\boldsymbol{z}^{\mathsf{H}}} \partial_{\boldsymbol{z}^*} f \\
	\partial_{\boldsymbol{z}^{\mathsf{T}}} \partial_{\boldsymbol{z}} f & \partial_{\boldsymbol{z}^{\mathsf{T}}} \partial_{\boldsymbol{z}^*} f
\end{matrix}\right].
$$
</p>

### Taylor expansion
The Taylor expansion of a complex function \\(g\\) can then be written generally as
<p>
$$\begin{align*}
	g(\boldsymbol{u} + \mathrm{d}\boldsymbol{u}) &= g(\boldsymbol{u}) + \frac{\partial g(\boldsymbol{u})}{\partial \boldsymbol{u}} [\mathrm{d} \boldsymbol{u}] + \frac{1}{2} \frac{\partial^2 g(\boldsymbol{u})}{\partial^2 \boldsymbol{u}} [\mathrm{d} \boldsymbol{u}, \mathrm{d} \boldsymbol{u}] + O(\|\mathrm{d} \boldsymbol{u}^3\|) \\
	&= g(\boldsymbol{u}) + \langle \nabla_{\boldsymbol{u}}g(\boldsymbol{u}), \mathrm{d}\boldsymbol{u}\rangle + \frac{1}{2} \langle H_\mathbb{C}(\boldsymbol{u}) [\mathrm{d} \boldsymbol{u}], \mathrm{d} \boldsymbol{u} \rangle + O(\|\mathrm{d} \boldsymbol{u}^3\|),
\end{align*}$$
</p>
where \\(H_\mathbb{C}(\boldsymbol{u})\\) is the complex Hessian *operator* evaluated at \\(\boldsymbol{u}\\). The exact representation to each component depends on the inner product used.

---
It should be noted that I truly enjoy the operator notation instead of the matrix-vector product notation, as it implicitly implies one using the complex Euclidean inner product.

By lifting oneself to the operator-level, the exact inner product used is no longer relevant. In optimization, however, we introduced back in an inner product to "evaluate" the performance of the descent method. The gradient used can then be chosen according to this inner product. But it need not be.

---
Now, onto optimization!

Since we are dealing with optimization algorithms, let us consider the function to be optimize as \\(g(\boldsymbol{u})\in\mathbb{R} = f(\boldsymbol{v})\\) with \\(\boldsymbol{u}\in\mathbb{C}^{2n}\\) and \\(\boldsymbol{v}\in\mathbb{R}^{2n}\\). The notations used in this post continues from the last post.

## Gradient descent
Our goal is to establish a descent algorithm of the form
<p>
$$
    \boldsymbol{z}_{t+1} = \boldsymbol{z}_{t} - \mu \boldsymbol{d}_{t}.
$$
</p>
Given an inner product \\(\langle \cdot , \cdot \rangle\\) which we will specify later in examples, we can set the vector \\(\boldsymbol{d}_{t}\\) as satisfying
<p>
$$
    \frac{\partial g(\boldsymbol{u}_{t})}{\partial \boldsymbol{u}} [\mathrm{d} \boldsymbol{u}] = 2 \mathrm{Re}\left\{\frac{\partial g(\boldsymbol{u}_{t})}{\partial \boldsymbol{z}} [\mathrm{d} \boldsymbol{z}]\right\} = \langle \boldsymbol{d}_{t}, \mathrm{d} \boldsymbol{z}\rangle
$$
</p>
for all \\(\mathrm{d} \boldsymbol{u} = [\mathrm{d} \boldsymbol{z}; \mathrm{d} \boldsymbol{z}^\*] \in \mathbb{C}^{2n}\\). The vector \\(\boldsymbol{d}_{t}\\) obtained is the gradient associated with \\(\langle\cdot,\cdot\rangle\\).

The gradient vector can be extended to be \\(\overline{\boldsymbol{d}} _{t} = [\boldsymbol{d} _{t}; \boldsymbol{d} _t^\*]\\) acting on \\(\boldsymbol{u} _{t}\\).

### Performance analysis
For our discussion on the performance guarantees on the descent algorithm, it is required that we make some local assumptions on the optimizing function \\(g\\).

#### Assumptions on function
Let the norm associated with the given inner product \\(\langle\cdot,\cdot\rangle\\) be \\(\|\cdot\|\\). Note that it might no longer be the usual complex Euclidean norm.

The gradients are \\(\delta\\)-Lipschitz, i.e., let the gradient at \\(\boldsymbol{u}\\) be noted by \\(\boldsymbol{d}(\boldsymbol{u})\\), then
<p>
$$\boxed{
    \left\| \boldsymbol{d}(\boldsymbol{u}_1) - \boldsymbol{d}(\boldsymbol{u}_2) \right\| \le \delta \left\| \boldsymbol{u}_1 - \boldsymbol{u}_2 \right\|
}.
$$
</p>

Secondly, the function is assumed to be \\(\nu\\)-strongly convex, i.e., for all \\(\boldsymbol{u}\\) and \\(\boldsymbol{u}_0\\),
<p>

$$\boxed{
    g(\boldsymbol{u}) \ge g(\boldsymbol{u}_0) + \frac{\partial g(\boldsymbol{u}_0)}{\partial \boldsymbol{u}}[\boldsymbol{u} - \boldsymbol{u}_0] + \frac{\nu}{2} \|\boldsymbol{u} - \boldsymbol{u}_0 \|^2
}.
$$
</p>

#### Convergence
Firstly, note that
<p>
$$
\langle \boldsymbol{d}_{t}^*, \mathrm{d} \boldsymbol{z}^* \rangle= \langle \boldsymbol{d}_{t}, \mathrm{d} \boldsymbol{z} \rangle^* \Rightarrow \frac{\partial g(\boldsymbol{u}_{t})}{\partial \boldsymbol{u}}[\mathrm{d}\boldsymbol{u}] = \langle \overline{\boldsymbol{d}}_{t}, \mathrm{d}\boldsymbol{u}\rangle.
$$
</p>

Consider the unique minimizer to \\(g\\) as \\(\boldsymbol{u} _{\star} = [\boldsymbol{z} _{\star};\boldsymbol{z}^\* _{\star}]\\), then define the deviation from the minimizer as \\(\widetilde{\boldsymbol{u}} _{t} = \boldsymbol{u} _{\star} - \boldsymbol{u} _{t}\\). Let \\(\boldsymbol{d} _\star = 0\\) be the gradient at the minimizer, then the norm of the error is
<p>

$$
\begin{align*}
    \widetilde{\boldsymbol{u}}_{t+1} &= \widetilde{\boldsymbol{u}}_{t} + \mu \overline{\boldsymbol{d}}_{t} \\
    \Rightarrow \|\widetilde{\boldsymbol{u}}_{t+1}\|^2 &= \|\widetilde{\boldsymbol{u}}_{t}\|^2 + 2 \mu \langle \widetilde{\boldsymbol{u}}_{t}, \overline{\boldsymbol{d}}_{t}\rangle + \mu^2 \| \overline{\boldsymbol{d}_{t}} \|^2 \\
    &= \|\widetilde{\boldsymbol{u}}_{t}\|^2 + 2 \mu \frac{\partial g(\boldsymbol{u}_{t})}{\partial \boldsymbol{u}}[\widetilde{\boldsymbol{u}}_{t}] + \mu^2 \| \overline{\boldsymbol{d}}_{t} - \overline{\boldsymbol{d}}_{\star}\|^2 \\
    &\le \|\widetilde{\boldsymbol{u}}_{t}\|^2 + 2\mu \left(g(\boldsymbol{u}_{t}) - g(\boldsymbol{u}_{\star}) - \frac{\nu}{2}\|\widetilde{\boldsymbol{u}}_{t}\|^2\right) + \mu^2 \delta^2 \| \widetilde{\boldsymbol{u}}_{t}\|^2 \\
    &= (1 - \mu \nu + \mu^2\delta^2) \| \widetilde{\boldsymbol{u}}_{t}\|^2 + 2\mu \left(g(\boldsymbol{u}_t) - g(\boldsymbol{u}_{\star})\right) \\
    &\le (1 - \mu \nu + \mu^2\delta^2) \| \widetilde{\boldsymbol{u}}_{t}\|^2 + 2\mu \left( - \frac{\nu}{2} \|\widetilde{\boldsymbol{u}_{t}}\|^2\right) \\
    &\le (1 - 2 \mu \nu + \mu^2\delta^2) \| \widetilde{\boldsymbol{u}}_{t}\|^2.
\end{align*}
$$
</p>

If we choose a step-size \\(\mu\\) such that
<p>
$$\boxed{
    1 - 2 \mu \nu + \mu^2\delta^2 \in [0,1)
},$$
</p>
we hence obtain the convergence of the gradient descent algorithm.

Note that since \\(\delta \ge \nu > 0\\), we can obtain the simpler criterion of \\(\mu \in (0,2\nu/\delta^2)\\).

### Example
I will show that the two inner products introduced in the last post ensures convergence of the gradient descent algorithm.

#### Hermitian inner product over \\(\mathbb{C}^{2n}\\)
The inner product used is
<p>
$$\langle \boldsymbol{u}_1, \boldsymbol{u}_2\rangle = \boldsymbol{u}_1^{\mathsf{H}} \boldsymbol{u}_2,$$
</p>
the associated norm is simply the usual norm of a complex vector. Henceforth, the two assumptions on Lipschitz gradient and strong-convexity are reasonable. The gradient descent is then
<p>
$$
\boldsymbol{u}_{t+1} = \boldsymbol{u}_{t} - \mu \left(\frac{\partial g(\boldsymbol{u}_{t})}{\partial \boldsymbol{u}}\right)^{\mathsf{H}}.
$$
</p>

#### Real inner product over \\(\mathbb{C}^{n}\\)
The inner product used is
<p>
$$\langle \boldsymbol{z}_1, \boldsymbol{z}_2\rangle = 2 \mathrm{Re}\\\{\boldsymbol{z}_1^{\mathsf{H}} \boldsymbol{z}_2\\\},$$
</p>
restricted on \\(\mathbb{C}^{n}\\) instead of \\(\mathbb{C}^{2n}\\) as in the previous example.

Note that since for \\(\boldsymbol{u} _1 = [\boldsymbol{z} _1; \boldsymbol{z} _1^\*]\\) and \\(\boldsymbol{u} _2 = [\boldsymbol{z} _2; \boldsymbol{z} _2^\*]\\),
<p>
$$
    \boldsymbol{u}_1^{\mathsf{H}} \boldsymbol{u}_2 = \boldsymbol{z}_1^{\mathsf{H}} \boldsymbol{z}_2 + \boldsymbol{z}_1^{\mathsf{T}} \boldsymbol{z}_2^* = 2 \mathrm{Re}\{\boldsymbol{z}_1^{\mathsf{H}} \boldsymbol{z}_2\}.
$$
</p>
Henceforth, we see that the real inner product over \\(\boldsymbol{z}\in\mathbb{C}^{n}\\) is equivalent in operation to the Hermitian inner product over \\(\boldsymbol{u} \in \mathbb{C}^{2n}\\). The gradient descent is then
<p>
$$
\boldsymbol{z}_{t+1} = \boldsymbol{z}_{t} - \mu \left(\frac{\partial g(\boldsymbol{u}_{t})}{\partial \boldsymbol{z}}\right)^{\mathsf{H}}.
$$
</p>

## Lagrange multipliers
As we have seen above, by using the real inner product over \\(\boldsymbol{z}\\), we can restrict our discussions to half the dimension as that of \\(\boldsymbol{u}\\). This is quite favorable, and I shall work in this fashion from now on if possible.

The method of Lagrange multiplier is used to find extrema over differentiable constrained sets. Consider optimizing a real function \\(g(\boldsymbol{u})\\) over the constrained set \\(\boldsymbol{h}(\boldsymbol{u}) = \boldsymbol{0}\\). Note that \\(\boldsymbol{h}\\) is a vector constraint.

This problem can be solved by considering the Lagrangian
<p>
$$
\boxed{
    \mathcal{L} = g(\boldsymbol{u}) + \mathrm{Re} \left\{\boldsymbol{\lambda}^{\mathsf{H}} \boldsymbol{h}(\boldsymbol{u})\right\}
}
$$
</p>
with Lagrange multiplier vector \\(\boldsymbol{\lambda}\\), the optima should satisfy both \\(\boldsymbol{h}(\boldsymbol{u}) = \boldsymbol{0}\\) and
<p>

$$
\boxed{
    \frac{\partial \mathcal{L}}{\partial \boldsymbol{z}} = \boldsymbol{0}
}.
$$
</p>

Note how the differentiation is with respect to \\(\boldsymbol{z}\\) only!

### Proving the method
I'll obtain the complex form above from the method of Lagrange multipliers for real functions. Let us separate the real and imaginary parts of the terms: \\(\boldsymbol{\lambda} = \boldsymbol{\lambda} _1 + \mathrm{i} \boldsymbol{\lambda} _2\\) and \\(\boldsymbol{h}(\boldsymbol{u}) = \boldsymbol{h} _1(\boldsymbol{u}) + \mathrm{i} \boldsymbol{h} _2(\boldsymbol{u}) = \boldsymbol{k} _1(\boldsymbol{v}) + \mathrm{i} \boldsymbol{k} _2(\boldsymbol{v})\\). Then the Lagrangian construction given above is equivalent to its real counterpart:
<p>

$$
\begin{align*}
    \mathcal{L} &= g(\boldsymbol{u}) + \boldsymbol{\lambda}_1^{\mathsf{T}} \boldsymbol{h}_1(\boldsymbol{u}) + \boldsymbol{\lambda}_2^{\mathsf{T}} \boldsymbol{h}_2(\boldsymbol{u}) \\
    &= f(\boldsymbol{v}) + \boldsymbol{\lambda}_1^{\mathsf{T}} \boldsymbol{k}_1(\boldsymbol{v}) + \boldsymbol{\lambda}_2^{\mathsf{T}} \boldsymbol{k}_2(\boldsymbol{v}).
\end{align*}
$$
</p>

The optimality condition requires that
<p>

$$
\begin{align*}
    &\frac{\partial\mathcal{L}}{\partial \boldsymbol{v}} = \boldsymbol{0} = \left[\begin{matrix}
        \frac{\partial\mathcal{L}}{\partial \boldsymbol{x}} & \frac{\partial\mathcal{L}}{\partial \boldsymbol{y}}
    \end{matrix}\right] \\
    &\Rightarrow \frac{\partial\mathcal{L}}{\partial \boldsymbol{x}} = \frac{\partial\mathcal{L}}{\partial \boldsymbol{y}} = \boldsymbol{0} \\
    &\Rightarrow \frac{\partial\mathcal{L}}{\partial \boldsymbol{z}} = \frac{1}{2} \left(\frac{\partial\mathcal{L}}{\partial \boldsymbol{x}} - \mathrm{i} \frac{\partial\mathcal{L}}{\partial \boldsymbol{y}}\right) = \boldsymbol{0}. \;\;\;\;\;\blacksquare
\end{align*}
$$
</p>
Thus the validity of the formulation in the box above is verified.