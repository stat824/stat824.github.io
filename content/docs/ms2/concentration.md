---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Basics of Concentration Inequalities'
weight: 1
---

## Why do concentration inequalities matter?

Suppose that we put 10 equally spaced points along each axis of the unit cube in $\mathbb{R}^{p}.$ This gives us $10^{p}$ points in total, which scales exponentially with the dimension $p.$ This is the curse of dimensonality. It paints a bleak scenario for statistics in high-dimensions because at first glance, it seems like we would need an almost infinite amount of data to answer reasonably any type of question when $p$ is large. However, data in high-dimensions can sometimes exhibit appealing properties that make estimation possible. For example, suppose that $X$ follows the unit distribution on the unit sphere of $\mathbb{R}^{p}.$ Then for any Lipschitz function $f$, one has

$$
\mathbb{P}\left[f(X)-\mathbb{E}[f(X)]>t\right]\leq C_{1}e^{-C_{2}t^{2}}
$$

where $C_{1}$ and $C_{2}$ are absolute constants. So regardless of the dimension $p$, a Lipschitz function of $X$ is nearly constant. This phenomenon is by no means restricted to the sphere, and we can find other types of variables that exhibit such properties. 



## Basic tail inequalities

Concentration inequalities are inequalities of the form $\mathbb{P}[X\geq t]\leq\phi(t)$ where $\phi$ goes to zero (rapidly) as $t\to\infty.$ Often, we will deal with concentration inequalities of the form $\mathbb{P}[\overline{X} _ {n} \geq t]\leq\phi _ {n}(t)$ where $\overline{X} _ n = \frac{1}{n} \sum_{i = 1}^n X_i$ is the mean of independent samples. The most basic concentration inequality is the classical Markov's inequality. 

{{% details title="Markov's inequality" %}}

If $X\geq0$ almost surely, then we have

$$
\mathbb{P}[X\geq t]\leq \frac{\mathbb{E}[X]}{t} \quad \text{for all } t > 0.
$$

{{% /details %}}

{{% details title="Proof" closed="true" %}}

We have $\mathbb{E}[X] = \mathbb{E}[X 1 _ {\{X<t\}}] + \mathbb{E}[X 1 _ {\{ X\geq t\}}]
	\geq\mathbb{E}[X1 _ {\{X\geq t\}}]
	\geq t\mathbb{P}[X\geq t].$

{{% /details %}}


If $X$ is square integrable, we have also have Chebyshev’s inequality. 

{{% details title="Chebyshev's inequality" %}}

If $X\in L^{2}(\Omega),$ then 

$$
\mathbb{P}[|X-\mathbb{E}[X]|\geq t]\leq\frac{\operatorname{Var}(X)}{t^{2}} \quad \text{for all t>0.}
$$ 

{{% /details %}}

Chebyshev's inequality follows by applying Markov's inequality to $Z=(X-\mathbb{E}[X])^{2}.$ There are also higher moment analogues:

$$
\mathbb{P}[|X-\mathbb{E}[X]|\geq t]\leq\frac{\mathbb{E}(|X-\mathbb{E}[X]|^{k})}{t^{k}}
$$

which holds for all $k \geq 1.$ Moreover, if $X$ has a moment generating function in a neighbourhood of 0 so that there exists $b>0$ such that $\phi(\lambda)=\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]$ exists for all $|\lambda|\leq b,$ then Markov's inequality implies

$$
\mathbb{P}[X-\mathbb{E}[X]\geq t]=\mathbb{P}[e^{\lambda(X-\mathbb{E}[X])}\geq e^{\lambda t}]\leq\frac{\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]}{e^{\lambda t}}.
$$

This holds for all $|\lambda|\leq b$, and optimizing it with respect to $\lambda$ gives the Chernoff bound

$$
\log\mathbb{P}[X-\mathbb{E}[X]\geq t]\leq\inf_{|\lambda|\leq b}\left(\log\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]-\lambda t\right).
$$

