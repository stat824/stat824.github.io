---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Sub-exponential Random Variables'
weight: 3
---
We now consider a class of random variables which are allowed to have heavier tails than sub-Gaussian variables. To motivate the definition, let us suppose that $X$ has the double exponential or Laplace distribution with parameter 1, so that $\mathbb{P}[|X|\geq t]\leq e^{-t}$ for all $t\geq0.$ The tails of this distribution do not decay as fast as the Gaussian ones. This tail behavior is captured by the moment generating function, which is given by

$$
\mathbb{E}[e^{\lambda X}]=\frac{1}{1-\lambda^{2}}\leq e^{2\lambda^{2}}\quad\text{for all }|\lambda|<1.
$$

So the moment generating function of the Laplace distribution is bounded by that of a Gaussian in a neighborhood of 0 but does not exist everywhere on the real line. It turns out that all distributions that have tails at most as heavy as that of a Laplace distribution satisfy such a property.

{{% details title="Lemma" %}}

Let $X$ be a random variable with mean zero such that $\mathbb{P}[|X|\geq t]\leq2e^{-2t/b}$ for some $b>0.$ Then for every positive integer $k\geq1,$ $\mathbb{E}[|X|^{k}]\leq b^{k}k!$ and $(\mathbb{E}[|X|^{k}])^{1/k}\leq2bk.$ Moreover, the moment generating function of $X$ satisfies

$$
\mathbb{E}[e^{\lambda X}]\leq e^{2\lambda^{2}b^{2}}\quad\text{for all }|\lambda|\le\frac{1}{2b}.
$$

{{% /details %}}

{{% details title="Proof" closed="true" %}}

We have

$$
\begin{aligned}
\mathbb{E}[|X|^{k}] &= \int_{0}^{\infty}\mathbb{P}[|X|^{k}\geq t]\,dt \\
	&=\int_{0}^{\infty}\mathbb{P}[|X|\geq t^{1/k}]\,dt \\
	&\leq2\int_{0}^{\infty}e^{-2t^{1/k}/b}\,dt \\
	&=2k\left(\frac{b}{2}\right)^{k}\int_{0}^{\infty}e^{-u}u^{k-1}\,du \\
	&\leq b^{k}k\Gamma(k).
\end{aligned}
$$

Since $k\Gamma(k)=k!,$ we have $\mathbb{E}[|X|^{k}]\leq b^{k}k!.$ Also, $\Gamma(k)\leq k^{k}$ and $k^{1/k}\leq e^{1/2}\leq2$ for $k\geq1,$ so $(\mathbb{E}[|X|^{k}])^{1/k}\leq(b^{k}k\Gamma(k))^{1/k}\leq2bk.$ For the MGF, we use its expansion. By the dominated convergence theorem, for any $s$ with $|s|\leq\frac{1}{2b},$ 

$$
\begin{aligned}
\mathbb{E}[e^{sX}] &\leq 1+\sum_{k=2}^{\infty}\frac{|s|^{k}\mathbb{E}[|X|^{k}]}{k!} \\
	&\leq1+\sum_{k=2}^{\infty}(|s|b)^{k} \\
	&=1+(|s|b)^{2}\sum_{k=0}^{\infty}(|s|b)^{k} \\
	&\leq1+2(|s|b)^{2} \\
	&\leq e^{2s^{2}b^{2}}.
\end{aligned}
$$
{{% /details %}}

## Definition and basic properties

{{% details title="Definition" %}}

We say a random variable $X$ is $(\tau^{2},b)$-sub-exponential if there exist non-negative numbers $\tau^2$ and $b$ such that

$$
\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]\leq e^{\frac{\lambda^{2}\tau^{2}}{2}}\quad\text{for all }|\lambda| < \frac{1}{b}.
$$
{{% /details %}}

It follows directly from this definition that sub-Gaussian variables are sub-exponential.

{{< callout >}}
**Example.** Let $Z\sim N(0,1).$ Consider $X=Z^{2} \sim \chi^2.$ Then for $\lambda<\frac{1}{2},$ 

$$
\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]=\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty}e^{\lambda(z^{2}-1)}e^{-z^{2}/2}\,dz=\frac{e^{-\lambda}}{\sqrt{1-2\lambda}}.\
$$

