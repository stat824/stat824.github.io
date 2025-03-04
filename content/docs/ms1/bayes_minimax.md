---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Bayes and Minimax Estimators'
weight: 4
---

{{< callout type="warning" >}}
  Add in proof that Bayes estimators are not unbiased unless average risk is zero. 
{{< /callout >}}


Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}P_{\theta}$, and let $\widehat{\theta}=\widehat{\theta}(X_{1},\ldots,X_{n})$ be an estimator of the parameter $\theta$. Let $L(\widehat{\theta},\theta)$ be a loss function which quantifies the accuracy of the estimator. Then the risk function is

$$
R(\widehat{\theta},\theta)=\mathbb{E}_{\theta}L(\widehat{\theta},\theta)=\int L(\widehat{\theta}(x),\theta)p(x|\theta)\,dx.
$$

In other words, $R(\widehat{\theta},\theta)$ is the average deviation of $\widehat{\theta}$ from the true parameter value if the true parameter value is taken to be $\theta$.


{{% details title="Rao-Blackwell Theorem" %}}
Assume $L(\widehat{\theta},\theta)$ is convex in $\widehat{\theta}$. For any $\widehat{\theta}$ and any sufficient $T$, define $\widetilde{\theta}=\mathbb{E}_{\theta}(\widehat{\theta}|T)$. Then $R(\widetilde{\theta},\theta)\leq R(\widehat{\theta},\theta)$.
{{% /details %}}

{{% details title="Proof" closed="true" %}}
By Jensen's inequality, we have $L(\widetilde{\theta},\theta)=L(\mathbb{E} _ {\theta}(\widehat{\theta}|T),\theta)\leq \mathbb{E} _ {\theta}(L(\widehat{\theta},\theta)|T)$, and taking expectation of both sides gives $R(\widetilde{\theta},\theta)\leq R(\widehat{\theta},\theta)$.
{{% /details %}}


Given a prior $\pi$ on $\Theta$, we say $\widehat{\theta}_\pi$ is a Bayes estimator for $\pi$ if 

$$
\widehat{\theta}_\pi = \argmin_{\widehat{\theta}}\int_{\Theta}R(\widehat{\theta},\theta)\pi(\theta)\,d\theta.
$$

We say $\widehat\theta$ is a minimax estimator if 

$$
\widehat{\theta}=\argmin_{\widehat{\theta}}\sup_{\theta\in\Theta}R(\widehat{\theta},\theta).
$$

We have

$$
\int R(\widehat{\theta},\theta)\pi(\theta)\,d\theta=\int\int L(\widehat{\theta}(x),\theta)p(x|\theta)\pi(\theta)\,dx\,d\theta=\int\int L(\widehat{\theta}(x),\theta)\pi(\theta|x)\,d\theta\,m(x)\,dx,
$$

where $\pi(\theta|x)$ is the posterior density and $m(x) = \int p(x|\theta)\pi(\theta) \, d\theta$  is the marginal of $X$. 

{{% details title="Claim" %}}
Given a prior $\pi$, the Bayes estimator is given by

$$
\widehat{\theta}_{\pi}(X)=\argmin_{a}\int L(a,\theta)\pi(\theta|X)\,d\theta.
$$

{{% /details %}}

{{% details title="Proof" closed="true" %}}
For any estimator $\widehat{\theta}$, we have

$$
\begin{aligned}
\int R(\widehat{\theta}_{\pi},\theta)\pi(\theta)\,d\theta &=\int\int L(\widehat{\theta}_{\pi}(x),\theta)\pi(\theta|x)\,d\theta\,m(x)\,dx \\
	&\leq\int\int L(\widehat{\theta}(x),\theta)\pi(\theta|x)\,d\theta\,m(x)\,dx \\
	&=\int R(\widehat{\theta},\theta)\pi(\theta)\,d\theta.
\end{aligned}
$$
{{% /details %}}

As an example, consider $\Theta\subseteq\mathbb{R}$ and $L(\widehat{\theta},\theta)=(\widehat{\theta}-\theta)^{2}$. Then 

$$
\widehat{\theta}_{\pi}(X)=\argmin_{a}\int(a-\theta)^{2}\pi(\theta|X)\,d\theta=\argmin_{a}\mathbb{E}\left((a-\theta)^{2}|X\right)=\mathbb{E}(\theta|X).
$$

{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Ber}(p)$, and let $L(\hat{p},p)=(\hat{p}-p)^{2}$. Consider the prior $\pi\sim\text{Beta}(\alpha,\beta)$, so $\pi(p)\propto p^{\alpha-1}(1-p)^{\beta-1}$. Then

$$
p|X_{1},\ldots,X_{n}\sim\text{Beta}\left(\sum_{i=1}^{n}X_{i}+\alpha,\sum_{i=1}^{n}(1-X_{i})+\beta\right).
$$

A Bayes estimator is then

$$
\hat{p}=\mathbb{E}(p|X_{1},\ldots,X_{n})=\frac{\sum_{i=1}^{n}X_{i}+\alpha}{n+\alpha+\beta}.
$$

The risk is

