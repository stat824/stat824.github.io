---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Uniformly Minimum Variance Unbiased Estimators'
weight: 9
---

We say that an estimator $\delta(X)$ is a uniformly minimum-variance unbiased estimator (UMVUE) for $g(\theta)$ if $\mathbb{E} _ {\theta}\delta(X)=g(\theta)$ for all $\theta\in\Theta$ and for any other estimator $\widetilde{\delta}(X)$ which is unbiased for $g(\theta)$, it holds that $\operatornamewithlimits{Var} _ {\theta}(\delta(X))\leq\operatornamewithlimits{Var} _ {\theta}(\widetilde{\delta}(X))$ for all $\theta\in\Theta$. 

{{% details title="Lehmann-Scheffé Theorem" %}}

Suppose that $T$ is unbiased, sufficient, and complete for $\theta$. If $\delta(X)=h(T(X))$ is unbiased for $g(\theta)$, then

* $\delta(X)$ is the only function of $T(X)$ which is unbiased for $g(\theta)$,

* $\delta(X)$ is the unique UMVUE for $g(\theta)$.

{{% /details %}}

{{% details title="Proof" closed="true" %}}

Suppose that $\widetilde{h}(T(X))$ is also unbiased for $g(\theta)$. Then $\mathbb{E} _ {\theta}(\widetilde{h}(T(X))-h(T(X)))$, so by completeness, it follows that $\widetilde{h}(T(X))=h(T(X))$ almost surely. To show the second statement, suppose that $\widetilde{\delta}(X)$ is unbiased for $g(\theta)$. Then $\mathbb{E} _ \theta (\widetilde{\delta}(X)|T(X))$ is also unbiased, so $\mathbb{E} _ \theta (\widetilde{\delta}(X)|T(X))=h(T(X))$. By the Rao-Blackwell theorem, 

$$
\mathbb{E}_{\theta}\left(\mathbb{E}_{\theta}(\widetilde{\delta}(X)|T(X))-g(\theta)\right)^{2}\leq\mathbb{E}_{\theta}\left(\widetilde{\delta}(X)-g(\theta)\right)^{2}.
$$

The left hand side is $\operatornamewithlimits{Var} _ {\theta}(h(T(X))$ and the right hand side is $\operatornamewithlimits{Var} _ {\theta}(\widetilde{\delta}(X))$. 
{{% /details %}}



There are two methods to find UMVUEs:

1. Find $h(T(X))$ for some sufficient and complete $T(X)$ such that $\mathbb{E} _ {\theta}h(T(X))=g(\theta)$ for all $\theta\in\Theta$.

2. Find $\delta(X)$ such that $\mathbb{E} _ {\theta}\delta(X)=g(\theta)$ for all $\theta\in\Theta$. The UMVUE is then $\mathbb{E}_ \theta (\delta(X)|T(X))$ where $T(X)$ is sufficient and complete. 

{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Ber}(\theta)$ where $\theta\in(0,1)$. 

* UMVUE for $\theta$: The estimator $\widehat{\theta}=\overline{X}$ is unbiased, sufficient, and complete, it is the unique UMVUE.

* UMVUE for $\theta^{2}$: Since $\mathbb{E} _ \theta (X_{1}X_{2})=\theta^{2}$, the estimator $\delta(X)=\mathbb{E}(X_{1}X_{2}|\sum_{i=1}^{n}X_{i})$ is unbiased. Since $T(X) = \sum_{i=1}^{n}X_{i}$ is sufficient and complete for $\theta$, it follows that $\delta(X)$ is the UMVUE for $\theta^{2}$. 
{{< /callout >}}


{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Unif}(0,\theta)$ where $\theta>0$. To find the UMVUE for $\theta$, we start with $\mathbb{E} _ {\theta}(2X_{1})=\theta$, so the UMVUE is $\mathbb{E} _ {\theta}(2X_{1}|X_{(n)})$. Since $X_{1}|X_{(n)}\sim\frac{1}{n}\delta_{X_{(n)}}+\left(1-\frac{1}{n}\right)\text{Unif}(0,X_{(n)})$, it follows that 

$$
\mathbb{E}_{\theta}(2X_{1}|X_{(n)})	=2\left(\frac{1}{n}X_{n}+\left(1-\frac{1}{n}\right)\frac{X_{n}}{2}\right)=\left(1+\frac{1}{n}\right)X_{(n)}.
$$
{{< /callout >}}

{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\mu,\sigma^{2})$. A complete sufficient statistic is $\left(\sum_{i=1}^{n}X_{i},\sum_{i=1}^{n}X_{i}^{2}\right)$, which is equivalent to $\left(\overline{X},\sum_{i=1}^{n}(X_{i}-\overline{X})^{2}\right)$. The UMVUE for $\mu$ is $\overline{X}$, and the UMVUE for $\sigma^{2}$ is $\frac{1}{n-1}\sum_{i=1}^{n}(X_{i}-\overline{X})^{2}$. 
{{< /callout >}}


## Stein's unbiased risk estimator

Consider $X\sim N(\theta,I_{p})$ and let $\widehat{\theta}$ be an estimator. We want to find the UMVUE for the risk function $g(\theta)=\mathbb{E} _ {\theta}\Vert\widehat{\theta}-\theta\Vert^{2}$. Note that $X$ is complete and sufficient, so we want to write $\mathbb{E} _ {\theta}\Vert\widehat{\theta}-\theta\Vert^{2}$ as the expectation of some function of $X$ which does not depend on $\theta$. We have

$$
\begin{aligned}
\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2} &=\mathbb{E}_{\theta}\Vert\widehat{\theta}-X+X-\theta\Vert^{2} \\
	&=\mathbb{E}_{\theta}\left(\Vert\widehat{\theta}-X\Vert^{2}+\Vert X-\theta\Vert^{2}+2\langle X-\theta,\widehat{\theta}-X\rangle\right) \\
	&=\mathbb{E}_{\theta}\left(\Vert\widehat{\theta}-X\Vert^{2}+\Vert X-\theta\Vert^{2}-2\langle X-\theta,X\rangle+2\langle X-\theta,\widehat{\theta}\rangle\right).
