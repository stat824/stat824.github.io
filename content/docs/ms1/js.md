---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'James-Stein and Optimal Shrinkage Estimators'
weight: 6
---

Let $X_{1},\ldots,X_{n}\overset{\mathrm{i.i.d.}}{\sim}N(\theta,I_{p})$ where $\theta\in\mathbb{R}^{p}$, and consider the loss function $L(\widehat{\theta},\theta)=\Vert\widehat{\theta}-\theta\Vert^{2}$. As we have seen, the sample mean $\overline{X}$ is not admissible for $p \geq 3$. The James-Stein estimator gives an example of an estimator which has strictly smaller risk than $\overline{X}$. It is defined as

$$
\widehat{\theta}_{\text{JS}}=\left(1-\frac{p-2}{n\Vert\overline{X}\Vert^{2}}\right)\overline{X}.
$$

## James-Stein estimator as an empirical Bayes estimator
 
This estimator can be derived from the empirical Bayes perspective. In empirical Bayes, the prior distribution depends on a parameter $\tau$ which we estimate from the data rather than as a hyperparameter. In other words, we estimate $\tau$ from the marginal likelihood

$$
m(x|\tau)=\int p(x|\theta)\pi(\theta|\tau)\,d\theta.
$$

Consider the prior $\theta|\tau^{2}\sim N(0,\tau^{2}I_{p})$. Then the Bayes estimator is

$$
\widehat{\theta}=\mathbb{E}(\theta|X_{1},\ldots,X_{n})=\frac{n}{n+\frac{1}{\tau^{2}}}\overline{X}=\left(1-\frac{1}{n}\left(\frac{1}{\frac{1}{n}+\tau^{2}}\right)\right)\overline{X}.
$$

Note that we have $X_{i}=\theta+Z_{i}$ where $Z_{i}\overset{\text{i.i.d.}}{\sim}N(0,I_{p})$, and $\theta=\tau W$ where $W\sim N(0,I_{p})$, so $X_{i}=\tau W+Z_{i}$ for $i=1,\ldots,n$. This gives

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
\widehat{\theta}_{\text{JS}}=\left(1-\frac{p-2}{n\Vert\overline{X}\Vert^{2}}\right)\overline{X}.
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

{{% details title="Theorem" %}}

Let $p \geq 3$. Then 

$$
\mathbb{E}_{\theta}\Vert\widehat{\theta}_{\mathrm{JS}}-\theta\Vert^{2}<\frac{p}{n}=\mathbb{E}_{\theta}\Vert\overline{X}-\theta\Vert^{2}
$$

for all $\theta\in\mathbb{R}^{p}$.

{{% /details %}}


Let us write $\overline{X}=\frac{1}{\sqrt{n}}(\mu+Z)$ where $Z\sim N(0,I_{p})$ and $\mu=\sqrt{n}\theta$. We have

$$
\begin{aligned}
\mathbb{E}_{\theta}\Vert\widehat{\theta}_{\mathrm{JS}}-\theta\Vert^{2} &=\mathbb{E}_{\theta}\left\Vert \left(1-\frac{p-2}{n\Vert\overline{X}\Vert^{2}}\right)\overline{X}-\theta\right\Vert ^{2} \\
	&=\mathbb{E}_{\theta}\left\Vert \overline{X}-\theta-\frac{p-2}{n\Vert\overline{X}\Vert^{2}}\overline{X}\right\Vert ^{2} \\
	&=\mathbb{E}_{\theta}\left\Vert \frac{1}{\sqrt{n}}Z-\frac{p-2}{\Vert\mu+Z\Vert^{2}}\frac{1}{\sqrt{n}}(\mu+Z)\right\Vert ^{2} \\
	&=\frac{1}{n}\mathbb{E}_{\theta}\left\Vert Z-\frac{p-2}{\Vert\mu+Z\Vert^{2}}(\mu+Z)\right\Vert ^{2} \\
	&=\frac{1}{n}\left(\mathbb{E}_{\theta}\Vert Z\Vert^{2}+\mathbb{E}_{\theta}\frac{(p-2)^{2}}{\Vert\mu+Z\Vert^{2}}-2(p-2)\mathbb{E}_{\theta}\left\langle Z,\frac{\mu+Z}{\Vert\mu+Z\Vert^{2}}\right\rangle \right).
