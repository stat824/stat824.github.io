---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Sub-Gaussian Random Variables'
weight: 2
---
The form of the tail depends on the growth rate of the moment generating function $\phi(\lambda),$ so it is natural to define families of random variables according to their moment generating functions, which controls how nice their tail behaviour is. Sub-Gaussian random variables are random variables whose tail behaviour is at least as nice as that of a Gaussian random variable. 

## Definition and basic properties

If $X$ follows a Gaussian distribution with mean $\mu$  and variance $\sigma^{2},$ recall that its moment generating function is

$$
\mathbb{E}[e^{\lambda X}]=e^{\mu\lambda+\frac{\lambda^{2}\sigma^{2}}{2}},\quad\lambda\in\mathbb{R}.
$$

Then we say a random variable $X$ is $\sigma^{2}$-sub Gaussian if

$$
\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]\leq e^{\frac{\lambda^{2}\sigma^{2}}{2}}\quad\text{for all }\lambda\in\mathbb{R}.
$$

We call $\sigma$ the sub-Gaussian parameter. 

{{< callout >}}
Suppose that $\epsilon$ is a Rademacher random variable. Then

$$
\begin{aligned}
\mathbb{E}[e^{\lambda X}] &= \frac{e^{\lambda}+e^{-\lambda}}{2} \\
	&= \sum_{k=0}^{\infty}\frac{\lambda^{2k}}{(2k)!} \\
	&\leq 1+\sum_{k=1}^{\infty}\frac{\lambda^{2k}}{2^{k}k!} \\
	&\leq e^{\lambda^{2}/2},
\end{aligned}
$$

which shows that Rademacher random variables are sub-Gaussian with parameter $\sigma = 1.$ 
{{< /callout >}}

{{< callout >}}
If $X$ is a bounded random variable such that $X \in [a,b]$ almost surely, then $X$ is sub-Gaussian with parameter $\sigma = \frac{b - a}{2},$ so that

$$
\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]\leq e^{\frac{\lambda^{2}(b-a)^{2}}{8}}\quad\text{for all }\lambda\in\mathbb{R}.
$$

See homework for proof. 
{{< /callout >}}

A linear combination of random sub-Gaussian variables is also sub-Gaussian. 

{{% details title="Proposition" %}}

If $X_{1},\ldots,X_{n}$ are independent sub-Gaussian random variables with parameters $\sigma_{1},\ldots,\sigma_{n},$ then $\sum_{i=1}^{n}a_{i}X_{i}$ is $\sum_{i=1}^{n}a_{i}^{2}\sigma_{i}^{2}$-sub-Gaussian whenever $a_{1},\ldots,a_{n}$ are real constants. 

{{% /details %}}

{{% details title="Proof" closed="true" %}}

By independence, 

$$
\mathbb{E}\left[e^{\lambda\sum_{i=1}^{n}a_{i}(X_{i}-\mathbb{E}[X_{i}])}\right]=\prod_{i=1}^{n}\mathbb{E}\left[e^{\lambda a_{i}(X_{i}-\mathbb{E}[X_{i}])}\right]\leq\prod_{i=1}^{n}e^{\frac{\lambda^{2}a_{i}^{2}\sigma_{i}^{2}}{2}}=e^{\frac{\lambda^{2}}{2}\sum_{i=1}^{n}a_{i}^{2}\sigma_{i}^{2}}.
$$

{{% /details %}}

## Chernoff and Hoeffding bounds

For a sub-Gaussian variable, we have

$$
\inf_{\lambda\in\mathbb{R}}\left(\log\mathbb{E}[e^{\lambda(X-\mu)}]-\lambda t\right)=\inf_{\lambda\in\mathbb{R}}\left(\frac{\lambda^{2}\sigma^{2}}{2}-\lambda t\right)=-\frac{t^{2}}{2\sigma^{2}},
$$

giving the Chernoff bound

$$
\mathbb{P}[X-\mu\geq t]\leq e^{-t^{2}/2\sigma^{2}}\quad\text{for all }t>0.
$$

As a corollary, we have the following Hoeffding bounds. 

{{% details title="Hoeffding bounds" %}}

If $X_{1},\ldots,X_{n}$ are independent sub-Gaussian random variables with parameters $\sigma_{1},\ldots,\sigma_{n},$ then

