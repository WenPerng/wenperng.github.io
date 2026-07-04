---
layout: post
title: "Forward and Reverse KL: Interpreting via Information Geometry"
date: 2025-08-29
description: "Following from the last post where we introduced the \\(e\\)- and \\(m\\)-properties of information geometry, I will give an interpretation of the forward and reverse KL divergence in this post."
tags: math geometry
categories: information-geometry
toc:
    sidebar: left
---

> Following from the last post where we introduced the \\(e\\)- and \\(m\\)-properties of information geometry, I will give an interpretation of the forward and reverse KL divergence in this post.

First of all, for those who are unsure of the details, let me introduce first what the forward and reverse KL divergences are.

## Forward and reverse KL divergences
### Mathematical Formulation
If we want to match a true underlying distribution \\(P\\) by an approximate distribution \\(Q\\), we can minimize the "distance" between them. Suppose we restrict \\(Q\\) to be in a subset \\(\mathcal{S}\\), we can define it to be
<p>
$$
    Q^{\star} = \arg\min_{Q\in\mathcal{S}} D_{\mathrm{KL}}(P\|Q).
$$
</p>
This is called the *forward* KL divergence, and it is used to perform *moment matching* or *mean seeking*.

On the other hand, for
<p>
$$
    Q^{\star} = \arg\min_{Q\in\mathcal{S}} D_{\mathrm{KL}}(Q\|P),
$$
</p>
this is called the *reverse* KL divergence, and it is used to perform *mode finding*.

### Mean or mode seeking
The following description largely comes from this [post](https://agustinus.kristia.de/blog/forward-reverse-kl/) which is also worth a read, it gives a more analytical description as to what the difference between the two KL divergences are. The illustrations therein are pretty nice.

In brief, since the KL divergence is asymmetrical:
<p>
$$
D_{\mathrm{KL}}(P_1\|P_2) = \int P_1(x) \log \frac{P_1(x)}{P_2(x)} \,\mathrm{d}\mu(x),
$$
</p>
this implies that when \\(P_2(x) = 0 \Rightarrow P_1(x)\\) or else the KL divergence will diverge[^pun] to infinity! We say that \\(P_2\\) *dominates* \\(P_1\\), or simply \\(P_2 \gg P_1\\).

[^pun]: KL divergence diverges! Pun intended. :)

Henceforth, during forward KL optimization, we want \\(Q\\) to NEVER BE ZERO at places where \\(P\\) is zero, making it spread out. Hence this is mean seeking. It is also called zero-avoiding.

On the other hand, during reverse KL opitimization, we want \\(Q\\) to never locate at a zero of \\(P\\), this makes it concentrate. Hence this is mode seeking. It is also called zero-forcing.

<!-- For a pictorial example, see the end of this post. -->

When to use which really depends on the task at hand, for example, in VAE (variational autoencoders), one often use the reverse KL. This is natural, as it will be better that we train our network to concentrate its generation on a mode and not generate the mean (as the mean might have probability zero on the real distribution).

## Interpretation using information geometry
We can also interpret the meaning of the two KL divergences from the perspective of information geometry. For the mean time, we will restrict our discussion and only consider \\(\mathcal{S}\\) as an exponential family, then our task is to find a distribution \\(Q\\) in the exponential family that best matches the distribution \\(P\\). We choose a convex function \\(\psi\\) as the log-partition function of the family, and \\(\varphi\\) is the convex conjugate to \\(\psi\\).

Say for example, our goal is to find the best Gaussian approximation to an unknown distribution.

### Forward KL
The forward KL is then equivalent to
<p>
$$
    D_{KL}(P\|Q) = B_\psi(\theta(Q),\theta(P)) = B_\varphi(\eta(P)\|\eta(Q)).
$$
</p>
We can see that \\(Q\\) is in the front of \\(B_\psi\\) in forward KL.

<br/><img src='/assets/img/blog/2025-08-30-forwardKL.png' width="60%">

Its solution, as we have established is obtained by an \\(m\\)-projection of \\(P\\) onto \\(\mathcal{S}\\). The \\(m\\)-projection is achieved by connecting with \\(P\\) an \\(m\\)-geodesic \\(\eta(t)\\) that is *orthogonal* to all other \\(e\\)-geodesics on \\(\mathcal{S}\\) stemming from \\(Q^\star\\).

Therefore, the projection \\(Q^\star\\) should *match* \\(P\\) on the dual coordinates \\(\eta\\) (the two have the same coordinates). But wait! The dual coordinate is in fact the expectation:
<p>
$$\eta = \mathbb{E}[x],$$
</p>
hence we have that forward KL is mean seeking.

If one digs deeper into the theory of exponential families, one will know that \\(x\\) is called the **sufficient statistics** of the family. Thus, we should in fact say that the forward KL matches the sufficient statistics.

### Reverse KL
The reverse KL is then equivalent to
<p>
$$
    D_{KL}(Q\|P) = B_\psi(\theta(P),\theta(Q)) = B_\varphi(\eta(Q)\|\eta(P)).
$$
</p>
We can see that \\(Q\\) is in the back of \\(B_\psi\\) in reverse KL.

<br/><img src='/assets/img/blog/2025-08-30-reverseKL.png' width="60%">

Its solution, as we have established is obtained by an \\(e\\)-projection of \\(P\\) onto \\(\mathcal{S}\\). The \\(e\\)-projection is achieved by connecting with \\(P\\) an \\(e\\)-geodesic \\(\theta(t)\\) that is *orthogonal* to all other \\(m\\)-geodesics on \\(\mathcal{S}\\) stemming from \\(Q^\star\\).

Therefore, the projection \\(Q^\star\\) should *match* \\(P\\) on the primal coordinates \\(\theta\\) (the two have the same coordinates). They have the same mode, hence this is mode seeking.

---
For those who are enticipating an example can wait, I am still working on it haha. It requires a bit more math than merely the ones I have gone over so far.