$$
\begin{aligned}
R(\hat{p},p)=\mathbb{E}_{p}(\hat{p}-p)^{2} &=\operatorname{Var}(\hat{p})+(\mathbb{E}(\hat{p})-p)^{2} \\
	&=\left(\frac{n}{n+\alpha+\beta}\right)^{2}\frac{p(1-p)}{n}+\left(\frac{\alpha+\beta}{\alpha+\beta+n}\right)^{2}\left(\frac{\alpha}{\alpha+\beta}-p\right)^{2}.
\end{aligned}
$$
{{< /callout >}}


{{% details title="Theorem" %}}
If there exists a prior $\pi$ such that $\widehat{\theta}$ satisfies 

$$
\sup_{\theta\in\Theta}R(\widehat{\theta},\theta)=\inf_{\widetilde{\theta}}\int R(\widetilde{\theta},\theta)\pi(\theta)\,d\theta,
$$

then $\widehat{\theta}$ is minimax. 
{{% /details %}}

{{% details title="Proof" closed="true" %}}
For all $\widetilde{\theta}$, we have

$$
\sup_{\theta\in\Theta}R(\widetilde{\theta},\theta)\geq\int R(\widetilde{\theta},\theta)\pi(\theta)\,d\theta\geq\inf_{\widetilde{\theta}}\int R(\widetilde{\theta},\theta)\pi(\theta)\,d\theta=\sup_{\theta\in\Theta}R(\widehat{\theta},\theta).
$$
{{% /details %}}


{{% details title="Corollary" %}}
If $\widehat{\theta}=\widehat{\theta}_{\pi}$ for some $\pi$ and $R(\widehat{\theta} _{\pi},\theta)$ is constant over $\theta\in\Theta$, then $\widehat{\theta}$ is minimax. 
{{% /details %}}



{{% details title="Proof" closed="true" %}}
We have

$$
\sup_{\theta\in\Theta}R(\widehat{\theta},\theta)=\int R(\widehat{\theta},\theta)\pi(\theta)\,d\theta=\inf_{\widetilde{\theta}}\int R(\widetilde{\theta},\theta)\pi(\theta)\,d\theta,
$$

so by the theorem we have that $\widehat{\theta}$ is minimax. 

{{% /details %}}



In other words, a Bayes estimator with constant risk is minimax. This fact is usually the first line of attack when finding minimax estimators.

{{< callout >}}

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Ber}(p)$, and let $L(\hat{p},p)=(\hat{p}-p)^{2}$. Recall that for the prior $\pi\sim\text{Beta}(\alpha,\beta)$ we have the Bayes estimator

$$
\hat{p}=\mathbb{E}(p|X_{1},\ldots,X_{n})=\frac{\sum_{i=1}^{n}X_{i}+\alpha}{n+\alpha+\beta}.
$$

The risk is 

$$
R(\hat{p},p)=\mathbb{E}_{p}(\hat{p}-p)^{2}=\left(\frac{n}{n+\alpha+\beta}\right)^{2}\frac{p(1-p)}{n}+\left(\frac{\alpha+\beta}{\alpha+\beta+n}\right)^{2}\left(\frac{\alpha}{\alpha+\beta}-p\right)^{2},
$$

which can be written as 

$$
\left(\left(\frac{\alpha+\beta}{n+\alpha+\beta}\right)^{2}-\frac{1}{n}\left(\frac{n}{n+\alpha+\beta}\right)^{2}\right)p^{2}+\left(\frac{1}{n}\left(\frac{n}{n+\alpha+\beta}\right)^{2}-\left(\frac{\alpha+\beta}{n+\alpha+\beta}\right)^{2}\frac{2\alpha}{\alpha+\beta}\right)p+\left(\frac{\alpha+\beta}{n+\alpha+\beta}\right)^{2}\left(\frac{\alpha}{\alpha+\beta}\right)^{2}. 
$$

If $\alpha=\beta=\frac{\sqrt{n}}{2}$, then the coefficients of the $p$ and $p^{2}$ terms vanish, and the risk becomes

$$
R(\hat{p},p)=\frac{1}{4(\sqrt{n}+1)^{2}}
$$

which is constant with respect to $p$. Therefore, 

$$
\hat{p}_{\text{minimax}}=\frac{\sum_{i=1}^{n}X_{i}+\frac{\sqrt{n}}{2}}{n+\sqrt{n}}
$$

is a minimax estimator. How does this estimator compare to the maximum likelihood estimator $\hat{p} _ {\text{MLE}}=\overline{X}$? The risk function for the MLE estimator is 

$$
R(\hat{p}_{\text{MLE}},p)=\mathbb{E}_{p}(\hat{p}_{\text{MLE}}-p)^{2}=\frac{p(1-p)}{n}.
$$

There are some situations where the MLE has lower risk, for example when $p $is close to 0 or 1. However, if we consider the worst case, we find that

$$
\sup_{p\in(0,1)}R(\hat{p}_{\text{MLE}},p)=\frac{1}{4n}
$$

which is larger than 