$$
\mathbb{P}\left[\frac{1}{n}\sum_{i=1}^{n}(X_{i}-\mathbb{E}[X_{i}])\geq t\right]\leq\exp\left(-\frac{nt^{2}}{\frac{2}{n}\sum_{i=1}^{n}\sigma_{i}^{2}}\right).
$$

In particular, if $X_{i}\in[a,b]$ almost surely for all $i$, then

$$
\mathbb{P}\left[\frac{1}{n}\sum_{i=1}^{n}(X_{i}-\mathbb{E}[X_{i}])\geq t\right]\leq\exp\left(-\frac{2nt^{2}}{(b-a)^{2}}\right).
$$

{{% /details %}}

## Characterizations of sub-Gaussian variables

Next, we consider several equivalent characterizations of sub-Gaussian variables. 

{{% details title="Theorem" %}}

Suppose that $X$ is a random variable with zero mean. The following are equivalent:

1. There is a constant $\sigma^2 > 0$ such that $\mathbb{E}[e^{\lambda X}]\leq e^{\frac{\lambda^{2}\sigma^{2}}{2}}$ for all $\lambda\in\mathbb{R}.$

2. There is a constant $c\geq1$ and a Gaussian random variable $Z\sim N(0,\tau^{2})$ such that $\mathbb{P}[|X|\geq s]\leq c\mathbb{P}[|Z|\geq s]$ for all $s\geq0.$

3. There is a constant $\theta\geq0$ such that $\mathbb{E}[X^{2k}]\leq\frac{(2k)!}{2^{k}k!}\theta^{2k}$ for all $k=1,2,\ldots$

4. There is a constant $\sigma\geq0$ such that $\mathbb{E}[e^{\frac{sX^{2}}{2\sigma^{2}}}]\leq\frac{1}{\sqrt{1-s}}$ for all $s\in[0,1).$ 

{{% /details %}}

**Proof of $(1) \Longrightarrow (2)$:** We will show that if $X$ is $\sigma^{2}$-sub-Gaussian with zero mean, then 

$$
\frac{\mathbb{P}[X\geq t]}{\mathbb{P}[Z\geq t]}\leq4\sqrt{\pi}e\quad\text{for all }t\geq0.
$$

Firstly, by the Chernoff bound for sub-Gaussian variables, we have $\mathbb{P}[X\geq t]\leq e^{-t^{2}/2\sigma^{2}}.$ Then using a property for Gaussian variables (called the Mills-ratio for Gaussian tails, see homework), we have

$$
\mathbb{P}[Z\geq t]\geq\left(\frac{\sqrt{2}\sigma}{t}-\frac{(\sqrt{2}\sigma)^{3}}{t^{3}}\right)\frac{1}{\sqrt{2\pi}}e^{-t^{2}/4\sigma^{2}}.
$$

Consider two cases:

1. If $t\in[0,2\sigma]$, then

	$$
\mathbb{P}[Z\geq t]\geq\mathbb{P}[Z\geq2\sigma]\geq\left(\frac{1}{\sqrt{2}}-\frac{1}{2\sqrt{2}}\right)\frac{1}{\sqrt{2\pi}}e^{-1}=\frac{1}{4\sqrt{\pi}e}.
$$

	Since $\mathbb{P}[X\geq t]\leq1,$ it follows that

	$$
\frac{\mathbb{P}[X\geq t]}{\mathbb{P}[Z\geq t]}\leq4\sqrt{\pi}e.
$$

2. If $t>2\sigma,$ then combining the Mills ratio and the sub-Gaussian tail bound, 

	$$
\sup_{t>2\sigma}\frac{\mathbb{P}[X\geq t]}{\mathbb{P}[Z\geq t]}\leq\sup_{s>2}\frac{e^{-s^{2}/4}}{\left(\frac{\sqrt{2}}{s}-\frac{2\sqrt{2}}{s^{3}}\right)}\sqrt{2\pi}\leq\sup_{s>2}\frac{\sqrt{2\pi}s^{3}e^{-s^{2}/4}}{2\sqrt{2}}\leq4\sqrt{\pi}e.
$$

Finally, note that if $X$ is $\sigma^{2}$-sub-Gaussian, then so is $-X.$ Applying the same argument to $-X$ and adding the two bounds yields $\mathbb{P}[|X|\geq t]\leq8\sqrt{\pi}e\mathbb{P}[Z\geq t]=4\sqrt{\pi}e\mathbb{P}[|Z|\geq t]$ for all $t\geq0.$