The integral does not converge if $\lambda>\frac{1}{2},$ so this variable is not sub-Gaussian. However, in a neighborhood of 0, we find that

$$
\frac{e^{-\lambda}}{\sqrt{1-2\lambda}}\leq e^{2\lambda^{2}}=e^{4\lambda^{2}/2},
$$

so $X\sim\chi^{2}$ is sub-exponential.
{{< /callout >}}

To verify that a random variable is sub-exponential, we can explicitly bound the moment generating function, but this can sometimes be impractical. Another way to verify that a random variable is sub-exponential is by recognizing it as a sum of independent sub-exponential variables.

{{% details title="Proposition" %}}

Let $X_{1},\ldots,X_{n}$ be independent random variables such that $X_i$ is $(\tau_i^2, b_i)$-sub-exponential, and let $a_1,\ldots,a_n \in \mathbb{R}.$ Then $\sum_{i=1}^{n}a_i X_{i}$ is $(\sum_{i=1}^{n}a_i^2 \tau_{i}^{2},\max_{i}|a_i b_i|)$-sub-exponential. 

{{% /details %}}

## Chernoff bound for sub-exponential variables 

Let us derive the Chernoff bound for sub-exponential variables. Assume that $X$ is $(\tau^{2},b)$-sub-exponential. For $t \geq 0$, define $g(\lambda,t)=\frac{\lambda^{2}\tau^{2}}{2}-\lambda t$ and $g^{\ast}(t)=\inf_{\lambda\in[0,1/b)}g(\lambda,t).$ We have

$$
\inf_{|\lambda| < 1/b}\left(\log\mathbb{E}[e^{\lambda(X - \mathbb{E}[X])}]-\lambda t\right) \leq g^\ast(t).
$$

The unconstrained minimum of $g(\lambda,t)$ occurs at $\lambda^{\ast}=\frac{t}{\tau^{2}}.$ If $\frac{t}{\tau^{2}}<\frac{1}{b}\iff t<\frac{\tau^{2}}{b},$ then this unconstrained optimum corresponds to the constrained minimum as well, so that $g^{\ast}(t)=g(\frac{t}{\tau^{2}},t)=-\frac{t^{2}}{2\tau^{2}}.$ Otherwise, if $t\geq\frac{\tau^{2}}{b},$ since the function $g(\lambda,t)$ is monotonically decreasing in the interval $[0,\lambda^{\ast}),$ the constrained minimum is achieved at the boundary point $\lambda^{\dagger}=\frac{1}{b},$ and we have $g^{\ast}(t)=-\frac{t}{b}+\frac{1}{2b}\frac{\tau^{2}}{b}\leq-\frac{t}{2b}.$ This yields the tail bound

$$
\mathbb{P}[X-\mathbb{E}[X]\geq t]\leq\begin{cases}
e^{-\frac{t^{2}}{2\tau^{2}}} & \text{if }0\leq t\leq\frac{\tau^{2}}{b}\\
e^{-\frac{t}{2b}} & \text{if }t>\frac{\tau^{2}}{b}
\end{cases}=e^{-\min\left\{ \frac{t^{2}}{2\tau^{2}},\frac{t}{2b}\right\} }.
$$

Since $-X$ is also sub-exponential, we also have the two-sided inequality

$$
\mathbb{P}[|X-\mathbb{E}[X]|\geq t]\leq2e^{-\min\left\{ \frac{t^{2}}{2\tau^{2}},\frac{t}{2b}\right\} }.
$$

## Bernstein's condition

Another method to verify that a random variable is sub-exponential is to verify Bernstein’s condition, which controls the central moments. We say that Bernstein's condition with parameter $b$ holds if

$$
\left|\mathbb{E}[(X-\mu)^{k}]\right|\leq\frac{1}{2}k!b^{k-2}\sigma^{2}\quad\text{for }k=2,3,4,\ldots 
$$

where $\mu=\mathbb{E}[X]$ and $\sigma^{2}=\operatorname{Var}[X].$ A sufficient condition for this to hold is for the variable to be bounded. 

{{% details title="Proposition" %}}
If $X$ satisfies Bernstein's condition with parameter $b$, then $X$ is $(\sqrt{2}\sigma,2b)$-sub-exponential. 
{{% /details %}}

{{% details title="Proof" closed="true" %}}

To see this, for $|\lambda|<\frac{1}{b},$ we expand the moment generating function to get