$$
\sup_{p\in(0,1)}R(\hat{p}_{\text{minimax}},p)=\frac{1}{4(\sqrt{n}+1)^{2}}.
$$ 
{{< /callout >}}



The choice of loss function is important. Let us demonstrate this with another example. 

{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Ber}(p)$, and let $L(\hat{p},p)=\frac{(\hat{p}-p)^{2}}{p(1-p)}$. For the prior $\pi(p)=1$, the Bayes estimator is

$$
\begin{aligned}
\hat{p}(X) &= \argmin_{a} \int \frac{(a-p)^{2}}{p(1-p)} \pi(p|X)\,dp \\ 
	&=\argmin_{a}\int(a-p)^{2}\frac{\pi(p|X)}{p(1-p)}\,dp,
\end{aligned}
$$
where 

$$
\frac{\pi(p|X)}{p(1-p)}\propto p^{\sum_{i=1}^{n}X_{i}-1}(1-p)^{\sum_{i=1}^{n}(X_{i}-1)-1}=\text{Beta}\left(\sum_{i=1}^{n}X_{i},\sum_{i=1}^{n}(1-X_{i})\right),
$$

so

$$
\hat{p}(X)=\frac{\sum_{i=1}^{n}X_{i}}{\sum_{i=1}^{n}X_{i}+\sum_{i=1}^{n}(1-X_{i})}=\overline{X}=\hat{p}_{\text{MLE}}.
$$

The risk is 

$$
R(\hat{p},p) =\frac{\mathbb{E}_{p}(\hat{p}-p)^{2}}{p(1-p)}=\frac{1}{n}
$$

which is constant. Therefore, $\overline{X}$ is a Bayes estimator (which cannot be the case with the squared loss function because only biased estimators could be Bayes), and it is also a minimax estimator. 
{{< /callout >}}

{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\mu,\sigma^{2})$ where $\mu\in\mathbb{R}$ is the parameter to be estimated. Consider the loss function $L(\hat{\mu},\mu)=(\hat{\mu}-\mu)^{2}$. Then the estimator $\overline{X}$ cannot be Bayes as it is unbiased, but is it minimax? This is true intuitively because the risk $R(\overline{X},\mu)=\mathbb{E} _ {\mu}(\overline{X}-\mu)^{2}=\frac{\sigma^{2}}{n}$ is constant. To prove this formally, consider the prior $\pi\sim N(0,\tau^{2})$. Then the Bayes estimator for this prior is

$$
\hat{\mu}_{\text{Bayes}}=\mathbb{E}(\mu|X)=\frac{\frac{n}{\sigma^{2}}}{\frac{1}{\tau^{2}}+\frac{n}{\sigma^{2}}}\overline{X},
$$

and the risk is

$$
\begin{aligned}
R(\hat{\mu}_{\text{Bayes}},\mu) &= \text{Var}(\hat{\mu}_{\text{Bayes}})+(\mathbb{E}\hat{\mu}_{\text{Bayes}}-\mu)^{2} \\ 
	&=\left(\frac{\frac{n}{\sigma^{2}}}{\frac{1}{\tau^{2}}+\frac{n}{\sigma^{2}}}\right)^{2}\frac{\sigma^{2}}{n}+\left(\frac{\frac{1}{\tau^{2}}}{\frac{1}{\tau^{2}}+\frac{n}{\sigma^{2}}}\right)^{2}\mu^{2}.
\end{aligned}
$$

The Bayes risk is

$$
\int R(\hat{\mu}_{\text{Bayes}},\mu)\pi(\mu)\,d\mu=\left(\frac{\frac{n}{\sigma^{2}}}{\frac{1}{\tau^{2}}+\frac{n}{\sigma^{2}}}\right)^{2}\frac{\sigma^{2}}{n}+\left(\frac{\frac{1}{\tau^{2}}}{\frac{1}{\tau^{2}}+\frac{n}{\sigma^{2}}}\right)^{2}\tau^{2}=\frac{1}{\frac{1}{\tau^{2}}+\frac{n}{\sigma^{2}}}.
$$

Then for any estimator $\hat{\mu}$, we have 

$$
R(\hat{\mu},\mu)\geq\int R(\hat{\mu},\mu)\pi(\mu)\,d\mu\geq\inf_{\hat{\mu}}\int R(\hat{\mu},\mu)\pi(\mu)\,d\mu=\frac{1}{\frac{1}{\tau^{2}}+\frac{n}{\sigma^{2}}}.
$$

Letting $\tau\to\infty$, we get $R(\hat{\mu},\mu)\geq\frac{\sigma^{2}}{n}=R(\overline{X},\mu)$.
{{< /callout >}}

{{% details title="Theorem" %}}
If there exists a sequence of priors $(\pi_{m})$ such that 

$$
\sup_{\theta\in\Theta}R(\hat{\theta},\theta)=\lim_{m\to\infty}\inf_{\hat{\theta}}\int R(\hat{\theta},\theta)\pi_{m}(\theta)\,d\theta,
$$

then $\hat{\theta}$ is minimax. 
{{% /details %}}

The proof follows from the same argument as in the above example.