\end{aligned}
$$

We have 

$$
\mathbb{E}_{\theta}\left\langle Z,\frac{\mu+Z}{\Vert\mu+Z\Vert^{2}}\right\rangle =\mathbb{E}_{\theta}\langle Z,g(Z)\rangle,
$$

where $g_{j}(z)=\frac{\mu_{j}+z_{j}}{\Vert\mu+z\Vert^{2}}$. Computing the derivative gives

$$
\frac{\partial}{\partial z_{j}}g_{j}(z)=\frac{\Vert\mu+z\Vert^{2}-2(\mu_{j}+z_{j})^{2}}{\Vert\mu+z\Vert^{4}},
$$

so by Stein's lemma we have

$$
\begin{aligned}
\mathbb{E}_{\theta}\left\langle Z,\frac{\mu+Z}{\Vert\mu+Z\Vert^{2}}\right\rangle  &=\sum_{j=1}^{p}\mathbb{E}_{\theta}\frac{\partial}{\partial z_{j}}g_{j}(Z) \\
	&=\sum_{j=1}^{p}\mathbb{E}_{\theta}\frac{\Vert\mu+Z\Vert^{2}-2(\mu_{j}+Z_{j})^{2}}{\Vert\mu+Z\Vert^{4}} \\
	&=\mathbb{E}_{\theta}\frac{(p-2)\Vert\mu+Z\Vert^{2}}{\Vert\mu+Z\Vert^{4}} \\
	&=\mathbb{E}_{\theta}\frac{p-2}{\Vert\mu+Z\Vert^{2}}.
\end{aligned}
$$

Then 

$$
\begin{aligned}
\mathbb{E}_{\theta}\Vert\widehat{\theta}_{\mathrm{JS}}-\theta\Vert^{2} &= \frac{1}{n}\left(\mathbb{E}_{\theta}\Vert Z\Vert^{2}+\mathbb{E}_{\theta}\frac{(p-2)^{2}}{\Vert\mu+Z\Vert^{2}}-2(p-2)\mathbb{E}_{\theta}\left\langle Z,\frac{\mu+Z}{\Vert\mu+Z\Vert^{2}}\right\rangle \right). \\
	&=\frac{1}{n}\left(p-(p-2)^{2}\mathbb{E}_{\theta}\frac{1}{\Vert\mu+Z\Vert^{2}}\right) \\
	&<\frac{p}{n}.
\end{aligned}
$$

We see that 

$$
R(\widehat{\theta}_{\text{JS}},\theta)=\frac{1}{n}\left(p-(p-2)^{2}\mathbb{E}_{\theta}\frac{1}{\Vert\sqrt{n}\theta+Z\Vert^{2}}\right),\quad Z\sim N(0,1).
$$

By symmetry, $R(\widehat{\theta} _ {\text{JS}},\theta)$ depends only on the magnitude of $\theta$, and we have 

$$
\lim_{\Vert\theta\Vert\to\infty}R(\widehat{\theta}_{\text{JS}},\theta)=\frac{p}{n},\quad\text{so }\sup_{\theta\in\mathbb{R}^{p}}R(\widehat{\theta}_{\text{JS}},\theta)=\sup_{\theta\in\mathbb{R}^{p}}R(\overline{X},\theta).
$$

## Optimal shrinkage estimator

Let us now consider the estimator $\widehat{\theta} _ {c}=c\overline{X}$ where $c$ is to be determined. We want to find $c^{\ast}$ which minimizes $R(\widehat{\theta} _ {c},\theta)$. We have

$$
R(\widehat{\theta} _ {c},\theta) = \mathbb{E} _ {\theta}\Vert c\overline{X}-c\theta\Vert^{2}+\Vert c\theta-\theta\Vert^{2}=c^{2}\frac{p}{n}+(c-1)^{2}\Vert\theta\Vert^{2},
$$

so

