---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Consistency of MLE'
weight: 11
---

Suppose that $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}P_{\theta^{\ast}}$. The maximum likelihood estimator is defined to be

$$
\widehat{\theta}=\argmax_{\theta}\sum_{i=1}^{n}\log p_{\theta}(X_{i}).
$$ 

Under identifiability and some empirical process condition, we will prove that the MLE $\widehat{\theta}$ is consistent, meaning that

$$
\mathbb{P}_{\theta^{\ast}}\left(\Vert\widehat{\theta}-\theta^{\ast}\Vert>\epsilon\right)\overset{n\to\infty}{\longrightarrow}0.
$$

The proof will be split into two parts. Firstly, we bound the probability in terms of the Kullback–Leibler divergence of $P_{\theta^\ast}$ and $P_{\widehat{\theta}}$. Then we finish off by applying a uniform law of large numbers. 

## Part 1: Bound using Kullback–Leibler divergence

For any two distributions $P$ and $Q$ with densities $p$ and $q$, we define the Kullback–Leibler divergence $D(P\Vert Q)$ to be

$$
D(P\Vert Q)=\int p\log\frac{p}{q}.
$$

The KL divergence is always non-negative.

{{% details title="Lemma" %}}
For any two probability distributions $P$ and $Q$, we have $D(P\Vert Q) \geq 0$.
{{% /details %}}

{{% details title="Proof" closed="true" %}}
We have

$$
D(P\Vert Q)=\int p\log\frac{p}{q}=\int qf(\frac{p}{q}),
$$

where $f(t)=t\log t$. Since $f$ is convex, by Jensen's inequality, we have

$$
\int qf(\frac{p}{q})	=\mathbb{E}_{X\sim Q}f\left(\frac{p(X)}{q(X)}\right)
	\geq f\left(\mathbb{E}_{X\sim Q}\frac{p(X)}{q(X)}\right)
	=f(1)
	=0.
$$
{{% /details %}}


## Part 2: Apply uniform law of large numbers


