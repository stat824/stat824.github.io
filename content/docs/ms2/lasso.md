---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'The Lasso Program'
weight: 8
---

We turn to the setting where there is noise in observations. Suppose that we observe $Y\in\mathbb{R}^{n}$ and a matrix $X\in\mathbb{R}^{n\times d}$ such that

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

## The restricted eigenvalue condition

{{% details title="Definition" %}}

For $\alpha\geq1$ and $S\subset[d],$ define $\mathbb{C} _ {\alpha}(S):= \\{\Delta\in\mathbb{R}^{d}:\Vert\Delta_{S^{c}}\Vert_{1}\leq\alpha\Vert\Delta_{S}\Vert_{1}\\}.$ We say that $X\in\mathbb{R}^{n\times d}$ satisfies the restricted eigenvalue condition over $S\subset[d]$ with parameters $(\alpha,\mu)$ if

$$
\frac{1}{n}\Vert X\Delta\Vert_{2}^{2}\geq\mu\Vert\Delta\Vert_{2}^{2}\quad\text{for all }\Delta\in\mathbb{C}_{\alpha}(S).
$$
{{% /details %}}

From where does the restricted eigenvalue condition arise? Suppose that we know $\Vert\theta^{\ast}\Vert_{1}=b$ and that

$$
\widehat{\theta}\in\argmin_{\theta\in\mathbb{R}^{d}}\left\{ \frac{1}{2}\Vert Y-X\theta\Vert_{2}^{2}:\Vert\theta\Vert_{1}\leq b\right\} .
$$

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

Let us assume that the columns of $X$ are normalized so that $\max_{j=1,\ldots,d}\frac{\Vert X_{j}\Vert_{2}}{\sqrt{n}}\leq C.$ Then

$$
\left\Vert \frac{X^{T}\epsilon}{n}\right\Vert _{\infty}=\max_{j=1,\ldots,d}\left|\frac{X_{j}^{T}\epsilon}{n}\right|
$$

where $X_{j}^{T}\epsilon/n$ is a sub-Gaussian random variable with variance proxy $\sigma_{j}^{2}=\frac{1}{n^{2}}\sum_{i=1}^{n}X_{ij}^{2}\sigma^{2}\leq C^{2}\sigma^{2}/n.$ Therefore, 

$$
\mathbb{P}\left[\frac{\left\Vert X^{T}\epsilon\right\Vert _{\infty}}{n}>t\right]\leq2de^{-\frac{nt^{2}}{2C^{2}\sigma^{2}}}.
$$

This yields

$$
\mathbb{P}\left[\frac{\left\Vert X^{T}\epsilon\right\Vert _{\infty}}{n}>C\sigma\left(\sqrt{\frac{2\log(d)}{n}}+\delta\right)\right]\leq2e^{-\frac{n\delta^{2}}{2}},
$$

leading to the following result. 

{{% details title="Theorem" %}}
Let $b=\Vert\theta^{\ast}\Vert_{1}$ and suppose that $X\in\mathbb{R}^{n\times d}$ satisfies the $\operatorname{RE}(1,\mu)$ condition over $S=\operatorname{supp}(\theta^{\ast}).$ If the columns of $X$ are normalized so that

$$
\max_{j=1,\ldots,d}\frac{\Vert X_{j}\Vert_{2}}{\sqrt{n}}\leq C,
$$

then with probability at least $1-2e^{-\frac{n\delta^{2}}{2}}$ it holds that

$$
\Vert\widehat{\theta}-\theta^{\ast}\Vert_{2}\leq\frac{4C\sigma}{\mu}\left(\sqrt{\frac{2k\log(d)}{n}}+\sqrt{k}\delta\right).
$$
{{% /details %}}


## The regularized form of the Lasso

We now consider the Lasso program

$$
\widehat{\theta}\in\argmin_{\theta\in\mathbb{R}^{d}}\left\{ \frac{1}{2n}\Vert Y-X\theta\Vert_{2}^{2}+\lambda_{n}\Vert\theta\Vert_{1}\right\} .
$$

The challenge now is that we can no longer guarantee that $\widehat{\theta}-\theta^{\ast}$ belongs to the cone $\mathbb{C}(S).$ However, we have the following result instead. 

{{% details title="Lemma" %}}
Assume that $\lambda_{n}\geq\frac{2\Vert X^{T}\epsilon\Vert_{\infty}}{n}.$ Then $\Delta=\widehat{\theta}-\theta^{\ast}$ satisfies $\Delta\in\mathbb{C}_{3}(S)$ where $S=\operatorname{supp}(\theta^{\ast}).$
{{% /details %}}

