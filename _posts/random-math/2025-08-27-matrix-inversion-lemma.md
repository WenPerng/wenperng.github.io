---
layout: post
title: Matrix Inversion Lemmas
date: 2025-08-27
description: "This post introduces two useful matrix inversion lemmas that I have actually utilized them in my research at EPFL."
tags: math
categories: random-math
toc:
    sidebar: left
---

> This post introduces two useful matrix inversion lemmas, the Woodbury formula that inverts matrix of the form $$A+UCV$$, and the inverse of a $$2\times2$$ block-partitioned matrix. So useful that I have actually utilized them in my research at EPFL.

Though they may seem daunting at first sight, they are actually quite trivial results with simple proofs. Without further adieu, let's get on with them. 

## Woodbury's formula
The [Woodbury matrix inversion formula](https://en.wikipedia.org/wiki/Woodbury_matrix_identity#Direct_proof) is of the form

$$
\boxed{
    (A+UCV)^{-1} = A^{-1} - A^{-1}U(C^{-1} + VA^{-1}U)^{-1} V A^{-1}
}.
$$

This lemma is especially useful is the size of $$A$$ is large, but the size of $$C$$ is small.

### Proof
The proof is as below: for matrices $$X$$, $$Y$$ such that the following operations are valid.

$$
\begin{align*}
    \left(I - XY\right)^{-1} &= \sum_{k=0}^{\infty} (XY)^k \\
    &= I + X \left(\sum_{k=0}^{\infty} (YX)^n \right) Y \\
    &= I + X \left(YX\right)^{-1} Y
\end{align*}
$$

By setting $$X = A^{-1} U$$ and $$Y = CV$$, we have

$$
\begin{align*}
    \left(A + UCV\right)^{-1} &= \left(I + A^{-1}UCV\right) A^{-1}\\
    &= \left(I + XY\right) A^{-1} \\
    &= \left(I + X \left(I + YX\right)^{-1} Y\right) A^{-1} \\
    &= A^{-1} + A^{-1} U \left(I + CVA^{-1} U\right) CV A^{-1} \\
    &= A^{-1} - A^{-1}U(C^{-1} + VA^{-1}U)^{-1} V A^{-1}. \;\;\;\;\; \blacksquare
\end{align*}
$$

Thus it is proven.


## Inverse of block-partitioned matrix
For block-partitioned matrices, especially the $$2\times2$$ case, we have a nice formula for inverting it. Assume $$A$$ is invertible, then

$$
\boxed{
    \left[\begin{array}{c:c}
    A & B \\ \hdashline
    C & D
    \end{array}\right]^{-1} = \left[\begin{array}{c:c}
    A^{-1} + A^{-1}B\Delta^{-1}CA^{-1} & -A^{-1}B\Delta^{-1} \\ \hdashline
    -\Delta^{-1}CA^{-1} & \Delta^{-1}
    \end{array}\right]
},
$$

where

$$
\Delta = D - CA^{-1}B.
$$

The term $$\Delta$$ is also known as the ***Schur complement*** of $$A$$ of the whole matrix, denoted as $$\Delta = M/A$$, where $$M$$ is the full block matrix.

### Proof
The proof is trivial once you know the trick. Remember how we obtain the inverse to a matrix by consecutively applying row operations on an augmented matrix, we will now extend the procedure to block-partitioned matrices. The subtlety lies in the fact that matrix multiplication is NOT commutative, hence, one should be careful whether a matrix is multiplied for the left or the right. For row operations, the matrices are multiplied from the left:

$$
\left[\begin{matrix}
    1 & 2 \\ 0 & 1
\end{matrix}\right] \left[\begin{matrix}
    a & b \\ c & d
\end{matrix}\right] = \left[\begin{matrix}
    a + 2c & b + 2d \\ c & d
\end{matrix}\right].
$$

Henceforth, we have the following derivation:

$$
\begin{aligned}
    \left[\begin{array}{cc:cc}
        A & B & I & 0 \\
        C & D & 0 & I
    \end{array}\right] &\rightarrow \left[\begin{array}{cc:cc}
        A & B & I & 0 \\
        C - {\color{cyan}CA^{-1}}A & D - {\color{cyan}CA^{-1}}B & -{\color{cyan}CA^{-1}} & I
    \end{array}\right] \\
    &\rightarrow \left[\begin{array}{cc:cc}
        A & B - {\color{cyan}B\Delta^{-1}}\Delta & I + {\color{cyan}B\Delta^{-1}}CA^{-1} & - {\color{cyan}B\Delta^{-1}} \\
        0 & \Delta & -CA^{-1} & I
    \end{array}\right] \\
    &\rightarrow \left[\begin{array}{cc:cc}
        I & 0 & {\color{cyan}A^{-1}} + {\color{cyan}A^{-1}}B\Delta^{-1}CA^{-1} & - {\color{cyan}A^{-1}}B\Delta^{-1} \\
        0 & I & -{\color{cyan}\Delta^{-1}}CA^{-1} & {\color{cyan}\Delta^{-1}}
    \end{array}\right].\;\;\;\;\;\blacksquare
\end{aligned}
$$

The block on the right is the derived inverse.