$$
\frac{d}{dc}R(\widehat{\theta}_{c},\theta)=2c\frac{p}{n}+2(c-1)\Vert\theta\Vert^{2}\implies c^{\ast}=\frac{\Vert\theta\Vert^{2}}{\frac{p}{n}+\Vert\theta\Vert^{2}}.
$$

The estimator 

$$
\widehat{\theta}_{c^{\ast}}=\frac{\Vert\theta\Vert^{2}}{\frac{p}{n}+\Vert\theta\Vert^{2}}\overline{X}=\left(1-\frac{p}{p+n\Vert\theta\Vert^{2}}\right)\overline{X}
$$

is called the optimal shrinkage estimator, also known as the oracle estimator. This is not an estimator in the true sense because it depends on the true parameter. The risk function is

$$
\begin{aligned}
R(\widehat{\theta}_{c^{\ast}},\theta) &= \left(\frac{b}{a+b}\right)^{2}a+\left(\frac{a}{a+b}\right)^{2}b \\ 
&=\frac{b^{2}a+a^{2}b}{(a+b)^{2}} \\
&=\frac{ab}{a+b} \\
&=\frac{\frac{p}{n}\Vert\theta\Vert^{2}}{\frac{p}{n}+\Vert\theta\Vert^{2}} \\
&\leq\min\left(\frac{p}{n},\Vert\theta\Vert^{2}\right),
\end{aligned}
$$

where $a=\frac{p}{n}$ and $b=\Vert\theta\Vert^{2}$. The James-Stein estimator is nearly optimal in the following sense.

{{% details title="Oracle Inequality" %}}

For every $\theta \in \mathbb{R}^p$, we have

$$
R(\widehat{\theta}_{\mathrm{JS}},\theta)\leq R(\widehat{\theta}_{c^\ast},\theta)+\frac{2}{n} \leq \min\left(\frac{p}{n},\Vert\theta\Vert^{2}\right) + \frac{2}{n}.
$$
{{% /details %}}

Recall that

$$
R(\widehat{\theta}_{\mathrm{JS}},\theta)=\frac{1}{n}\left(p-(p-2)^{2}\mathbb{E}\frac{1}{\Vert\sqrt{n}\theta+Z\Vert^{2}}\right),\quad Z\sim N(0,1).
$$

Note that $\Vert Z+\sqrt{n}\theta\Vert^2 \sim\chi_{p,n\Vert\theta\Vert^{2}}^{2}\overset{d}{=}\chi_{p+2N}^{2}$ where $N\sim\text{Poisson}\left(\frac{n\Vert\theta\Vert^{2}}{2}\right)$, so

$$
\mathbb{E}\frac{1}{\Vert\sqrt{n}\theta+Z\Vert^{2}}=\mathbb{E}\frac{1}{\chi_{p+2N}^{2}}=\mathbb{E}\frac{1}{p+2N-2}\geq\frac{1}{\mathbb{E}(p+2N-2)}=\frac{1}{p+n\Vert\theta\Vert^{2}-2}.
$$

Therefore, 

$$
\begin{aligned}
R(\widehat{\theta}_{\mathrm{JS}},\theta) &\leq\frac{1}{n}\left(p-\frac{(p-2)^{2}}{p+n\Vert\theta\Vert^{2}-2}\right) \\
	&=\frac{1}{n}\frac{np\Vert\theta\Vert^{2}+2(p-2)}{p+n\Vert\theta\Vert^{2}-2} \\
	&=\frac{1}{n}\left(2+\frac{(p-2)\Vert\theta\Vert^{2}}{p-2+n\Vert\theta\Vert^{2}}\right) \\
	&=\frac{2}{n}+\frac{\frac{p-2}{n}\Vert\theta\Vert^{2}}{\frac{p-2}{n}+\Vert\theta\Vert^{2}}  \\
	&\leq\frac{2}{n}+R(\widehat{\theta}_{c^{\ast}},\theta).
\end{aligned}
$$


It is worth noting that $\frac{2}{n}$ is independent of the dimension $p$, so even in high dimensions the James-Stein estimator performs very closely to the optimal shrinkage estimator as long as the sample size is sufficiently large. 