---
layout: post
title: f-Divergences
date: 2025-08-31
description: "This post talks about another type of information divergence, the f-divergence."
tags: math geometry
categories: information-geometry
toc:
    sidebar: left
---

> This post talks about another type of information divergence, the f-divergence.

What constitutes a *divergence* between points on a manifold? See the definition below.

Consider points \\(P\\) and \\(Q\\) on a manifold, \\(D(P,Q)\\) is called a divergence if (1) it is strictly non-negative, (2) it equals to zero iff \\(P=Q\\), and (3) by denoting the coordinates to \\(P\\) and \\(Q\\) as \\(\xi_P\\) and \\(\xi_Q = \xi_P + \mathrm{d}\xi\\), respectively, then
<p>
$$
D(P,Q) = \frac{1}{2} g_{ij}(\xi_P)\,\mathrm{d}\xi^i \,\mathrm{d}\xi^j + O(|\mathrm{d}\xi|^3),
$$
</p>
where the metric \\(g_{ij}\\) is positive-definite and the *Einstein summation convention* is used.

Through the definition above, we are able to identify a new set of divergences, the \\(f\\)-divergences. These will be of great importance once we decide to consider the full geometry of information theory. Besides that, in information theory, these information quantities are also of much use.

But first of all, let us check that the Bregman divergence satisfies the above definition.

## Taylor expansion of Bregman divergence
For \\(B_\psi\\) with \\(\psi\\) strictly convex and differentiable, we can immediately show the first two. The third one also follows right away, however, let us see what the derived metric is:
<p>

$$
\begin{align*}
    B_F(\theta,\theta + \mathrm{d}\theta) &= \psi(\theta) - \psi(\theta + \mathrm{d}\theta) + \langle \nabla \psi(\theta + \mathrm{d}\theta), \mathrm{d}\theta\rangle \\
    &= - \langle\nabla\psi(\theta), \mathrm{d}\theta\rangle + \langle \nabla\psi(\theta) + \nabla^2\psi(\theta)[\mathrm{d}\theta], \mathrm{d}\theta\rangle \\
    &= \langle \nabla^2\psi(\theta)[\mathrm{d}\theta], \mathrm{d}\theta\rangle.
\end{align*}
$$
</p>
The positive-definiteness of \\(B_\psi\\) follows from the strict convexity of \\(\psi\\).

For those who have questions about the notation above, one can refer to my talks on [matrix differentiation](/talks/2024-09-18-talk) and [manifold optimization](/talks/2024-10-01-talk). But basically, one can view \\(\nabla^2\psi : V \rightarrow V^\*\\), hence I used the square brackets \[ and \] to denote its action[^1].

[^1]: Note that the equation above is an abuse of notation, where though \\(\theta\\) is a point on the manifold, we treat \\(\mathrm{d}\theta\\) a tangent vector as additive with the point on the manifold. If written more rigorously, one should use the exponential map to write \\(B_F(\theta,\exp_\theta(\mathrm{d}\theta))\\) instead. Now that I think about it, you can just imagine we are working on an \\(e\\)-flat manifold, then there will be no problem.

When \\(\psi\\) is the free energy of an exponential family, we can rewrite the metric \\(g\\) as[^2]: firstly, note that \\(x\\) and \\(\theta\\) are functions of each other, then

[^2]: In operator notation, since I have already shown the details for the index notation in [this post](/posts/2025/08/blog-post-5/).

<p>
$$
\begin{align*}
    g = \nabla^2 \psi(\theta) &= \mathbb{E}[xx^\mathsf{T}] - \mathbb{E}[x]\mathbb{E}[x]^\mathsf{T} \\
    &= \mathbb{E}\left[\left(x - \mathbb{E}[x]\right) \left(x - \mathbb{E}[x]\right)^{\mathsf{T}}\right] \\
    &= \mathbb{E}\left[\left(x - \nabla\psi(\theta)\right) \left(x - \nabla\psi(\theta)\right)^\mathsf{T}\right] \\
    &= \mathbb{E}\left[\left(\nabla \log p(x\vert\theta)\right) \left(\nabla \log p(x\vert\theta)\right)^{\mathsf{T}} \right]. \;\;\;\;\; \blacksquare