$$
\begin{aligned}
\mathbb{E}[e^{\lambda(X-\mu)}] &= 1+\frac{\lambda^{2}\sigma^{2}}{2}+\sum_{k=3}^{\infty}\lambda^{k}\frac{\mathbb{E}[(X-\mu)^{k}]}{k!} \\
	&\leq1+\frac{\lambda^{2}\sigma^{2}}{2}+\frac{\lambda^{2}\sigma^{2}}{2}\sum_{k=3}^{\infty}(|\lambda|b)^{k-2} \\
	&\leq1+\frac{\lambda^{2}\sigma^{2}}{2}\frac{1}{1-b|\lambda|} \\
	&\leq e^{\frac{\lambda^{2}\sigma^{2}}{2(1-b|\lambda|)}}.
\end{aligned}
$$

If $|\lambda|<\frac{1}{2b},$ then $e^{\frac{\lambda^{2}\sigma^{2}}{2(1-b|\lambda|)}}\leq e^{\lambda^{2}\sigma^{2}}=e^{\frac{\lambda^{2}(\sqrt{2}\sigma)^{2}}{2}},$ so $X$ is $(\sqrt{2}\sigma,2b)$-sub-exponential. 
{{% /details %}}

{{% details title="Bernstein-type bound" %}}
If $X$ satisfies Bernstein's condition with parameter $b,$ then

$$
\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]\leq e^{\frac{\lambda^{2}\sigma^{2}}{2(1-b|\lambda|)}}\quad\text{for all }|\lambda|\leq\frac{1}{b}
$$

where $\sigma^{2}=\operatorname{Var}[X],$ and we have the concentration inequality 

$$
\mathbb{P}[X-\mathbb{E}[X]\geq t]\leq e^{-\frac{t^{2}}{2(\sigma^{2}+bt)}}\quad\text{for all }t\geq0.
$$
{{% /details %}}

{{% details title="Proof" closed="true" %}}
The first statement is what we just proved. The second statement follows from setting $\lambda=\frac{t}{bt+\sigma^{2}}\in[0,\frac{1}{b}]$ in the Chernoff bound $\mathbb{P}[X-\mathbb{E}[X]\geq t]\leq e^{-\lambda t}\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]$ and then applying the bound on the moment generating function.
{{% /details %}}

{{< callout type="info" >}}
This leads to interesting observations for a bounded random variable $X$ satisfying $|X|\leq b.$ Note that in this case, we can use either the Bernstein type bound to control the tail behaviour, or we could also use the Hoeffding bound. Recall that the Hoeffding bound gives

$$
\mathbb{P}\left[|X-\mathbb{E}[X]|\geq t\right]\leq2e^{-\frac{t^{2}}{2b^{2}}}.
$$

Since $\sigma^{2}\leq b^{2},$ the Bernstein bound is always sharper.
{{< /callout >}}

## One-sided Bernstein's inequality

We know that bounded variables satisfy the Bernstein condition, but what about variables that are only bounded above by a positive constant? We will show that a similar one-sided bound holds in this case. One-sided here refers to the fact that a two-sided version does not necessarily hold, unlike the concentration inequalities we have considered so far. 

{{% details title="One-sided Bernstein's inequality" %}}
If $X-\mathbb{E}[X]\leq b$ almost surely, then

$$
\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]\leq\exp\left(\frac{\lambda^{2}\sigma^{2}}{2(1-\frac{b\lambda}{3})}\right)\quad\text{for all }\lambda\in[0,3/b)
$$

where $\sigma^{2}=\operatorname{Var}[X].$ Consequently, given independent random variables $X_{1},\ldots,X_{n}$ such that $X_{i}-\mathbb{E}[X_{i}]\leq b$ almost surely, we have

$$
\mathbb{P}\left[\sum_{i=1}^{n}(X_{i}-\mathbb{E}[X_{i}])\geq n\delta\right]\leq\exp\left(-\frac{n\delta^{2}}{2\left(\frac{1}{n}\sum_{i=1}^{n}\sigma_{i}^{2}+\frac{b\delta}{3}\right)}\right).
$$
{{% /details %}}

{{% details title="Proof" closed="true" %}}

To prove it, define $h(u)=2\frac{e^{u}-u-1}{u^{2}}=2\sum_{k=2}^{\infty}\frac{u^{k-2}}{k!}.$ Then 