{{% details title="Proof" closed="true" %}}

By definition of $\widehat{\theta},$ we have

$$
\frac{1}{2n}\Vert Y-X\widehat{\theta}\Vert_{2}^{2}+\lambda_{n}\Vert\widehat{\theta}\Vert_{1}\leq\frac{1}{2n}\Vert Y-X\theta^{\ast}\Vert_{2}^{2}+\lambda_{n}\Vert\theta^{\ast}\Vert_{1}.
$$

This gives

$$
\frac{1}{2n}\Vert X\Delta-\epsilon\Vert_{2}^{2}+\lambda_{n}\Vert\widehat{\theta}\Vert_{1}\leq\frac{1}{2n}\Vert\epsilon\Vert_{2}^{2}+\lambda_{n}\Vert\theta^{\ast}\Vert_{1},
$$

and expanding gives

$$
\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2}\leq\frac{1}{n}\langle X^{T}\epsilon,\Delta\rangle+\lambda_{n}(\Vert\theta^{\ast}\Vert_{1}-\Vert\widehat{\theta}\Vert_{1}).
$$

Also, we have

$$
\Vert\theta^{\ast}\Vert_{1}-\Vert\widehat{\theta}\Vert_{1}	=\Vert\theta_{S}^{\ast}\Vert_{1}-\Vert\theta_{S}^{\ast}+\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}
	\leq\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1},
$$

so

$$
\begin{aligned}
0\leq\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2} &\leq \frac{1}{n}\Vert X^{T}\epsilon\Vert_{\infty}\Vert\Delta\Vert_{1}+\lambda_{n}(\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}) \\
	&\leq\frac{\lambda_{n}}{2}(\Vert\Delta_{S}\Vert_{1}+\Vert\Delta_{S^{c}}\Vert_{1})+\lambda_{n}(\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}).
\end{aligned}
$$

Rearranging gives $\Vert\Delta_{S^{c}}\Vert_{1}\leq3\Vert\Delta_{S}\Vert_{1}.$
{{% /details %}}

From the proof of the lemma, we have the inequalities

$$
\begin{aligned}
\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2} &\leq\frac{1}{n}\langle X^{T}\epsilon,\Delta\rangle+\lambda_{n}(\Vert\theta^{\ast}\Vert_{1}-\Vert\widehat{\theta}\Vert_{1}) \\
	&\leq\frac{1}{n}\langle X^{T}\epsilon,\Delta\rangle+\lambda_{n}(\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}).
\end{aligned}
$$

We call these the new basic inequalities. Using this lemma, we can prove the following. 

{{% details title="Theorem" %}}
Assume that $X$ satisfies the $\operatorname{RE}(3,\mu)$ condition over $S=\operatorname{supp}(\theta^{\ast}).$ If $\lambda_{n}\geq\frac{2\Vert X^{T}\epsilon\Vert_{\infty}}{n},$ then

$$
\Vert\widehat{\theta}-\theta^{\ast}\Vert_{2}\leq\frac{3\lambda_{n}\sqrt{k}}{2\mu}
$$

where $k=|S|.$
{{% /details %}}

{{% details title="Proof" closed="true" %}}
We have

$$
\begin{aligned}
\mu\Vert\Delta\Vert_{2}^{2}\leq\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2} &\leq\frac{1}{n}\langle X^{T}\epsilon,\Delta\rangle+\lambda_{n}(\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}) \\
	&\leq\frac{1}{n}\Vert X^{T}\epsilon\Vert_{\infty}\Vert\Delta\Vert_{1}+\lambda_{n}(\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}) \\
	&\leq\frac{\lambda_{n}}{2}(\Vert\Delta_{S}\Vert_{1}+\Vert\Delta_{S^{c}}\Vert_{1})+\lambda_{n}(\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}) \\
	&\leq\frac{3\lambda_{n}}{2}\Vert\Delta_{S}\Vert_{1} \\
	&\leq\frac{3\lambda_{n}\sqrt{k}}{2}\Vert\Delta_{S}\Vert_{2} \\
	&\leq\frac{3\lambda_{n}\sqrt{k}}{2}\Vert\Delta\Vert_{2}.
\end{aligned}
$$

This yields $\Vert\Delta\Vert_{2}\leq\frac{3\lambda_{n}\sqrt{k}}{2\mu}$ as desired. 
{{% /details %}}

We obtain the following as a corollary.

{{% details title="Corollary" %}}
Assume that the columns of $X/\sqrt{n}$ are unit vectors. Let $\gamma\geq0$ and let

$$
\lambda_{n}=2\sqrt{\frac{2(1+\gamma)\sigma^{2}\log(2d)}{n}}.
$$

