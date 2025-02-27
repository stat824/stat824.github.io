---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'James-Stein Estimator'
weight: 6
---

Let $X_{1},\ldots,X_{n}\overset{\mathrm{iid}}{\sim}N(\theta,I_{p})$ where $\theta\in\mathbb{R}^{p}$, and consider the loss function $L(\hat{\theta},\theta)=\Vert\hat{\theta}-\theta\Vert^{2}$. As we have seen, the sample mean $\overline{X}$ is not admissible for $p \geq 3$. The James-Stein estimator gives an example of an estimator which has strictly smaller risk than $\overline{X}$. It is defined as

$$
\hat{\theta}_{\text{JS}}=\left(1-\frac{p-2}{n\Vert\overline{X}\Vert^{2}}\right)\overline{X}.
$$

## James-Stein estimator as an empirical Bayes estimator
 
This estimator can be derived from the empirical Bayes perspective. In empirical Bayes, the prior distribution depends on a parameter $\tau$ which we estimate from the data rather than as a hyperparameter. In other words, we estimate $\tau$ from the marginal likelihood

$$
m(x|\tau)=\int p(x|\theta)\pi(\theta|\tau)\,d\theta.
$$

Consider the prior $\theta|\tau^{2}\sim N(0,\tau^{2}I_{p})$. Then the Bayes estimator is

$$
\hat{\theta}=\mathbb{E}(\theta|X_{1},\ldots,X_{n})=\frac{n}{n+\frac{1}{\tau^{2}}}\overline{X}=\left(1-\frac{1}{n}\left(\frac{1}{\frac{1}{n}+\tau^{2}}\right)\right)\overline{X}.
$$

Note that we have $X_{i}=\theta+Z_{i}$ where $Z_{i}\overset{\text{iid}}{\sim}N(0,I_{p})$, and $\theta=\tau W$ where $W\sim N(0,I_{p})$, so $X_{i}=\tau W+Z_{i}$ for $i=1,\ldots,n$. This gives

$$
\overline{X}=\tau W+\overline{Z}\sim N\left(0,\left(\tau^{2}+\frac{1}{n}\right)I_{p}\right).
$$

Therefore, 

$$
\frac{\Vert\overline{X}\Vert^{2}}{\tau^{2}+\frac{1}{n}}\sim\chi_{p}^{2}\implies\frac{\tau^{2}+\frac{1}{n}}{\Vert\overline{X}\Vert^{2}}\sim\text{inv-}\chi_{p}^{2}.
$$

Then

$$
\mathbb{E}\left(\frac{\tau^{2}+\frac{1}{n}}{\Vert\overline{X}\Vert^{2}}\right)=\frac{1}{p-2}\implies\mathbb{E}\left(\frac{p-2}{\Vert\overline{X}\Vert^{2}}\right)=\frac{1}{\tau^{2}+\frac{1}{n}},
$$

so $\frac{p-2}{\Vert\overline{X}\Vert^{2}}$ is unbiased estimator of $\frac{1}{\tau^{2}+\frac{1}{n}}$. Thus, the empirical Bayes estimator is

$$
\hat{\theta}_{\text{JS}}=\left(1-\frac{p-2}{n\Vert\overline{X}\Vert^{2}}\right)\overline{X}.
$$

## Risk estimate for the James-Stein estimator

We shall prove that for $p \geq 3$, the James-Stein estimator has strictly smaller risk than the sample mean at every $\theta \in \mathbb{R}^p$. We will need Stein's lemma for the proof.

{{% details title="Stein's Lemma" %}}
If $Z \sim N(0, I_p)$, then we have 

$$
\mathbb{E} [\langle Z, g(Z) \rangle] = \mathbb{E} [\langle \nabla, g(Z) \rangle]
$$

for any $g \in C^1(\mathbb{R}^p ; \mathbb{R}^p)$ for which both expectations exist.
{{% /details %}}

{{% details title="Proof" closed="true" %}}

We will start with the $p=1$ case. Let $\phi(x)=\frac{1}{\sqrt{2\pi}}e^{-x^{2}/2}$. Then $\phi'(x)=-x\phi(x)$, so 

$$
\mathbb{E}[Zg(Z)]=\int xg(x)\phi(x)\,dx=-\int\phi'(x)g(x)\,dx=\int\phi(x)g'(x)\,dx=\mathbb{E}[g'(Z)]
$$

where the second last equality follows from integration by parts. Now suppose that $p > 1$. Then we can write $Z = (Z_1, \ldots, Z_p)$ where $Z_1,\ldots,Z_p$ each follows a standard normal distribution. Then

$$
\begin{aligned}
\mathbb{E}[\langle Z,g(Z)\rangle] &=\sum_{i=1}^{p}\mathbb{E}[Z_{i}g_{i}(Z_{1},\ldots,Z_{p})] \\
	&=\sum_{i=1}^{p}\mathbb{E}[\mathbb{E}[Z_{i}g_{i}(Z_{1},\ldots,Z_{p})|Z_{1},\ldots,Z_{i-1},Z_{i+1},\ldots,Z_{p}]] \\
	&=\sum_{i=1}^{p}\mathbb{E}[\mathbb{E}[\partial_{i}g_{i}(Z_{1},\ldots,Z_{p})|Z_{1},\ldots,Z_{i-1},Z_{i+1},\ldots,Z_{p}]] \\
	&=\sum_{i=1}^{p}\mathbb{E}[\partial_{i}g_{i}(Z_{1},\ldots,Z_{p})] \\
	&=\mathbb{E}[\langle\nabla,g(Z)\rangle],
\end{aligned}
$$

where the third equality follows from the $p=1$ case.

{{% /details %}}