$$
\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]=1+\frac{1}{2}\lambda^{2}\mathbb{E}[(X-\mathbb{E}[X])^{2}h(\lambda(X-\mathbb{E}[X]))].
$$

For all $x\in(-\infty,0),$ $x'\in[0,b],$ and $\lambda>0,$ we have

$$
h(\lambda x)\leq h(0)\leq h(\lambda x')\leq h(\lambda b).
$$

Since $X-\mathbb{E}[X]\leq b,$ we have $\mathbb{E}[(X-\mathbb{E}[X])^{2}h(\lambda(X-\mathbb{E}[X]))]\leq\sigma^{2}h(\lambda b)$ and hence

$$
\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]	\leq1+\frac{\lambda^{2}\sigma^{2}}{2}h(\lambda b)\leq e^{\lambda^{2}\sigma^{2}h(\lambda b)/2}.
$$

It remains to show that $h(\lambda b)\leq(1-\frac{\lambda b}{3})^{-1}$ for $0\leq\lambda b<3.$ Since $k!\geq2\times3^{k-2}$ for all $k\geq2,$ we have

$$
h(\lambda b)=2\sum_{k=2}^{\infty}\frac{(\lambda b)^{k-2}}{k!}\leq\sum_{k=2}^{\infty}\left(\frac{\lambda b}{3}\right)^{k-2}=\frac{1}{1-\frac{\lambda b}{3}}
$$

since $\frac{\lambda b}{3}\in[0,1).$ To prove the concentration inequality, we use the Chernoff bound

$$
\begin{aligned}
\mathbb{P}\left[\sum_{i=1}^{n}(X_{i}-\mathbb{E}[X_{i}])\geq n\delta\right]&\leq e^{-\lambda n\delta}\mathbb{E}[e^{\lambda\sum_{i=1}^{n}(X_{i}-\mathbb{E}[X_{i}])}] \\ &\leq\exp\left(-\lambda n\delta+\frac{\lambda^{2}\sum_{i=1}^{n}\sigma_{i}^{2}}{2(1-\frac{\lambda b}{3})}\right).
\end{aligned}
$$

Substituting in $\lambda=\frac{n\delta}{\sum_{i=1}^{n}\sigma_{i}^{2}+\frac{b\delta}{3}}\in[0,\frac{3}{b})$ and simplifying yields the desired bound.
{{% /details %}}

## Characterizations of sub-exponential variables
We consider several equivalent characterizations of sub-exponential variables.
{{% details title="Proposition" %}}
Suppose that $X$ is a random variable with zero mean. The following are equivalent:

1. There are non-negative real numbers $(\nu,\alpha)$ such that

	$$
\mathbb{E}[e^{\lambda X}]\leq e^{\nu^{2}\lambda^{2}/2}\quad\text{for all }|\lambda|\leq\frac{1}{\alpha}.
$$

2. There is a constant $c_{0}>0$ such that $\mathbb{E}[e^{\lambda X}]<\infty$ for all $|\lambda|\leq c_{0}.$ 

3. There are constants $c_{1},c_{2}>0$ such that

	$$
\mathbb{P}[|X|\geq t]\leq c_{1}e^{-c_{2}t}\quad\text{for all }t\geq0.
$$

4. $\sup_{k\geq1}\left(\frac{\mathbb{E}[|X|^{k}]}{k!}\right)^{1/k}<\infty .$
{{% /details %}}

For an $\mathbb{R}$-valued random variable $X,$ define its Orlicz 1-norm to be

$$
\Vert X\Vert_{\psi_1}:=\inf\{t\in\mathbb{R}_{+}:\mathbb{E}[\exp(|X|/t)]\leq2\}.
$$

This norm characterizes sub-exponentiality.  

{{% details title="Proposition" %}}

We have $\Vert X\Vert_{\psi_1} <\infty$ if and only if $X$ is sub-exponential. Moreover:
* We have the concentration inequality $\mathbb{P}[|X| \geq t] \leq 2e^{-t / \Vert X\Vert_{\psi_1}}.$
* If $X$ is $(\tau^2, b)$-sub-exponential with zero mean, then $\Vert X \Vert_{\psi_2}$ and $\tau$ differ by an absolute constant factor. 

{{% /details %}}
