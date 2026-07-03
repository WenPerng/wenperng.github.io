---
layout: page
title: "Matrix Differentiation"
description: "This talk is a revamped description of how we can perform differentiation over functions on matrices, with an example of backpropagation over MLP given."
img: 
venue: "Department of Electrical Engineering, National Taiwan University"
date: 2024-09-18
category: NTUEE SAAD
---

> This talk is a revamped description of how we can perform differentiation over functions on matrices, with an example of backpropagation over MLP given.

<iframe width="560" height="315" 
        src="https://www.youtube.com/embed/YNsgjUQE2q4?si=YoVAeJaWhZxTHo03" 
        frameborder="0" 
        allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
        allowfullscreen>
</iframe>

# About the Talk

Again, this talk starts off from the notion of treating derivatives as a linear operator mapping the changes in the variable to the first-order changes in the function (Fréchet Derivative).

A more rigorous definition to finding matrix derivatives via *directional derivatives* is given. This definition is crucial in leading to manifold optimization, which is the next talk. Furthermore, it also justified the form of a differentiation of a scalar function by a matrix, which was glossed over in its introduction from the previous talk on matrix differentiation in 2023.

Drawing inspiration from the Taylor expansion, the gradient and Hessian are also rigorously defined. They are treated, again, as an operator defined so with respect to an inner product. Usually, the Euclidean inner product is assumed.

Examples of applications of matrix differentiation are given near the end of the talk. As a taste of freshness, I demonstrate how backpropagation is used in the training of a multi-layer perceptron (MLP). This also motivates the need for ResNet, to combat against the diminishing of gradient.

<br/><img src='/assets/img/talk/2024-09-18-MLP.png'>

# Slides

<embed src="/assets/slides/talks/2024_Matrix_Differentiation.pdf" type="application/pdf" width="100%" height="600px" />

Download the [slides](/assets/slides/talks/2024_Matrix_Differentiation.pdf).

More can be found [here](https://github.com/WenPerng/EESAAD_slides).

---
**About NTUEE SAAD Theoretical Talks**

The student academic association department (SAAD), NTUEE, is a student-run association under the electrical engineering department of National Taiwan University. It organizes events and courses such as this theoretical talk to bachelor students in the department.

The theoretical talks target at students with an interest in the more theoretical and mathematical aspects of engineering.