\end{align*}
$$
</p>

We finally obtain that the induced metric is the *Fisher information matrix*!
<p>
$$
\boxed{\begin{aligned}
    \nabla^2\psi(\theta) = \mathcal{I}(\theta) &= \mathbb{E}\left[\left(\nabla \log p(x\vert\theta)\right) \left(\nabla \log p(x\vert\theta)\right)^{\mathsf{T}} \right] \\
    &= - \mathbb{E}\left[\nabla^2 \log p(x\vert\theta)\right]
\end{aligned}}.
$$
</p>

The second equality is by differentiating the regularity condition (the total probability is 1):
<p>
$$
\begin{align*}
    1 &= \int p(x\vert\theta)\,\mathrm{d}\mu \\
    \Rightarrow 0 &= \nabla^2 \int p(x\vert\theta)\,\mathrm{d}\mu = \nabla \int \frac{\nabla p(x\vert\theta)}{p(x\vert\theta)} p(x\vert\theta)\, \mathrm{d}\mu \\
    &= \nabla \int p(x\vert\theta) \nabla\log p(\vert\theta) \,\mathrm{d}\mu \\
    &= \int \left(\nabla\log p(x\vert\theta)\right) \left(\nabla\log p(x\vert\theta)\right)^\mathsf{T} p(x\vert\theta) \,\mathrm{d}\mu \\
    &\hspace{1cm} + \int \left(\nabla^2 p(x\vert\theta) \right) p(x\vert\theta) \,\mathrm{d}\mu. \;\;\;\;\; \blacksquare
\end{align*}
$$
</p>

## \\(f\\)-divergence
Next, let us define the \\(f\\)-divergences. Given a differentiable convex function \\(f:[0,\infty)\rightarrow (-\infty,\infty)\\) that satisfies \\(f(1) = 0\\). Then we write the associated \\(f\\)-divergence between two distributions \\(P\\) and \\(Q\\) as
<p>
$$\boxed{
    D_f(P\|Q) = \sum p_i f\left(\frac{q_i}{p_i}\right) = \int f\left(\frac{\mathrm{d}Q}{\mathrm{d}P}\right) \,\mathrm{d}P
}.$$
</p>

### Explanation to criterion on \\(f\\)
Here we bring about some properties of the \\(f\\)-divergence that supports that our constraint \\(f(1) = 0\\) is well-justified and causes no major restriction.

This criterion is required for positivity of the divergence: by Jensen's inequality,
<p>

$$
    D_f(P\|Q) = \sum p_i f\left(\frac{q_i}{p_i}\right) \ge f\left(\sum p_i \cdot \frac{q_i}{p_i}\right) = f(1) = 0.
$$
</p>
The equality is achieved iff \\(q_i = p_i\\).

Furthermore, as \\(f\\) is convex, by the above, we can see that \\(f\\)-divergence is indeed a divergence.


Next, note that the \\(f\\)-divergence is invariant under addition of linear term and scales linearly with \\(f\\): let \\(g(x) = af(x) + c(x-1)\\), then
<p>
$$
\begin{align*}
    D_g(P\|Q) &= \sum p_i \left(cf\left(\frac{q_i}{p_i}\right) + c\left(\frac{q_i}{p_i} - 1\right)\right) \\
    &= c \sum p_i f\left(\frac{q_i}{p_i}\right) = cD_f(P\|Q).
