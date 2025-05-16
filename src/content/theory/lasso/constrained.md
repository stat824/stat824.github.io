# Restricted eigenvalue conditions and constrained lasso

Suppose that we observe $Y\in\mathbb{R}^{n}$ and a matrix $X\in\mathbb{R}^{n\times d}$ such that

$$
Y=X\theta^{\ast}+\epsilon
$$

where $X\in\mathbb{R}^{n\times d}$ is a deterministic design matrix and $\epsilon$ is sub-Gaussian noise with independent components. A natural extension of the basis pursuit program is based on minimizing 

$$
\frac{1}{2n}\Vert Y-X\theta\Vert_{2}^{2}+\lambda_{n}\Vert\theta\Vert_{1},
$$

where $\lambda_{n}>0$ is a hyperparameter. This is called the Lasso program. Alternatively, one can consider different constrained forms of the Lasso, either

$$
\min_{\theta\in\mathbb{R}^{d}}\left\{ \frac{1}{2n}\Vert Y-X\theta\Vert_{2}^{2}:\Vert\theta\Vert_{1}\leq R\right\} \quad\text{for some }R>0,
$$

or 

$$
\min_{\theta\in\mathbb{R}^{d}}\left\{ \Vert\theta\Vert_{1}:\frac{1}{2n}\Vert Y-X\theta\Vert_{2}^{2}\leq b^{2}\right\} \quad\text{for some }b>0.
$$

These are called the relaxed basis pursuit programs. By Lagrangian duality theory, all three families of convex programs are equivalent. 

<details open>
<summary>Definition</summary>

For $\alpha\geq1$ and $S\subset[d],$ define $\mathbb{C}_{\alpha}(S):= \{\Delta\in\mathbb{R}^{d}:\Vert\Delta_{S^{c}}\Vert_{1}\leq\alpha\Vert\Delta_{S}\Vert_{1}\}.$ We say that $X\in\mathbb{R}^{n\times d}$ satisfies the restricted eigenvalue condition over $S\subset[d]$ with parameters $(\alpha,\mu)$ if

$$
\frac{1}{n}\Vert X\Delta\Vert_{2}^{2}\geq\mu\Vert\Delta\Vert_{2}^{2}\quad\text{for all }\Delta\in\mathbb{C}_{\alpha}(S).
$$
</details>

From where does the restricted eigenvalue condition arise? The answer is given by the following result.

<details open>
<summary>Theorem</summary>

Let $b=\Vert\theta^{\ast}\Vert_{1}$ and suppose that we solve

$$
\widehat{\theta}\in\argmin_{\theta\in\mathbb{R}^{d}}\left\{ \frac{1}{2}\Vert Y-X\theta\Vert_{2}^{2}:\Vert\theta\Vert_{1}\leq b\right\} .
$$

If $X\in\mathbb{R}^{n\times d}$ satisfies the $\operatorname{RE}(1,\mu)$ condition over $S=\operatorname{supp}(\theta^{\ast})$ and the columns of $X$ are normalized so that

$$
\max_{j=1,\ldots,d}\frac{\Vert X_{j}\Vert_{2}}{\sqrt{n}}\leq C,
$$

then with probability at least $1-2e^{-\frac{n\delta^{2}}{2}}$ it holds that

$$
\Vert\widehat{\theta}-\theta^{\ast}\Vert_{2}\leq\frac{4C\sigma}{\mu}\left(\sqrt{\frac{2k\log(d)}{n}}+\sqrt{k}\delta\right).
$$
</details>

<details>
<summary>Proof</summary>

Define $\Delta$ so that $\widehat{\theta}=\theta^{\ast}+\Delta .$ Let us try to bound the quantity $\Vert\widehat{\theta}-\theta^{\ast}\Vert_{2}=\Vert\Delta\Vert_{2}.$ Let $S=\operatorname{supp}(\theta^{\ast}).$ Then $\Delta\in\mathbb{C}(S)$ since

$$
\begin{aligned}
\Vert\theta_{S}^{\ast}\Vert_{1}=b &\geq \Vert\widehat{\theta}\Vert_{1} \\
	&=\Vert\theta^{\ast}+\Delta\Vert_{1} \\
	&=\Vert\theta_{S}^{\ast}+\Delta_{S}\Vert_{1}+\Vert\Delta_{S^{c}}\Vert_{1} \\
	&\geq\Vert\theta_{S}^{\ast}\Vert_{1}-\Vert\Delta_{S}\Vert_{1}+\Vert\Delta_{S^{c}}\Vert_{1}
\end{aligned}
$$

which implies $\Vert\Delta_{S}\Vert_{1}\geq\Vert\Delta_{S^{c}}\Vert_{1}.$ Also, from 

$$
\frac{1}{2}\Vert X\Delta-\epsilon\Vert_{2}^{2}=\frac{1}{2}\Vert X\widehat{\theta}-Y\Vert_{2}^{2}\leq\frac{1}{2}\Vert X\theta^{\ast}-Y\Vert_{2}^{2}=\frac{1}{2}\Vert\epsilon\Vert_{2}^{2},
$$

expanding yields the inequality

$$
\Vert X\Delta\Vert_{2}^{2}\leq2\Delta^{T}X^{T}\epsilon.
$$

If $X$ satisfies the restricted eigenvalue condition over $S\subset[d]$ with parameters $(1,\mu),$ it follows that

$$
\begin{aligned}
n\mu\Vert\Delta\Vert_{2}^{2} &\leq 2\Delta^{T}X^{T}\epsilon \\
	&\leq2\Vert\Delta\Vert_{1}\Vert X^{T}\epsilon\Vert_{\infty} \\
	&\leq4\Vert\Delta_{S}\Vert_{1}\Vert X^{T}\epsilon\Vert_{\infty} \\
	&\leq4\sqrt{k}\Vert\Delta_{S}\Vert_{2}\Vert X^{T}\epsilon\Vert_{\infty},
\end{aligned}
$$

where $k=|S|.$ This implies that 

$$
\Vert\Delta\Vert_{2}\leq\frac{4\sqrt{k}\Vert X^{T}\epsilon\Vert_{\infty}}{n\mu}.
$$

Note that

$$
\left\Vert \frac{X^{T}\epsilon}{n}\right\Vert _{\infty}=\max_{j=1,\ldots,d}\left|\frac{X_{j}^{T}\epsilon}{n}\right|
$$

where $X_{j}^{T}\epsilon/n$ is a sub-Gaussian random variable with variance proxy $\sigma_{j}^{2}=\frac{1}{n^{2}}\sum_{i=1}^{n}X_{ij}^{2}\sigma^{2}\leq C^{2}\sigma^{2}/n.$ Therefore, 

$$
\mathbb{P}\left[\frac{\left\Vert X^{T}\epsilon\right\Vert _{\infty}}{n}>t\right]\leq2de^{-\frac{nt^{2}}{2C^{2}\sigma^{2}}}.
$$

This yields

$$
\mathbb{P}\left[\frac{\left\Vert X^{T}\epsilon\right\Vert _{\infty}}{n}>C\sigma\left(\sqrt{\frac{2\log(d)}{n}}+\delta\right)\right]\leq2e^{-\frac{n\delta^{2}}{2}}.
$$
</details>
