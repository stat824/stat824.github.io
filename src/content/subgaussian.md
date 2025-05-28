# Basic properties

In the Chernoff bound, the form of the tail depends on the moment generating function $\phi(\lambda),$ so it is natural to define families of random variables according to the growth rate of their moment generating functions. Sub-Gaussian random variables are random variables whose tail behaviour is at least as nice as that of a Gaussian random variable. 

## Definition and basic properties

If $X$ follows a Gaussian distribution with mean $\mu$  and variance $\sigma^{2},$ recall that its moment generating function is

$$
\mathbb{E}[e^{\lambda X}]=e^{\mu\lambda+\frac{\lambda^{2}\sigma^{2}}{2}},\quad\lambda\in\mathbb{R}.
$$

<details title=<details open>
<summary>Definition</summary>

We say a random variable $X$ is $\sigma^{2}$-sub Gaussian if

$$
\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]\leq e^{\frac{\lambda^{2}\sigma^{2}}{2}}\quad\text{for all }\lambda\in\mathbb{R}.
$$

We call $\sigma$ the sub-Gaussian parameter. 

</details>

<details open>
<summary>Example</summary>

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
</details>

More generally, every bounded random variable is sub-Gaussian.

<details open>
<summary>Example</summary>

If $X$ is a bounded random variable such that $X \in [a,b]$ almost surely, then $X$ is sub-Gaussian with parameter $\sigma = \frac{b - a}{2},$ so that

$$
\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]\leq e^{\frac{\lambda^{2}(b-a)^{2}}{8}}\quad\text{for all }\lambda\in\mathbb{R}.
$$

</details>


A linear combination of random sub-Gaussian variables is also sub-Gaussian. 

<details open>
<summary>Proposition</summary>

If $X_{1},\ldots,X_{n}$ are independent sub-Gaussian random variables with parameters $\sigma_{1},\ldots,\sigma_{n},$ then $\sum_{i=1}^{n}a_{i}X_{i}$ is $\sum_{i=1}^{n}a_{i}^{2}\sigma_{i}^{2}$-sub-Gaussian whenever $a_{1},\ldots,a_{n}$ are real constants. 

</details>

<details>
<summary>Proof</summary>

By independence, 

$$
\mathbb{E}\left[e^{\lambda\sum_{i=1}^{n}a_{i}(X_{i}-\mathbb{E}[X_{i}])}\right]=\prod_{i=1}^{n}\mathbb{E}\left[e^{\lambda a_{i}(X_{i}-\mathbb{E}[X_{i}])}\right]\leq\prod_{i=1}^{n}e^{\frac{\lambda^{2}a_{i}^{2}\sigma_{i}^{2}}{2}}=e^{\frac{\lambda^{2}}{2}\sum_{i=1}^{n}a_{i}^{2}\sigma_{i}^{2}}.
$$

</details>

## Chernoff bounds

For a sub-Gaussian variable, we have

$$
\inf_{\lambda\in\mathbb{R}}\left(\log\mathbb{E}[e^{\lambda(X-\mu)}]-\lambda t\right)=\inf_{\lambda\in\mathbb{R}}\left(\frac{\lambda^{2}\sigma^{2}}{2}-\lambda t\right)=-\frac{t^{2}}{2\sigma^{2}}.
$$

This gives the following Chernoff bounds.

<details open>
<summary>Sub-Gaussian Chernoff Bounds</summary>

Suppose that $X \sim \operatorname{subG}(\sigma^2).$ Then for all $t \geq 0,$ we have

$$
\mathbb{P}[X-\mu\geq t]\leq e^{-t^{2}/2\sigma^{2}}, \quad \mathbb{P}[|X-\mu|\geq t]\leq 2e^{-t^{2}/2\sigma^{2}}.
$$

</details>

The two sided bound above follows from the observation that $-X$ is also $\sigma^2$-sub-Gaussian. 

<details open>
<summary>Example</summary>

If $X \in[a,b]$ almost surely, then

$$
\mathbb{P}[X - \mathbb{E}[X] \geq t]\leq\exp\left(-\frac{2t^{2}}{(b-a)^{2}}\right).
$$
</details>

The Chernoff bound leads to the following Hoeffding bound. 

