---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Vector and Matrix Norms'
weight: 1
---
Let $\mathbb{F} = \mathbb{R}$ or $\mathbb{C}$. We give here several examples of vector and matrix norms. 

## Vector norms

### $p$-norms

For $p \geq 1$ and $\mathbf{x} \in \mathbb{F}^n$, we define the $p$-norm $\Vert \mathbf{x} \Vert_p$ by 

$$
\Vert \mathbf{x} \Vert_p = (|x_1|^p + \cdots + |x_n|^p)^{1/p}
$$

It is easy to see that for any $p$, we have 

$$
\left( \max_{i=1,\ldots,n} |x_i|^p \right)^{1/p} \leq \Vert \mathbf{x} \Vert_p \leq \left( n \max_{i=1,\ldots,n} |x_i|^p \right)^{1/p},
$$

from which it follows that 

$$
\max_{i=1,\ldots,n} |x_i| \leq \Vert \mathbf{x} \Vert_p \leq n^{1/p} \max_{i=1,\ldots,n} |x_i|.
$$

Taking $p \to \infty$ gives the infinity norm

$$
\Vert \mathbf{x} \Vert_\infty = \lim_{p \to \infty} \Vert \mathbf{x} \Vert_p = \max_{i=1,\ldots,n} |x_i|
$$

which is also known as the Chebyshev norm. 

### Weighted $p$-norms

A generalization of the $p$-norm is the weighted $p$-norm

$$
\Vert \mathbf{x} \Vert_{p,\mathbf{w}} = \left( \sum_{i=1}^n w_i |x_i|^p \right)^{1/p}.
$$

It can be shown that this is a norm as long as the weights $w_1,\ldots,w_n$ are strictly positive real numbers.

### $A$-norms

A vast generalization of the weighted 2-norm is the $A$-norm or Mahalanobis norm, defined in terms of a matrix $A$ by

$$
\Vert \mathbf{x} \Vert_A = (\mathbf{x}^\ast A \mathbf{x})^{1/2} = \left( \sum_{i,j = 1}^n a_{ij} \overline{x}_i x_j\right)^{1/2}
$$

which can be shown to be a norm if $A$ is positive definite. If $A$ is a diagonal matrix, this reduces to a weighted 2-norm. 

## Matrix norms