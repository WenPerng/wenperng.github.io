---
layout: page
title: "Fourier Transform: Distributions and Generalizations"
description: "What is Fourier transform? Besides the usual Fourier transform defined over the reals and the integers, this talks introduces the notion of Fourier transform over groups, fields, and graphs. Further, a slight taste of distribution theory is provided to make our usual applications of Fourier transform in engineering mathematics more rigorous."
img: 
venue: "Department of Electrical Engineering, National Taiwan University"
date: 2025-05-15
category: NTUEE SAAD
---

> What is Fourier transform? Besides the usual Fourier transform defined over the reals and the integers, this talks introduces the notion of Fourier transform over groups, fields, and graphs. Further, a slight taste of distribution theory is provided to make our usual applications of Fourier transform in engineering mathematics more rigorous. 

<iframe width="560" height="315" 
        src="https://www.youtube.com/embed/Jql1E0A5E70?si=SLalWjerNVz1oSwb" 
        frameborder="0" 
        allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
        allowfullscreen>
</iframe>

# About the Talk

The usual Fourier transforms introduced in the course *Signals and Systems* are those defined over $$\mathbb{R}$$ (CTFT), $$\mathbb{T}$$ (CTFS), $$\mathbb{Z}$$ (DTFT), and $$[N]$$ (DTFS), with the first one written as

$$
\hat{f}(k) = \int_{-\infty}^{\infty} f(x) \mathrm{e}^{-\mathrm{i} 2\pi kx} \mathrm{d}x .
$$

In essence, the Fourier transform is just a unitary transformation between two sets of orthogonal coordinates. This viewpoint of the Fourier transform is emphasized.

Then, as a taste of the mathematics that is to come, we give an introduction to the matrix representation of DTFS and its two-dimensional variant -- the Fourier transform of an image. The multi-dimensional Fourier transform, on the other hand, leads to the famous Fourier slice theorem that is used in the mathematics of a CT scan.

<br/><img src='/assets/img/talk/2025-05-15-Fourier-slice.png'>

Next, we dig into the basics of distribution theory, justifying terms and equations such as the delta distribution or the Fourier transform of $$1$$:

$$
\delta(k) = \int_{-\infty}^{\infty} 1 \cdot \mathrm{e}^{-\mathrm{i} 2\pi kx} \mathrm{d}x.
$$

The integral above is really an abuse of notation, as the integral on the right-hand side does not converge in the usual sense of Riemann integrals.

The last section is on the other variants of Fourier transform. The topics included are what I have met during my bachelor studies. The first one is on the Fourier transform over prime fields, also known as the number theoretic transform (NTT). NTT is crucial in providing fast polynomial multiplication without floating point error. The second one is the Fourier transform over graphs. As informations can lie on a general undirected graph instead of a grid, we need graph Fourier transform (GFT) to decompose signals over a graph into different frequency components. This section reinforces the idea that the Fourier transform is a coordinate transformation between orthogonal frames. The last one is Fourier transform over abelian groups. This section is aimed to give a new perspective on the duality between CTFS and DTFT. Near the end, we give a hint at the Fourier transform over general groups via representation theory.

<br/><img src='/assets/img/talk/2025-05-15-GFT.png' width="70%">

All in all, the topics related to Fourier transform is not only ubiquitous in engineering but also deep in mathematics. This is my favorite aspect of engineering.

# Slides

<embed src="/assets/slides/talks/2025_Fourier_Transform.pdf" type="application/pdf" width="100%" height="600px" />

Download the [slides](/assets/slides/talks/2025_Fourier_Transform.pdf).

More can be found [here](https://github.com/WenPerng/EESAAD_slides).

---
**About NTUEE SAAD Theoretical Talks**

The student academic association department (SAAD), NTUEE, is a student-run association under the electrical engineering department of National Taiwan University. It organizes events and courses such as this theoretical talk to bachelor students in the department.

The theoretical talks target at students with an interest in the more theoretical and mathematical aspects of engineering.