---
layout: post
title: The Geometry of Cycles in Permutations
date: 2026-07-22
description: "This post discusses relation between the genus of the embedding space of a permutation and the number of cycles in the permutation."
tags: random matrices
categories: random-math
toc:
    sidebar: left
---

While reading through the book "Free Probability and Random Matrices" by J. A. Mingo and R. Speicher, it is in Chapter 1.7 that we want to discuss the moment

$$
\mathbb{E}[\mathrm{tr}\{X^{2k}\}],
$$

where $$X$$ is an $$N\times N$$ GUE (Gaussian unitary ensemble) and $$\mathrm{tr}\{\cdot\}$$ is the normalized trace.

The value of the moment above is

$$
\mathbb{E}[\mathrm{tr}\{X^{2k}\}] = \sum_{\pi \in \mathcal{P}_{2}(2k)} N^{\#(\gamma_{2k}\pi) - k - 1}= \sum_{\pi \in \mathcal{P}_{2}(2k)} N^{-2g_{\pi}}.
$$

The operator $$\#(\cdot)$$ returns the number of cycle in a permutation. The value $$g_{\pi}$$ is the ***genus*** of the permutation $$\pi$$ with respect to the one cycle $$\gamma_{2k} = (1,2,\ldots, 2k)$$. What does this mean?

This note is to give a geometric relation between "the genus of a permutation with respect to another permutation" with "the number of cycles of the product of the two permutations".

## Main Result
For any two transitive[^1] permutations $$\pi$$ and $$\gamma$$ over $$n$$ elements, the number of cycles in them satisfy the relation

[^1]: The two permutations $$\pi$$ and $$\gamma$$ are transitive if any element can reach any other element by applying $$\pi$$ or $$\gamma$$.

$$
\boxed{
    \#(\pi) + \#(\gamma) + \#(\gamma\pi) = n + 2 - 2 g
},
$$

where $$g$$ is the smallest genus of a surface that can embed the permutation $$\pi$$ with respect to $$\gamma$$.

> ##### NOTE
> What does this last sentence even mean? We will give it a meaningful definition later.
{: .block-warning}

### Examples
Here are two examples that demonstrate this relation.

Consider $$\gamma = (1,2,3,4,5,6)$$ and $$\pi = (1,2)(3,4)(5,6)$$, we have $$\gamma\pi = (1,3,5)(2)(4)(6)$$. Hence,

$$
\underbrace{\#(\pi)}_{=3} + \underbrace{\#(\gamma)}_{=1} + \underbrace{\#(\gamma\pi)}_{=4} = \underbrace{n}_{=6} + 2 - \underbrace{2g}_{=0}.
$$

Therefore, we see that the genus is zero. I.e., the permutation $$\pi$$ can be drawn on a flat plane without crossing, and this is indeed the case. See the figure below for an illustration.

<br/><img src='/assets/img/blog/2026-07-22-noncrossing-pairing.png' width="100%">

On the other hand, if we let $$\pi = (1,4)(2,5)(3,6)$$, then $$\gamma\pi = (1,5,3)(2,6,4)$$. Hence,

$$
\underbrace{\#(\pi)}_{=3} + \underbrace{\#(\gamma)}_{=1} + \underbrace{\#(\gamma\pi)}_{=2} = \underbrace{n}_{=6} + 2 - \underbrace{2g}_{=1}.
$$

The genus is $$1$$, which is equal to a surface with one hole, i.e., a torus. Thus, the permutation $$\pi$$ cannot be drawn on a plane without edges crossing, instead, it needs to be drawn on a torus. See the figure below for an illustration. If the permutation graph of $$\pi$$ is drawn on a plane (left), it has its edges crossing each other. While if the permutation graph is drawn on a torus (right), the edges will not cross each other.

<br/><img src='/assets/img/blog/2026-07-22-crossing-pairing.png' width="100%">

Note that for both examples above, the ordering of the numbers cannot be permuted as they have to respect the permutation order of $$\gamma$$.

## Proof
The appearance of the genus stems from the Euler's polyhedron formula: if a polyhedron has $$V$$ vertices, $$E$$ edges, and $$F$$ faces, then

$$
\boxed{
    V + F - E = 2 - 2g
},
$$

where $$g$$ is the genus of the polyhedron. The value $$\chi = 2 - 2 g$$ is the Euler characteristic of the polyhedron.

To utilize the Euler's polyhedron formula in our proof, we need to associate a geometric meaning to the elements of the permutation graph.

> ##### NOTE
> The permutation graph we have drawn above are limited in that each edge, which represents a cycle of $$\pi$$, can only have two vertices connected by it. Hence, the cycles represented are all of length $$2$$. This is quite restrictive
>
> In general, we can have cycles of arbitrary length $$\ge 1$$. A new visualization is required.
{: .block-warning}

Notice that each element $$i \in [n]$$ can only be in a single cycle of a permutation. Henceforth, it is better to represent the cycles of $$\pi$$ and $$\gamma$$ as vertices, and the elements in $$[n]$$ as edges connecting cycles in which the elements appear in. I.e., we have

$$V = \#(\pi) + \#(\gamma)$$

and

$$E = n.$$

This creates a bipartite graph, where we have black vertices as $$\#(\pi)$$ and white vertices as $$\#(\gamma)$$. Note that the ordering of the elements around a black or a white vertex should respect the corresponding ordering of the cycle.

What should the faces be? The assignment of the faces should guarantee that the edges do not cross in the sense of this new geometric visualization. (This visualization is equivalent to the previous one under the case of 2-pairing $$\pi$$ and one cycle $$\gamma$$.)

Starting from an edge and heading towards a black vertex, we set the face this edge is traversing around as the face on our left hand side. When arriving at a black vertex, we head for a white vertex by going on the edge that respects $$\pi$$. I.e., if we enter the black vertex by edge $$i$$, then we leave on $$\pi(i)$$. Next, when arriving on a white vertex via edge $$j$$, we head for a black vertex by going on the edge $$\gamma(j)$$. Since $$n$$ is finite, we will be able to return back to $$i$$, and the enclosed surface on our left hand side will be a face to this graph. Since there are $$\#(\gamma\pi)$$ cycles, we have

$$
F = \#(\gamma\pi).
$$

By the transitivity of $$\pi$$ and $$\gamma$$, the graph we have drawn is connected. Then, by applying Euler's polyhedron formula, we arrive at

$$
\underbrace{\#(\pi) + \#(\gamma)}_{V} + \underbrace{\#(\gamma\pi)}_{F} - \underbrace{n}_{E} = 2 - 2g.
$$

Thus it is shown.

## Examples
Here are two examples. First, consider again $$\gamma = (1,2,3,4,5,6)$$ and $$\pi = (1,4)(2,5)(3,6)$$, then $$\gamma\pi = (1,5,3)(2,6,4)$$. We know the genus of this surface to be $$1$$. The new visualization is as shown below. Consider entering the black vertex $$(1,4)$$ via the edge $$1$$, we marked the left-hand side of each traversed edge with arrows, and the encircled face is shaded. We can see that there are indeed two faces, representing the two cycles.

<br/><img src='/assets/img/blog/2026-07-22-permutation-torus1.png' width="100%">

Another example is to consider $$\gamma = (1,2,3,4,5,6)$$ and $$\pi = (1,2,3,4)(5)(6)$$, then $$\gamma\pi = (1,3,5,6)(2,4)$$. The genus of this surface is also $$1$$.

<br/><img src='/assets/img/blog/2026-07-22-permutation-torus2.png' width="100%">

Remember, all the nodes should have their edges ordered with respect to the cycle order, and the same clockwise orientation was chosen.