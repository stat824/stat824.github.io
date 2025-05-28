# Basic tail inequalities

Concentration inequalities are inequalities of the form $\mathbb{P}[X\geq t]\leq\phi(t)$ where $\phi$ goes to zero (rapidly) as $t\to\infty.$ Often, we will deal with concentration inequalities of the form $\mathbb{P}[\overline{X} _ {n} \geq t]\leq\phi _ {n}(t)$ where $\overline{X} _ n = \frac{1}{n} \sum_{i = 1}^n X_i$ is the mean of independent samples. The most basic concentration inequality is the classical Markov's inequality. 

<details open>
<summary>Markov's Inequality</summary>

If $X\geq0$ almost surely, then we have

$$
\mathbb{P}[X\geq t]\leq \frac{\mathbb{E}[X]}{t} \quad \text{for all } t > 0.
$$

</details>

<details>
<summary>Proof</summary>

We have $\mathbb{E}[X] = \mathbb{E}[X 1 _ {\{X<t\}}] + \mathbb{E}[X 1 _ {\{ X\geq t\}}]
	\geq\mathbb{E}[X1 _ {\{X\geq t\}}]
	\geq t\mathbb{P}[X\geq t].$

</details>


If $X$ is square integrable, we have also have Chebyshev's inequality. 

<details open>
<summary>Chebyshev's Inequality</summary>

If $X\in L^{2}(\Omega),$ then 

$$
\mathbb{P}[|X-\mathbb{E}[X]|\geq t]\leq\frac{\operatorname{Var}(X)}{t^{2}} \quad \text{for all t>0.}
$$ 

</details>

Chebyshev's inequality follows by applying Markov's inequality to $Z=(X-\mathbb{E}[X])^{2}.$ There are also higher moment analogues:

$$
\mathbb{P}[|X-\mathbb{E}[X]|\geq t]\leq\frac{\mathbb{E}(|X-\mathbb{E}[X]|^{k})}{t^{k}}
$$

which holds for all $k \geq 1.$ Moreover, if $X$ has a moment generating function in a neighbourhood of 0, so that there exists $b>0$ such that $\phi(\lambda)=\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]$ exists for all $|\lambda|\leq b,$ then Markov's inequality implies

$$
\mathbb{P}[X-\mathbb{E}[X]\geq t]=\mathbb{P}[e^{\lambda(X-\mathbb{E}[X])}\geq e^{\lambda t}]\leq\frac{\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]}{e^{\lambda t}}.
$$

This holds for all $|\lambda|\leq b$, and optimizing it with respect to $\lambda$ gives the Chernoff bound.

<details open>
<summary>Chernoff Bound</summary>

If $\phi(\lambda)=\mathbb{E}[e^{\lambda(X-\mathbb{E}[X])}]$ exists for all $|\lambda|\leq b,$ then

$$
\log\mathbb{P}[X-\mathbb{E}[X]\geq t]\leq\inf_{|\lambda|\leq b}\left(\log \phi(\lambda)-\lambda t\right).
$$
</details>