<details open>
<summary>Hoeffding Bounds</summary>

If $X_{1},\ldots,X_{n}$ are independent random variables such that $X_{i}$ is $\sigma_{i}^{2}$-sub-Gaussian, then

$$
\mathbb{P}\left[\frac{1}{n}\sum_{i=1}^{n}(X_{i}-\mathbb{E}[X_{i}])\geq t\right]\leq\exp\left(-\frac{nt^{2}}{\frac{2}{n}\sum_{i=1}^{n}\sigma_{i}^{2}}\right).
$$

</details>

## Moments of sub-Gaussian

We have the following bound on the moments of a sub-Gaussian variable.

<details open>
<summary>Proposition</summary>

Let $X \sim \operatorname{subG}(\sigma^2).$ For any positive integer $k \geq 1,$ we have

$$
\mathbb{E}[|X|^k] \leq (2\sigma^2)^{k/2}k\Gamma(k/2).
$$

In particular, we have $(\mathbb{E}[|X|^k])^{1/k} \leq \sigma e^{1/e} \sqrt{k}$ for all $k \geq 2.$

</details>

<details>
<summary>Proof</summary>

We have

$$
\begin{aligned}
\mathbb{E}[|X|^{k}] &=\int_{0}^{\infty}\mathbb{P}[|X|\geq t^{1/k}]\,dt \\ 
	&\leq2\int_{0}^{\infty}e^{\frac{-t^{2/k}}{2\sigma^{2}}}dt \\
	&=(2\sigma^{2})^{k/2}k\int_{0}^{\infty}e^{-u}u^{k/2-1}du \\
	&=(2\sigma^{2})^{k/2}k\Gamma(k/2),
\end{aligned}
$$

where we used the substitution $u=\frac{1}{2\sigma^{2}}t^{2/k}.$ The second statement follows from $\Gamma(k/2)\leq(k/2)^{k/2}$ and $k^{1/k}\leq e^{1/e}$ for any $k\geq2.$
</details>


## Sub-Gaussian vectors and matrices

We can also talk about sub-Gaussian random vectors and matrices. 

<details open>
<summary>Definition</summary>

* A random vector $X\in\mathbb{R}^{n}$ is said to be $\sigma^{2}$-sub-Gaussian if $u^{T}(X-\mathbb{E}[X]) \sim \operatorname{subG}(\sigma^{2})$ for any $u\in\mathcal{S}^{n-1}.$ We write $X\sim\operatorname{subG}_{n}(\sigma^{2}).$
* A random matrix $X\in\mathbb{R}^{m\times n}$ is said to be $\sigma^{2}$-sub-Gaussian if $u^{T}(X-\mathbb{E}[X])v \sim \operatorname{subG}(\sigma^{2})$ for any $u\in\mathcal{S}^{m-1}$ and $v\in\mathcal{S}^{n-1}.$ We write $X\sim\operatorname{subG}_{m\times n}(\sigma^{2}).$

</details>

## Equivalent characterizations

Next, we note that there are several equivalent characterizations of sub-Gaussian variables. 

<details open>
<summary>Theorem</summary>

Suppose that $X$ is a random variable with zero mean. The following are equivalent:

1. There is a constant $\sigma \geq 0$ such that $\mathbb{E}[e^{\lambda X}]\leq e^{\frac{\lambda^{2}\sigma^{2}}{2}}$ for all $\lambda\in\mathbb{R}.$

2. There is a constant $c\geq1$ and a Gaussian random variable $Z\sim N(0,\tau^{2})$ such that $\mathbb{P}[|X|\geq s]\leq c\mathbb{P}[|Z|\geq s]$ for all $s\geq0.$

3. There is a constant $\theta\geq0$ such that $\mathbb{E}[X^{2k}]\leq\frac{(2k)!}{2^{k}k!}\theta^{2k}$ for all $k=1,2,\ldots$

4. There is a constant $\sigma\geq0$ such that $\mathbb{E}[e^{\lambda X^{2}}]\leq\frac{1}{\sqrt{1-2\lambda \sigma^2}}$ for all $0 \leq \lambda < \frac{1}{2\sigma^2}.$ 

</details>