**Proof of $(2) \Longrightarrow  (3)$:** Since $X^{2k}$ is a non-negative random variable, we have

$$
\mathbb{E}[X^{2k}]=\int_{0}^{\infty}\mathbb{P}[|X|\geq s^{1/2k}]\,ds\leq c\int_{0}^{\infty}\mathbb{P}[|Z|\geq s^{1/2k}]=c\mathbb{E}[Z^{2k}].
$$

By property of the normal distribution, we have $\mathbb{E}[Z^{2k}]=\frac{(2k)!}{2^{k}k!}\tau^{2k},$ so 

$$
\mathbb{E}[X^{2k}]\leq c\frac{(2k)!}{2^{k}k!}\tau^{2k}\leq\frac{(2k)!}{2^{k}k!}\theta^{2k}
$$

where $\theta=c\tau.$

**Proof of $(3) \Longrightarrow  (1)$:** For $\lambda\in\mathbb{R},$ 

$$
\mathbb{E}[e^{\lambda X}]=1+\sum_{k=2}^{\infty}\frac{\lambda^{k}\mathbb{E}[X^{k}]}{k!}.
$$

If $X$ is symmetric about 0, then the odd moments vanish, giving 

$$
\mathbb{E}[e^{\lambda X}]=\sum_{k=0}^{\infty}\frac{|\lambda|^{2k}\mathbb{E}[|X|^{2k}]}{(2k)!}\leq\sum_{k=0}^{\infty}\frac{|\lambda|^{2k}}{(2k)!}\frac{(2k)!}{2^{k}k!}\theta^{2k}\leq e^{\lambda^{2}\theta^{2}/2}.
$$

If $X$ is not symmetric, then by the Cauchy-Schwarz inequality we have

$$
\mathbb{E}[|\lambda X|^{2k+1}]\leq\sqrt{\mathbb{E}[|\lambda X|^{2k}]\mathbb{E}[|\lambda X|^{2k+2}]}\leq\frac{1}{2}(\mathbb{E}[|\lambda X|^{2k}]+\mathbb{E}[|\lambda X|^{2k+2}])
$$

where the last inequality follows from the AM-GM inequality. This bounds the odd moments in terms of the even moments. Then 


$$
\begin{aligned}
\mathbb{E}[e^{\lambda X}] &\leq1+\sum_{k=2}^{\infty}\frac{|\lambda|^{k}\mathbb{E}[|X|^{k}]}{k!} \\
	&\leq1+\sum_{k=1}^{\infty}\left(\frac{1}{(2k)!}+\frac{1}{2}\left(\frac{1}{(2k-1)!}+\frac{1}{(2k+1)!}\right)\right)\mathbb{E}[|\lambda X|^{2k}],
\end{aligned}
$$

and we have

$$
\mathbb{E}[e^{\lambda X}]\leq\sum_{k=0}^{\infty}2^{k}\frac{\lambda^{2k}\mathbb{E}[X^{2k}]}{(2k)!}\leq\sum_{k=0}^{\infty}2^{k}\frac{\lambda^{2k}}{(2k)!}\frac{(2k)!}{2^{k}k!}\theta^{2k}=e^{\lambda^{2}\theta^{2}/2}.
$$

**Proof of $(1) \Longrightarrow  (4)$:** The result holds trivially when $s=0,$ so assume $s\in(0,1).$ Then we multiply the sub-Gaussian inequality by $e^{-\lambda^{2}\sigma^{2}/2s}$ to obtain

$$
\mathbb{E}[e^{\lambda X-\frac{\lambda^{2}\sigma^{2}}{2s}}]\leq e^{\frac{\lambda^{2}\sigma^{2}(s-1)}{2s}}.
$$

This holds for all $\lambda\in\mathbb{R},$ so we can integrating both sides with respect to $\lambda.$ On the right hand side, we have

$$
\int_{-\infty}^{\infty}e^{\frac{\lambda^{2}\sigma^{2}(s-1)}{2s}}\,d\lambda=\frac{1}{\sigma}\sqrt{\frac{2\pi s}{1-s}}.
$$

On the left hand side, using Fubini's theorem, we have