Then with probability at least $1-\frac{1}{(2d)^{\gamma}},$

$$
\Vert\widehat{\theta}-\theta\Vert_{2}\leq\frac{3\lambda_{n}\sqrt{k}}{2}=\frac{6\sqrt{2(1+\gamma)}}{\mu}\sqrt{\frac{\sigma^{2}k\log(2d)}{n}}.
$$
{{% /details %}}

{{% details title="Proof" closed="true" %}}
Note that $\frac{2}{n}X_{j}^{T}\epsilon$  is sub-Gaussian with variance proxy $\sigma_{j}^{2}=\frac{4}{n^{2}}\sum_{i=1}^{n}X_{ij}^{2}\sigma^{2}=\sigma^{2}/n,$ so

$$
\mathbb{P}\left[\frac{2\Vert X^{T}\epsilon\Vert_{\infty}}{n}>t\right]\leq2d\exp\left(-\frac{nt^{2}}{2\sigma^{2}}\right).
$$

Solving $2d\exp\left(-\frac{nt^{2}}{2\sigma^{2}}\right)=\frac{1}{(2d)^{\gamma}}$ gives 

$$
t=2\sqrt{\frac{2(1+\gamma)\sigma^{2}\log(2d)}{n}}.
$$

Therefore, by choosing $\lambda_{n}$ to be this value, the condition $\lambda_{n}\geq\frac{2\Vert X^{T}\epsilon\Vert_{\infty}}{n}$ holds with probability at least $1-\frac{1}{(2d)^{\gamma}}.$ 
{{% /details %}}

## Bounds on prediction error for the Lasso

Apart from the error in the parameter, sometimes we may also be interested in the prediction error

$$
\frac{1}{n}\mathbb{E}[\Vert Y-X\widehat{\theta}\Vert_{2}^{2}]=\frac{1}{n}\mathbb{E}[\Vert X(\theta^{\ast}-\widehat{\theta})\Vert_{2}^{2}]+\sigma^{2}.
$$

{{% details title="Theorem" %}}
Consider the regularized Lasso with $\lambda_{n}\geq2\Vert\frac{X^{T}\epsilon}{n}\Vert_{\infty}.$

1. Any optimal solution $\widehat{\theta}$ satisfies

	$$
\frac{\Vert X(\theta^{\ast}-\widehat{\theta})\Vert_{2}^{2}}{n}\leq12\Vert\theta^{\ast}\Vert_{1}\lambda_{n}.
$$

2. If the design matrix $X$ satisfies the $\operatorname{RE}(3,\mu)$ property over $S=\operatorname{supp}(\theta^{\ast}),$ then

$$
\frac{\Vert X(\theta^{\ast}-\widehat{\theta})\Vert_{2}^{2}}{n}\leq\frac{9k\lambda_{n}^{2}}{\mu}
$$

where $k=|S|.$

{{% /details %}}

{{% details title="Proof" closed="true" %}}
Let $\widehat{\theta}$ be a solution to the Lasso program with $\lambda_{n}\geq2\Vert\frac{X^{T}\epsilon}{n}\Vert_{\infty}.$ Let $\Delta=\widehat{\theta}-\theta^{\ast}.$ We have

$$
\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2}	\leq\frac{1}{n}\langle X^{T}\epsilon,\Delta\rangle+\lambda_{n}(\Vert\theta^{\ast}\Vert_{1}-\Vert\widehat{\theta}\Vert_{1}),
$$

where 

$$
\begin{aligned}
\left|\frac{\langle X^{T}\epsilon,\Delta\rangle}{n}\right| &\leq \left\Vert \frac{X^{T}\epsilon}{n}\right\Vert _{\infty}\Vert\Delta\Vert_{1} \\
	&\leq\frac{\lambda_{n}}{2}\left(\Vert\Delta_{S}\Vert_{1}+\Vert\Delta_{S^{c}}\Vert_{1}\right) \\
	&=\frac{\lambda_{n}}{2}\left(\Vert\widehat{\theta}_{S}-\theta_{S}^{\ast}\Vert_{1}+\Vert\widehat{\theta}_{S^{c}}\Vert_{1}\right) \\
	&\leq\frac{\lambda_{n}}{2}\left(\Vert\widehat{\theta}_{S}\Vert_{1}+\Vert\theta_{S}^{\ast}\Vert_{1}+\Vert\widehat{\theta}_{S^{c}} \\\Vert_{1}\right)\\
	&=\frac{\lambda_{n}}{2}\left(\Vert\theta^{\ast}\Vert_{1}+\Vert\widehat{\theta}\Vert_{1}\right).