\end{align*}
$$
</p>
Without loss of generality, we have the freedom of setting \\(f'(1) = f^{(1)}(1) = 0\\) and \\(f^{(2)}(1) = 1\\). But it is not enforced.

### Dual \\(f\\)-divergence
By defining the *dual* to \\(f\\) as \\(f^\*\\) (NOT to be confused with *convex* conjugation):
<P>
$$\boxed{
f^*(u) = u f\left(\frac{1}{u}\right)
},
$$
</p>
we can show that the \\(f\\)-divergence and its dual satisfies
<p>
$$\boxed{
    D_f(P\|Q) = D_{f^*}(Q\|P)
}.
$$
</p>
Note that one should be careful and establish the convexity to \\(f^\*\\): let \\(u(t) = (1-t)u_1+tu_2\\),
<p>
$$
\begin{aligned}
    f^*\left((1-t)u_1+tu_2\right) &= u(t) f\left(u(t)\right) \\
    &= u(t) f\left(\frac{(1-t)u_1}{u(t)} \frac{1}{u_1} + \frac{tu_2}{u(t)} \frac{1}{u_2}\right) \\
    &= u(t) \left(\frac{(1-t)u_1}{u(t)} f\left(\frac{1}{u_1}\right) + \frac{tu_2}{u(t)} f\left(\frac{1}{u_2}\right)\right) \\
    &= (1-t) f^*(u_1) + t f^*(u_2).
\end{aligned}
$$
</p>

This proof is the same as proving the [*perspective*](https://www.heldermann-verlag.de/jca/jca15/jca0677_b.pdf#:~:text=The%20key%20of%20the%20new%20proof%20is%20the,%28x%2Cy%29%20%E2%86%92%20g%28y%29f%28x%2Fg%28y%29%29%2C%20with%20suitable%20assumptions%20on%20g.) of a convex function is convex.

It is due to this duality that one may often see a different definition to the \\(f\\)-divergence expressed instead in its dual divergence. For me, I stick with this divergence that we have since I follow the general notations from Amari's book on information geometry.

## Examples of \\(f\\)-divergences
Here I introduce you to some examples of \\(f\\)-divergence. Some of them were introduced because they have a special place in my heart, these includes the Hellinger distance, the total variational distance, and the Bhattacharyya distance, as they appeared in my [lecture notes to modern coding theory](/projects/2025-06-MCTT-note). 

The last one introduced is the "Amari" \\(\alpha\\)-divergence. Note that it is a bit different from "Rényi" \\(\alpha\\)-divergence.  Their similarities and differences are clarified [here](https://mathoverflow.net/questions/339233/relationship-between-alpha-divergences#:~:text=The%20simplest%20thing%20to%20say%20is%20that%20%24R_%5B%26alpha%26%5D%24,order%20%24%20%281%20%2B%20%5B%26alpha%26%5D%29%2F2%24%2C%20and%20vice%20versa.).

### KL divergence
The first one that we discuss is obviously the KL divergence. Choosing \\(f(u) = -\log u\\), we have
<p>
$$D_{\mathrm{KL}}(P\|Q) = D_f(P\|Q).$$
</p>
Or by choosing \\(f^\*(u) = u\log u\\), we have
<p>
$$D_{\mathrm{KL}}(P\|Q) = D_{f^*}(Q\|P).$$
</p>
We see that KL divergence is both a Bregman divergence and an \\(f\\)-divergence.

### \\(\chi^\alpha\\)-divergence
For \\(f_\alpha(u) = \frac{1}{2}\|u-1\|^\alpha \\) and \\(\alpha \ge 1\\), 
<p>
$$
\chi^\alpha(P\|Q) = D_{f_\alpha}(P\|Q).
$$
</p>

For the case of \\(\chi^2\\), this is useful in hypothesis testing. The term "Neyman-Pearson test" may ring a bell.

For the case of \\(\chi^1\\), this is the total variation distance:
<p>
$$
    \delta(P,Q) = \frac{1}{2} \sum |p_i-q_i| = D_{f_1}(P\|Q).
$$
</p>
Note that it is not differentiable though, hence it is NOT a divergence by our definition.

### Bhattacharyya distance
By choosing \\(f(u) = \sqrt{u}\\), we have the Bhattacharyya distance
<p>
$$
    D_{\mathrm{BC}}(P\|Q) = \sum \sqrt{p_iq_i} = D_f(P\|Q).
$$
</p>

### Amari \\(\alpha\\)-divergence
Define
<p>
$$\boxed{
    f_\alpha(u) = \begin{cases}
        u \log u, & \alpha = 1;\\
        \frac{4}{1-\alpha^2} \left(1 - u^{\frac{1+\alpha}{2}}\right), & \alpha \neq \pm 1; \\
        -\log u, & \alpha = -1,
    \end{cases}
}$$
</p>
then the Amari \\(\alpha\\)-divergence is

<p>
$$\boxed{
A_\alpha(P\|Q) = \begin{cases}
    \sum q_i \log\frac{q_i}{p_i} = D_{\mathrm{KL}}(Q\|P), & \alpha = 1; \\
    \frac{4}{1-\alpha^2} \left(1 - \sum p_i^{\frac{1-\alpha}{2}} q_i^{\frac{1+\alpha}{2}}\right), & \alpha \neq \pm 1; \\
    \sum p_i \log\frac{p_i}{q_i} = D_{\mathrm{KL}}(P\|Q), & \alpha = -1.
\end{cases}
}.$$
</p>

When \\(\alpha = 0\\), we have \\(f(u) = 4(1-\sqrt{u})\\), in which we obtain the Hellinger distance:
<p>
$$
D_f(P\|Q) = 2 \sum\left(\sqrt{p_i} - \sqrt{q_i}\right)^2.
$$
</p>
Hence, the Hellinger distance is \\(0\\)-divergence, KL divergence is \\(-1\\)-divergence, and its dual is the \\(1\\)-divergence.

As a final property to introduce in this post, we have the duality between \\(\alpha\\)-divergences.

The following duality holds:
<p>
$$
\boxed{
    A_\alpha(P\|Q) = A_{-\alpha}(Q\|P)
}.
$$
</p>
The proof is trivial.

As a final note, the Rényi \\(\alpha\\)-divergence is written as
<p>
$$\boxed{
    R_\alpha(P\|Q) = \frac{1}{\alpha - 1} \log \sum p_i^\alpha q_i^{1-\alpha}.
}.$$
</p>

### Proof
#### Establishing Amari \\(\alpha\\)-divergence
The associated convex function \\(f\\) has limits:
<p>
$$
\begin{align*}
    \lim_{\alpha \rightarrow 1} f_{\alpha}(u) &= \lim_{\alpha \rightarrow 1} \frac{4}{1+\alpha} \frac{u^{\frac{1+\alpha}{2}}-1}{\alpha - 1} \\
    &= 2 \left.\frac{\mathrm{d}}{\mathrm{d} \alpha}\right|_{1} u^{\frac{1+\alpha}{2}} \\
    &= 2 \cdot \left.\frac{1}{2} \log u \cdot u^{\frac{1+\alpha}{2}}\right|_1 = u\log u. \;\;\;\;\; \blacksquare
\end{align*}
$$
</p>
And
<p>
$$
\begin{align*}
    \lim_{\alpha \rightarrow -1} f_{\alpha}(u) &= \lim_{\alpha \rightarrow 1} -\frac{4}{1-\alpha} \frac{u^{\frac{1+\alpha}{2}} - 1}{\alpha - (-1)} \\
    &= -2 \left.\frac{\mathrm{d}}{\mathrm{d} \alpha}\right|_{-1} u^{\frac{1+\alpha}{2}} \\
    &= -2 \cdot \left.\frac{1}{2} \log u \cdot u^{\frac{1+\alpha}{2}}\right|_{-1} = -\log u. \;\;\;\;\; \blacksquare
\end{align*}
$$
</p>

---