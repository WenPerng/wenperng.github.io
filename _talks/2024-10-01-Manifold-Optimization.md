---
layout: page
title: "Manifold Optimization"
description: "Continued on from matrix differentiation, this talk considers the matrix differentiation restricted onto a subset -- a matrix manifold. The techniques developed in this talk allow one to perform optimization algorithms on functions defined over constrained matrices."
img: /assets/img/talk/2024-10-01-manifold.png
venue: "Department of Electrical Engineering, National Taiwan University"
date: 2024-10-01
category: NTUEE SAAD
---

> Continued on from matrix differentiation, this talk considers the matrix differentiation restricted onto a subset -- a matrix manifold. The techniques developed in this talk allow one to perform optimization algorithms on functions defined over constrained matrices.

<iframe width="560" height="315" 
        src="https://www.youtube.com/embed/TuS7czodRsg?si=yOXqXPfMSaNbN3zE" 
        frameborder="0" 
        allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
        allowfullscreen>
</iframe>

# About the Talk

From principal component analysis (PCA) to diagonalizing a matrix via optimizing the Brockett function, manifold optimization is ubiquitous. In this talk, we especially focuses on the optimization over a *matrix manifold*.

Starting off with a recap of how to perform differentiation over a matrix in $$\mathbb{R}^{m\times n}$$ via *directional derivatives*, this motivates us in how to define the differentiation over a matrix in a general manifold $$\mathcal{M}$$.

But first, what is a manifold? As this is a talk given in an electrical engineering department, we simply view manifolds as a constrained set embedded in a larger Euclidean space. The usual symmetric matrices, skew-symmetric matrices, orthogonal matrices, and Stiefel manifold are all examples of matrix manifolds. The usual components to a manifold, such as its tangent space $$T_X\mathcal{M}$$ and geodesics $$\gamma_X(tH)$$ are also defined.

<br/><img src='/assets/img/talk/2024-10-01-manifold.png'>

Next, with geodesics defined, the directional derivatives is then introduced, bringing about the differential map over a function between manifolds:

$$
\frac{\partial^n f}{\partial X^n}[H] = \left.\frac{\mathrm{d}^n}{\mathrm{d}t^n} f(\gamma_X(tH))\right|_{t=0} .
$$

This is the pushforward map, often denoted in literatures as $$\mathrm{D}f$$ or $$f_{*}$$ instead of $$\partial f/\partial X$$. Via the *Riesz representation theorem*, the Riemannian gradient and Hessian are also defined as

$$
\frac{\partial f}{\partial X}[H] = \langle \mathrm{grad} f(X),H\rangle
$$

and

$$
\frac{\partial^2f}{\partial X^2}[H,K] = \langle \mathrm{Hess} f(X)[H],K\rangle,
$$

respectively.

With gradient and Hessian defined, one can perform descent algorithms such as gradient methods or Newton's methods on a loss function defined over a manifold. I give an example of applying the gradient descent on the Brockett function $$ f(X) = \mathrm{Tr} \{X^{\mathsf{T}}AXB \} $$ defined over the special orthogonal matrices. This special loss function allows us to diagonalize matrices via gradient descent.

# Slides

<embed src="/assets/slides/talks/2024_Manifold_Optimization.pdf" type="application/pdf" width="100%" height="600px" />

Download the [slides](/assets/slides/talks/2024_Manifold_Optimization.pdf).

More can be found [here](https://github.com/WenPerng/EESAAD_slides).

---
**About NTUEE SAAD Theoretical Talks**

The student academic association department (SAAD), NTUEE, is a student-run association under the electrical engineering department of National Taiwan University. It organizes events and courses such as this theoretical talk to bachelor students in the department.

The theoretical talks target at students with an interest in the more theoretical and mathematical aspects of engineering.