$$
\int_{-\infty}^{\infty}\mathbb{E}[e^{\lambda X-\frac{\lambda^{2}\sigma^{2}}{2s}}]\,d\lambda=\mathbb{E}\left[\int_{-\infty}^{\infty}e^{\lambda X-\frac{\lambda^{2}\sigma^{2}}{2s}}\,d\lambda\right]=\frac{\sqrt{2\pi s}}{\sigma}\mathbb{E}[e^{\frac{sX^{2}}{2\sigma^{2}}}].
$$

Therefore, $\mathbb{E}[e^{\frac{sX^{2}}{2\sigma^{2}}}]\leq\frac{\sigma}{\sqrt{2\pi s}}\frac{1}{\sigma}\sqrt{\frac{2\pi s}{1-s}}=\frac{1}{\sqrt{1-s}}.$

**Proof of $(4) \Longrightarrow  (1)$:** We apply the bound $e^{u}\leq u+e^{9u^{2}/16}$ with $u=\lambda X$ to obtain

$$
\mathbb{E}[e^{\lambda X}]\leq\mathbb{E}[\lambda X]+\mathbb{E}[e^{\frac{9\lambda^{2}X^{2}}{16}}]=\mathbb{E}[e^{\frac{sX^{2}}{2\sigma^{2}}}]\leq\frac{1}{\sqrt{1-s}},
$$

which is valid whenever $s=\frac{9}{8}\lambda^{2}\sigma^{2}$ is less than 1. Since $s\leq\frac{1}{2}$ when $|\lambda|\leq\frac{2}{3\sigma}$ and $\frac{1}{\sqrt{1-s}}\leq e^{s}$ for $s\in[0,\frac{1}{2}],$ it follows that

$$
\mathbb{E}[e^{\lambda X}]\leq e^{\frac{9}{8}\lambda^{2}\sigma^{2}}\quad\text{for }|\lambda|\leq\frac{2}{3\sigma}.
$$

To show a similar bound for $|\lambda|\geq\frac{2}{3\sigma},$ we use a special case of the Fenchel-Young inequality which states that

$$
uv\leq\frac{u^{2}}{2\alpha}+\frac{\alpha v^{2}}{2}\quad\text{for all }u,v\in\mathbb{R}\text{ and }\alpha>0.
$$

Choosing $u=\lambda, v=X, \alpha=c/\sigma^{2}$ gives

$$
\mathbb{E}[e^{\lambda X}]\leq\mathbb{E}[e^{\lambda^{2}\sigma^{2}/(2c)+cX^{2}/2\sigma^{2}}]=e^{\lambda^{2}\sigma^{2}/(2c)}\mathbb{E}[e^{\frac{cX^{2}}{2\sigma^{2}}}].
$$

If $c\in(0,1/2),$ then we have $\mathbb{E}[e^{\frac{cX^{2}}{2\sigma^{2}}}]\leq\frac{1}{\sqrt{1-c}}\leq e^{c}.$ Letting $c=1/4$ and using the fact that $\frac{1}{4}\leq\frac{9}{16}\lambda^{2}\sigma^{2}$ holds whenever $|\lambda|\geq\frac{2}{3\sigma},$ it follows that

$$
\mathbb{E}[e^{\lambda X}]\leq e^{2\lambda^{2}\sigma^{2}}e^{1/4}\leq e^{2\lambda^{2}\sigma^{2}+\frac{9}{16}\lambda^{2}\sigma^{2}}\leq e^{3\lambda^{2}\sigma^{2}}.
$$

Therefore, we have $\mathbb{E}[e^{\lambda X}]\leq e^{3\lambda^{2}\sigma^{2}}$ for all $\lambda\in\mathbb{R}.$

## Sub-Gaussian vectors and matrices

We can also talk about sub-Gaussian random vectors and matrices. 

* A random vector $X\in\mathbb{R}^{n}$ is said to be $\sigma^{2}$-sub-Gaussian if $u^{T}(X-\mathbb{E}[X])$ is $\sigma^{2}$-sub-Gaussian for any vector $u\in\mathcal{S}^{n-1}.$ We write $X\sim\operatorname{subG}_{n}(\sigma^{2}).$
* A random matrix $X\in\mathbb{R}^{m\times n}$ is said to be $\sigma^{2}$-sub-Gaussian if $u^{T}(X-\mathbb{E}[X])v$ is $\sigma^{2}$-sub-Gaussian for any vector $u\in\mathcal{S}^{m-1}$ and $v\in\mathcal{S}^{n-1}.$ We write $X\sim\operatorname{subG}_{m\times n}(\sigma^{2}).$