# Hodges' estimator

Although the maximum likelihood estimator achieves the Cramer-Rao lower bound, it is possible to find estimators that have lower asymptotic variance at at least one point. Suppose that $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\theta,1)$ and consider Hodges' estimator, given by

$$
\widehat{\theta}_{H}=\begin{cases}
\overline{X} & |\overline{X}|>n^{-1/4},\\
0 & |\overline{X}|\leq n^{-1/4}.
\end{cases}
$$

<details open>
<summary>Proposition</summary>

It holds that

$$
\sqrt{n}(\widehat{\theta}_{H}-\theta)\rightsquigarrow\begin{cases}
N(0,1) & \text{if }\theta\neq0,\\
0 & \text{if }\theta=0.
\end{cases}
$$
</details>

<details>
<summary>Proof</summary>

Since $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\theta,1),$ we have $\overline{X}=\theta+\frac{1}{\sqrt{n}}Z$ where $Z\sim N(0,1).$ Then we can write 

$$
\begin{aligned}
\widehat{\theta}_{H} &= \overline{X}1(|\overline{X}|>n^{-1/4}) \\
	&=(\theta+\frac{1}{\sqrt{n}}Z)1(|\theta+\frac{1}{\sqrt{n}}Z|>n^{-1/4}) \\
	&=\theta-\theta1(|\theta+\frac{1}{\sqrt{n}}Z|\leq n^{-1/4})+\frac{1}{\sqrt{n}}Z1(|\theta+\frac{1}{\sqrt{n}}Z|>n^{-1/4}).
\end{aligned}
$$

This gives

$$
\sqrt{n}(\widehat{\theta}_{H}-\theta) =-\sqrt{n}\theta1(|\sqrt{n}\theta+Z|\leq n^{1/4})+Z1(|\sqrt{n}\theta+Z|>n^{1/4}).
$$

Consider the two cases:

* If $\theta\neq0,$ then for every $\omega\in\Omega$ there exists $N(\omega)$ such that $|\sqrt{n}\theta+Z(\omega)|>n^{1/4}$ for all $n\geq N(\omega).$ Therefore, $1(|\sqrt{n}\theta+Z|\leq n^{1/4})$ converges to 0 almost surely, and we have $-\sqrt{n}\theta1(|\sqrt{n}\theta+Z|\leq n^{1/4})\to0$ since it is eventually 0. The complementary indicator $1(|\sqrt{n}\theta+Z|>n^{1/4})$ converges to 1, so Slutsky's theorem implies $\sqrt{n}(\widehat{\theta}_{H}-\theta)$ converges in distribution to $Z\sim N(0,1).$

* If $\theta=0,$ then clearly we have $\sqrt{n}(\widehat{\theta}_{H}-\theta)=Z1(|Z|>n^{1/4})\rightsquigarrow0. $
</details>

Thus, asymptotically Hodges' estimator performs as well as the maximum likelihood estimator when $\theta\neq0,$ and even better when $\theta=0.$ Such an estimator is called superefficient and the point 0 is called a superefficient point. 