\end{aligned}
$$

This gives

$$
0\leq\frac{\lambda_{n}}{2}\left(\Vert\theta^{\ast}\Vert_{1}+\Vert\widehat{\theta}\Vert_{1}\right)+\lambda_{n}(\Vert\theta^{\ast}\Vert_{1}-\Vert\widehat{\theta}\Vert_{1})\implies\Vert\widehat{\theta}\Vert_{1}\leq3\Vert\theta^{\ast}\Vert_{1}
$$

and hence

$$
\Vert\Delta\Vert_{1}\leq\Vert\widehat{\theta}\Vert_{1}+\Vert\theta^{\ast}\Vert_{1}\leq4\Vert\theta^{\ast}\Vert_{1}.
$$

Using this, we obtain

$$
\begin{aligned}
\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2} &\leq \frac{\lambda_{n}}{2}\Vert\Delta\Vert_{1}+\lambda_{n}(\Vert\theta^{\ast}\Vert_{1}-\Vert\widehat{\theta}\Vert_{1}) \\
	&\leq\frac{\lambda_{n}}{2}\Vert\Delta\Vert_{1}+\lambda_{n}(\Vert\theta^{\ast}\Vert_{1}-\Vert\theta^{\ast}+\Delta\Vert_{1}) \\
	&\leq\frac{\lambda_{n}}{2}\Vert\Delta\Vert_{1}+\lambda_{n}\Vert\Delta\Vert_{1} \\
	&\leq\frac{12\lambda_{n}}{2}\Vert\theta^{\ast}\Vert_{1}
\end{aligned}
$$

which proves the first part of the theorem. For the second part of the theorem, assume that $X$ satisfies the $\operatorname{RE}(3,\mu)$ property over $S=\operatorname{supp}(\theta^{\ast}).$ From the proof of the previous theorem, we have

$$
\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2}\leq\frac{3\lambda_{n}\sqrt{k}}{2}\Vert\Delta\Vert_{2}.
$$

We also have from a previous lemma that $\Delta\in\mathbb{C}_{3}(S),$ and since the $\operatorname{RE}(3,\mu)$ condition holds for $X$ we have

$$
\Vert\Delta\Vert_{2}^{2}\leq\frac{1}{\mu n}\Vert X\Delta\Vert_{2}^{2}.
$$

Thus, 

$$
\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2}\leq\frac{3\lambda_{n}\sqrt{k}}{2}\frac{1}{\sqrt{\mu n}}\Vert X\Delta\Vert_{2}\implies\frac{1}{\sqrt{n}}\Vert X\Delta\Vert_{2}\leq\frac{3\lambda_{n}\sqrt{k}}{\sqrt{\mu}}.
$$

Squaring both sides of this inequality gives the desired result. 
{{% /details %}}



We make the following observations:

* As seen in a previous computation, if the columns of $X$ satisfy $\max_{j=1,\ldots,d}\frac{\Vert X_{j}\Vert_{2}}{\sqrt{n}}\leq C,$ then we have

	$$
\mathbb{P}\left[\frac{\left\Vert X^{T}\epsilon\right\Vert _{\infty}}{n}\leq C\sigma\left(\sqrt{\frac{2\log(d)}{n}}+\delta\right)\right]\geq1-2e^{-\frac{n\delta^{2}}{2}}.
$$

	Therefore, by choosing $\lambda_{n}=2C\sigma\left(\sqrt{\frac{2\log(d)}{n}}+\delta\right),$ the first part of the theorem implies the upper bound

	$$
\frac{\Vert X(\widehat{\theta}-\theta^{\ast})\Vert_{2}^{2}}{n}\leq24C\sigma\Vert\theta^{\ast}\Vert_{1}\left(\sqrt{\frac{2\log(d)}{n}}+\delta\right)
$$

	holds with the same high probability. We make no assumptions on the design matrix: $X$ could have as ill-conditioned as you could imagine, and this would still hold with high probability. 

* If we assume further that $X$ satisfies the $\operatorname{RE}(3,\mu)$ property over $S=\operatorname{supp}(\theta^{\ast}),$ then the second part of the theorem implies the bound

	$$
\frac{\Vert X(\widehat{\theta}-\theta^{\ast})\Vert_{2}^{2}}{n}\leq\frac{72}{\mu}C^{2}\sigma^{2}\left(\frac{2s\log(d)}{n}+s\delta^{2}\right),
$$

	which can be a substantially tighter bound. 



For these reasons, the bound in the second part of the theorem is known as the fast rate for the Lasso, while the bound in the first part is known as the slow rate.