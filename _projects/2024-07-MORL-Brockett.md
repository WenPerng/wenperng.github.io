---
layout: page
title: "Newton's Method on Brockett Function"
description: "My exploration into the numerics of applying Newton's method on the Brockett function."
img: /assets/img/projects/basin.gif
date: 2024-07-03
category: Notes
---

During the course \"Manifold Optimisation for Representation Learning\" given in the summer of 2024 by Prof. [Hao Shen](https://scholar.google.com/citations?user=Kce9W-8AAAAJ&hl=en) and [Julian Wörmann](https://scholar.google.com/citations?hl=de&user=aqG8AJcAAAAJ&view_op=list_works&sortby=pubdate) at TUM, I was especially interested in the numerics of the optimization of the Brockett function

$$
\begin{equation*}
    f(X) = \frac{1}{2}\mathrm{Tr}\{X^{\mathsf{T}}AXB\}
\end{equation*}
$$

defined over orthogonal matrices $$X\in\mathrm{O}(m)$$ given arbitrary positive definite matrices $$A$$ and $$B$$.

The optimization of the Brockett function to find its maxima or minima has a lot of applications. One of which that fascinates me the most is to use it to diagonalize a Hermitian matrix. There are plenty of methods to perform the optimization as well, this note specifically focuses on using the Riemannian Newton's method.

In finding the Riemannian Newton's step, one is required to obtain the Riemannian gradient, the Riemannian Hessian, and the inverse to the Riemannian Hessian in closed forms. Though no closed form can be found for the inverse of the Riemannian Hessian in simple terms, one can devise plenty numerical methods to obtain it. Two are to be noted:
- using matrix vectorization and the Kronecker product, proposed by myself during the course, and
- using matrix pseudo-inverse, proposed by the two lecturers.
I gave a small talk on the derivation and code implementation of the Newton's method during the class.

# Code
The MATLAB code realization of the methods proposed in the note below can be found [here](https://github.com/WenPerng/Matrix-Manifold-Optimization/blob/2403ea8817ef1a797c1d728e0bd3807bd8fa625c/newtonLike.m).

# Note
The note to my small talk can be downloaded [here](/assets/pdf/projects/2024_MORL_Brockett.pdf).
<embed src="/assets/pdf/projects/2024_MORL_Brockett.pdf" type="application/pdf" width="100%" height="600px" />

Some open problems on the computational side remains. For example, whether the answer obtained by the different methods coincide. Though they most certainly seem to be the same, I have yet come up with a clean proof of it.

# Further Explorations
See the file [here](/assets/pdfs/projects/2024_Exploiting_Basins_of_Attraction_for_Newton_s_Method_on_Brockett_Function_Maximization.pdf).