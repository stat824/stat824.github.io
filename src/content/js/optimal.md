# Oracle inequality

Let us now consider the estimator $\widehat{\theta} _ {c}=c\overline{X}$ where $c$ is to be determined. We want to find $c^{\ast}$ which minimizes $R(\widehat{\theta} _ {c},\theta)$. We have

$$
R(\widehat{\theta} _ {c},\theta) = \mathbb{E} _ {\theta}\Vert c\overline{X}-c\theta\Vert^{2}+\Vert c\theta-\theta\Vert^{2}=c^{2}\frac{p}{n}+(c-1)^{2}\Vert\theta\Vert^{2},
$$

so

$$
\frac{d}{dc}R(\widehat{\theta}_{c},\theta)=2c\frac{p}{n}+2(c-1)\Vert\theta\Vert^{2}\implies c^{\ast}=\frac{\Vert\theta\Vert^{2}}{\frac{p}{n}+\Vert\theta\Vert^{2}}.
$$

<details open>
<summary>Definition</summary>

The estimator 

$$
\widehat{\theta}_{c^{\ast}}=\frac{\Vert\theta\Vert^{2}}{\frac{p}{n}+\Vert\theta\Vert^{2}}\overline{X}=\left(1-\frac{p}{p+n\Vert\theta\Vert^{2}}\right)\overline{X}
$$

is called the optimal shrinkage estimator, also known as the oracle estimator. 

</details>

This is not an estimator in the true sense because it depends on the true parameter. The risk function is

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

<details open>
<summary>Oracle Inequality</summary>

For every $\theta \in \mathbb{R}^p$, we have

$$
R(\widehat{\theta}_{\mathrm{JS}},\theta)\leq R(\widehat{\theta}_{c^\ast},\theta)+\frac{2}{n} \leq \min\left(\frac{p}{n},\Vert\theta\Vert^{2}\right) + \frac{2}{n}.
$$
</details>


<details>
<summary>Proof</summary>

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

</details>


It is worth noting that $\frac{2}{n}$ is independent of the dimension $p$, so even in high dimensions the James-Stein estimator performs very closely to the optimal shrinkage estimator as long as the sample size is sufficiently large. 