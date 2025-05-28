# Maximum over a finite set

We first consider maximum over a finite set of sub-Gaussian variables. 

<details open>
<summary>Theorem</summary>

Let $X_{1},\ldots,X_{N}$ be random variables such that $X_{i}\sim\operatorname{subG}(\sigma^{2}).$ Then

$$
\mathbb{E}\left[\max_{1\leq i\leq N}X_{i}\right]\leq\sigma\sqrt{2\log N}\quad\text{and}\quad\mathbb{E}\left[\max_{1\leq i\leq N}|X_{i}|\right]\leq\sigma\sqrt{2\log(2N)}.
$$

Moreover, for any $t>0,$ 

$$
\mathbb{P}\left[\max_{1\leq i\leq N}X_{i}>t\right]\leq Ne^{-\frac{t^{2}}{2\sigma^{2}}}\quad\text{and}\quad\mathbb{P}\left[\max_{1\leq i\leq N}|X_{i}|>t\right]\leq2Ne^{-\frac{t^{2}}{2\sigma^{2}}}.
$$

</details>

<details>
<summary>Proof</summary>

For all $s>0,$ we have

$$
\begin{aligned}
\mathbb{E}\left[\max_{1\leq i\leq N}X_{i}\right] &= \frac{1}{s}\mathbb{E}\left[\log\left(e^{s\max_{1\leq i\leq N}X_{i}}\right)\right] \\
	&\leq\frac{1}{s}\log\left(\mathbb{E}\left[e^{\max_{1\leq i\leq N}sX_{i}}\right]\right) \\
	&\leq\frac{1}{s}\log\left(\sum_{i=1}^{N}\mathbb{E}[e^{sX_{i}}]\right) \\
	&\leq\frac{1}{s}\log\left(\sum_{i=1}^{N}e^{\frac{s^{2}\sigma^{2}}{2}} \\\right)=\frac{\log(N)}{s}+\frac{s\sigma^{2}}{2}.
\end{aligned}
$$

Differentiating the upper bound with respect to $s$ and setting the derivative to 0, we find that $s=\sqrt{2\log(N)/\sigma^{2}}$ yields the tightest bound. This gives 

$$
\mathbb{E}\left[\max_{1\leq i\leq N}X_{i}\right]\leq\sigma\sqrt{2\log N}.
$$

 For the tail probability, we have

$$
\mathbb{P}\left[\max_{1\leq i\leq N}X_{i}>t\right]=\mathbb{P}\left[\bigcup_{i=1}^{N}\{X_{i}>t\}\right]\leq\sum_{i=1}^{N}\mathbb{P}[X_{i}>t]\leq Ne^{-\frac{t^{2}}{2\sigma^{2}}}.
$$

The inequalities for $\max_{1\leq i\leq N}|X_{i}|$ follow by noting that $\max_{1\leq i\leq N}|X_{i}|=\max_{1\leq i\leq2N}X_{i}$ where we have set $X_{N+i}=-X_{i}.$

</details>

