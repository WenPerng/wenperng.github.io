---
layout: post
title: Bregman Divergence is a Squared Distance
date: 2025-08-23
description: "This note demonstrates why the Bregman divergence can be seen as an asymmetric squared distance. This topic is deeply related to the field of information geometry."
tags: math geometry
categories: information-geometry
toc:
    sidebar: left
---

> This note demonstrates why the Bregman divergence can be seen as an asymmetric squared distance. This topic is deeply related to the field of information geometry.

In the last blog on [mirror descent](/posts/optimization/mirror-descent), we mentioned how we can treat Bregman divergences as squared distances, but without any further explanations! Therefore, this post is to elaborate on it. This is a basic result from information geometry, a subject under information theory that utilizes the tools from differential geometry. However, do not worry, as this post contains nothing from differential geometry nor information theory. But bare in mind, this is a lengthy post.

For those who are interested, the works by [Frank Nielsen](https://franknielsen.github.io/) are definitenly worth a read and is a good place to start. To dive deeper, the you should follow the footsteps of [Shun'ichi Amari](https://en.wikipedia.org/wiki/Shun%27ichi_Amari).

---
## Main results
I shall first state the results here, the proofs to the statements are some boring algebra and are deferred to the end.

### Bregman divergence is a squared distance
The first result is the "generalized law of cosines" satisfied by the Bregman divergence: for points $$x_1, x_2, x_3 \in \mathcal{M} \subseteq V$$[^notation],

$$
\boxed{
\begin{equation*}
    B_F(x_1, x_3) = B_F(x_1, x_2) + B_F(x_2, x_3) + \langle x_1 - x_2, \nabla F(x_2) - \nabla F(x_3) \rangle.
\end{equation*}
}
$$

And in the special case where the *orthogonality condition* $$\langle x_1 - x_2, \nabla F(x_2) - \nabla F(x_3) \rangle = 0$$ is met, we obtain the "generalized Pythagorean theorem":

$$
\boxed{
\begin{equation*}
	B_F(x_1, x_3) = B_F(x_1, x_2) + B_F(x_2, x_3).
\end{equation*}
}
$$

If we view $$B_F(x_1,x_2)$$ as some form of an asymmetric squared distance over the "edge" connecting $$x_1$$ from $$x_2$$, then the equations above are direct analogs of the usual law of cosines and Pythagorean theorem we are so accustomed to from high school[^1]. The other term $$\langle x_1 - x_2, \nabla F(x_2) - \nabla F(x_3) \rangle$$ is then an asymmetric inner product between the edge connecting $$x_1$$ from $$x_2$$ and the edge connecting $$x_2$$ from $$x_3$$.

[^notation]: Note that the notations are modified in comparison to the previous two posts. This is to bridge this discussion with further posts that might be more general.
[^1]: I'm assuming the Taiwanese education system here.

Let's make sense of their validity in the usual Euclidean distance case: Let $$F(x) = \| x \|_2^2$$, then $$\nabla F(x) = 2x$$ and $$B_F(x_1, x_2) = \|x_1-x_2\|_2^2$$, then generalized law of cosines becomes:

$$
\left\|x_1 - x_3\right\|_2^2 = \left\|x_1 - x_2\right\|_2^2 + \left\|x_2 - x_3\right\|_2^2 - 2 \left\|x_1 - x_2\right\|_2 \left\|x_2 - x_3\right\|_2 \cos\theta.
$$

This is the Euclidean law of cosine, where $$\theta$$ is the angle between the vectors $$x_1-x_2$$ and $$x_3-x_2$$.

## Primal and dual geodesics
Back to the more general case, let me persuade to you how the generalized law of cosines is indeed the law of cosine, just with a more exotic notion of edges.

Remember from [the post about mirror descent](/posts/optimization/mirror-descent), we used the mirror map $$\nabla F$$ to map a point \\(x\\) in the primal space to another point \\(y\\) in the dual (mirror) space. We can now see that the edge
<p>
$$x_1 - x_2$$
</p>
is a straight line (geodesic) in the primal space, while the edge
<p>
$$\nabla F(x_2) - \nabla F(x_3)$$
</p>
is a straight line in the dual space. Hence they are given the name the primal geodesic (between \\(x_1\\) and \\(x_2\\)) and the dual geodesic (between \\(x_2\\) and \\(x_3\\)).

### Interpreting the generalized law of cosines
Back to the generalized law of cosines. The Bregman divergence \\(B_F(x_1,x_2)\\) is the squared length of the primal geodesic, while \\(B_F(x_2,x_3)\\) is the squared length of the *dual* geodesic. The reason why the first geodesic is taken to be the primal while the latter is taken to be the dual is because the Bregman divergence is "asymmetric". In fact, we can note that
<p>
$$
B_F({\color{red}\text{primal}},{\color{teal}\text{dual}}),
$$
</p>
the geodesic that connects to the first element should be primal; the geodesic that connects to the second element should be dual. Easy to remember, right?

<br/><img src='/assets/img/blog/2025-08-23-geodesics.png' width="60%">

But wait! Weird. Isn't \\(B_F(x_2,x_3)\\) the same equation as the squared length of a *primal* geodesic? Great observation. But as we will see in the next section, the two lengths are actually the same.


## Some more properties of the Bregman divergence
Last time we have shown how, given a differentiable strictly convex closed function \\(F\\), we are able to map between the primal and dual (mirror) spaces. The notion of primal and dual is everywhere, appearing in anything that relates with the Bregman divergence, and of course, in information geometry.

This secion shows you some more examples to give you a sense of what's going on and shed some light on the relations of primal and dual.

### Relating the primal and the dual
This subsection gives some more description to the Bregman divergence. First, we will show that
<p>
$$\boxed{\begin{equation*}
	B_F(x_1,x_2) = B_{F^*}(y_2,y_1),
\end{equation*}}$$
</p>
where \\(y_1 = \nabla F(x_1)\\) and \\(y_2 = \nabla F(x_2)\\). This equation basically states that the lengths of the primal geodesic and the dual geodesic are the same. Its proof is simple: by invoking the definition to the convex conjugates, we have
<p>
$$\begin{align*}
	B_{F^*}(y_2,y_1) &= F^*(y_2) - F^*(y_1) - \left\langle \nabla F^*(y_1), y_2-y_1\right\rangle \\
	&= \left(\langle x_2,y_2\rangle -F(x_2)\right) - \left(\langle x_1,y_1\rangle -F(x_1)\right) - \langle x_1,y_2-y_1\rangle \\
	&= F(x_1) - F(x_2) - \langle y_2,x_1-x_2\rangle. \;\;\;\;\;\blacksquare
\end{align*}$$
</p>
Thus it is proven.

The second thing I want to introduce you to is the *Fenchel-Young divergence*:
<p>
$$\boxed{\begin{equation*}
Y_{F,F^*}(x_1,y_2) = F(x_1) + F^*(y_2) - \langle x_1,y_2\rangle.
\end{equation*}}$$
</p>
As a small excercise, one should check that the following relations hold:
<p>
$$\boxed{\begin{align*}
	Y_{F,F^*}(x_1,y_2)
	&= Y_{F^*,F}(y_1,x_2) \\
	&= B_{F}(x_1,x_2) \\
	&= B_{F^*}(y_2,y_1).
\end{align*}}$$
</p>
The symmetry of these relations really demonstrate the duality.

### Projection theorems
Having the generalized Pythagorean theorem, we can now define projections!

Consider a subspace \\(\mathcal{S} \subseteq \mathcal{M}\\), we want to find a point \\(x_2 \in \mathcal{S}\\) that minimizes the Bregman divergence to \\(x_1\mathcal{M}\\), viz.,
<p>
$$
\boxed{x_2 = \arg\min_{x\in\mathcal{S}} B_F(x_1,x)}.
$$
</p>
How can we identify \\(x_2\\)? Look at the figure below. From our intuition in Euclidean space, we can identify \\(x_2\\) as the point that results in the primal geodesic \\(x_1-x_2\\) being perpendicular to \\(\mathcal{S}\\).

<br/><img src='/assets/img/blog/2025-08-23-primal-projection.png' width="60%">

We can show the statement above more rigorously. Consider any other point \\(x_3 \in \mathcal{S}\\), by the generalized Pythagorean:
<p>
$$\begin{align*}
	B_F(x_1,x_3) = B_F(x_1,x_2) + B_F(x_2,x_3) \ge B_F(x_1,x_2),
\end{align*}$$
</p>
wher the inequality is by the fact that the Bregman divergence being non-negative and equates to zero if and only if \\(x_2=x_3\\) (Can you prove it? Remember that \\(F\\) is convex.). We call the \\(x_2\\) obtained the "primal geodesic projection of \\(x_1\\) onto \\(\mathcal{S}\\).

By similar arguments, we have the "dual geodesic projection of \\(x_1\\) onto \\(\mathcal{S}\\)" defined as
<p>
$$
\boxed{x_2 = \arg\min_{x\in\mathcal{S}} B_F(x,x_1)}.
$$
</p>
An illustration of this projection is shown below.

<br/><img src='/assets/img/blog/2025-08-23-dual-projection.png' width="60%">

---
I hope that these discussions have kindled your interest in information geometry as well. In the future, I might do a note-like blog sharing cool things I find while learning information geometry on this blog. Hope you enjoyed this exposition. See ya.

## Proofs to statements
With the notation defined as above, let us show the generalized law of cosine:
<p>
$$\begin{align*}
	B_F(x_1,x_3) 
	&= F(x_1) - F(x_3) - \langle \nabla F(x_3), x_1 - x_3 \rangle \\
	&= F(x_1) - {\color{teal} F(x_2)} - {\color{teal} \langle \nabla F(x_2), x_1 - x_2\rangle} \ldots \\
	&\hspace{1cm} + {\color{teal} F(x_2)} - F(x_3) - {\color{teal} \langle \nabla F(x_3), x_2 - x_3\rangle} \ldots \\
	&\hspace{1cm} - \langle \nabla F(x_3), x_1 - x_3\rangle + {\color{teal} \langle \nabla F(x_2), x_1 - x_2\rangle} + {\color{teal} \langle \nabla F(x_3), x_2 - x_3\rangle} \\
	&= B_F(x_1,x_3) + B_F(x_2,x_3) + \langle \nabla F(x_2), x_1-x_2 \rangle + \langle \nabla F(x_3), x_2-x_1 \rangle \\
	&= B_F(x_1,x_3) + B_F(x_2,x_3) + \langle x_1-x_2, \nabla F(x_2) - \nabla F(x_3) \rangle \;\;\;\;\; \blacksquare
\end{align*}$$
</p>
Thus it is proven.

---