\end{aligned}
$$

Writing $X=\theta+Z$ where $Z\sim N(0,I_{p})$, we have $\mathbb{E} _ {\theta}\Vert X-\theta\Vert^{2}=p$, $\mathbb{E} _ {\theta}\langle X-\theta,X\rangle=\mathbb{E} _ {\theta}\langle Z,\theta+Z\rangle=p$, and by Stein's lemma

$$
\mathbb{E}_{\theta}\langle X-\theta,\widehat{\theta}\rangle	=\mathbb{E}_{\theta}\langle Z,\widehat{\theta}(\theta+Z)\rangle=\mathbb{E}_{\theta}\sum_{j=1}^{p}\frac{\partial}{\partial z_{j}}\widehat{\theta}_{j}(\theta+Z)=\mathbb{E}_{\theta}\sum_{j=1}^{p}\frac{\partial}{\partial x_{j}}\widehat{\theta}_{j}.
$$

Therefore, $\mathbb{E} _ {\theta}\Vert\widehat{\theta}-\theta\Vert^{2}=\mathbb{E} _ {\theta}\operatorname{SURE}(\widehat{\theta})$ where 

$$
\operatorname{SURE}(\widehat{\theta})=\Vert\widehat{\theta}-X\Vert^{2}-p+2\sum_{j=1}^{p}\frac{\partial}{\partial x_{j}}\widehat{\theta}_{j}
$$

is called Stein's unbiased risk estimator. This is the UMVUE of the risk function. 

{{< callout >}}
Let $\widehat{\theta} _ {c}=cX$. Then $\widehat{\theta} _ {c^{\ast}}$ where $c^{\ast}=\argmin_{c}\operatorname{SURE}(cX)$ will give something similar to the James-Stein estimator. 
{{< /callout >}}

{{< callout >}}
Consider the linear model $Y\sim N(\theta,I_{n})$. Let $X\in\mathbb{R}^{n\times p}$ be a fixed full-rank design matrix and let $\widehat{\beta}=\argmin_{\beta}\Vert Y-X\beta\Vert^{2}$. Then $\widehat{\theta}=X\widehat{\beta}=HY$ where $H=X(X^{T}X)^{-1}X^{T}$. Then

$$
\sum_{i=1}^{n}\frac{\partial}{\partial y_{i}}\widehat{\theta}_{i}=\sum_{i=1}^{n}H_{ii}=\operatorname{Tr}(H)=p,
$$

which gives the Akaike information criterion

$$
\operatorname{SURE}(X\widehat{\beta})=\Vert Y-X\widehat{\beta}\Vert^{2}+2p-n.
$$
{{< /callout >}}