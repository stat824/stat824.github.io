# The regularized form of the lasso

Restricted eigenvalue conditions can also be used to prove bounds for the regularized lasso

$$
\widehat{\theta}\in\argmin_{\theta\in\mathbb{R}^{d}}\left\{ \frac{1}{2n}\Vert Y-X\theta\Vert_{2}^{2}+\lambda_{n}\Vert\theta\Vert_{1}\right\} .
$$

The challenge now is that we can no longer guarantee that $\Delta = \widehat{\theta}-\theta^{\ast}$ belongs to the cone $\mathbb{C}(S).$ However, we instead have $\Delta \in \mathbb{C}_3(S).$ First, we prove two inequalities known as the new basic inequalities.

<details open>
<summary>Lemma</summary>

Let $\Delta = \widehat{\theta}-\theta^{\ast}.$ We have

$$
\begin{aligned}
\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2} &\leq\frac{1}{n}\langle X^{T}\epsilon,\Delta\rangle+\lambda_{n}(\Vert\theta^{\ast}\Vert_{1}-\Vert\widehat{\theta}\Vert_{1}) \\
	&\leq\frac{1}{n}\langle X^{T}\epsilon,\Delta\rangle+\lambda_{n}(\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}).
\end{aligned}
$$

These are called the new basic inequalities. 
</details>

<details>
<summary>Proof</summary>

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
\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2}\leq\frac{1}{n}\langle X^{T}\epsilon,\Delta\rangle+\lambda_{n}(\Vert\theta^{\ast}\Vert_{1}-\Vert\widehat{\theta}\Vert_{1}),
$$

which is the first inequality. Also, we have

$$
\Vert\theta^{\ast}\Vert_{1}-\Vert\widehat{\theta}\Vert_{1}	=\Vert\theta_{S}^{\ast}\Vert_{1}-\Vert\theta_{S}^{\ast}+\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}
	\leq\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1},
$$
which gives the second inequality.
</details>


An almost immediate consequence is the following. 


<details open>
<summary>Corollary</summary>

Assume that $\lambda_{n}\geq\frac{2\Vert X^{T}\epsilon\Vert_{\infty}}{n}.$ Then $\Delta=\widehat{\theta}-\theta^{\ast}$ satisfies $\Delta\in\mathbb{C}_{3}(S)$ where $S=\operatorname{supp}(\theta^{\ast}).$
</details>

<details>
<summary>Proof</summary>

From the second inequality, we have

$$
\begin{aligned}
0\leq\frac{1}{2n}\Vert X\Delta\Vert_{2}^{2} &\leq \frac{1}{n}\Vert X^{T}\epsilon\Vert_{\infty}\Vert\Delta\Vert_{1}+\lambda_{n}(\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}) \\
	&\leq\frac{\lambda_{n}}{2}(\Vert\Delta_{S}\Vert_{1}+\Vert\Delta_{S^{c}}\Vert_{1})+\lambda_{n}(\Vert\Delta_{S}\Vert_{1}-\Vert\Delta_{S^{c}}\Vert_{1}).
\end{aligned}
$$

Rearranging gives $\Vert\Delta_{S^{c}}\Vert_{1}\leq3\Vert\Delta_{S}\Vert_{1}.$
</details>

We can also prove the following bound on the error. 

<details open>
<summary>Theorem</summary>

Assume that $X$ satisfies the $\operatorname{RE}(3,\mu)$ condition over $S=\operatorname{supp}(\theta^{\ast}).$ If $\lambda_{n}\geq\frac{2\Vert X^{T}\epsilon\Vert_{\infty}}{n},$ then

$$
\Vert\widehat{\theta}-\theta^{\ast}\Vert_{2}\leq\frac{3\lambda_{n}\sqrt{k}}{2\mu}
$$

where $k=|S|.$
</details>

<details>
<summary>Proof</summary>

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
</details>

We obtain the following as a corollary.

<details open>
<summary>Corollary</summary>

Assume that the columns of $X/\sqrt{n}$ are unit vectors. Let $\gamma\geq0$ and let

$$
\lambda_{n}=2\sqrt{\frac{2(1+\gamma)\sigma^{2}\log(2d)}{n}}.
$$

Then with probability at least $1-\frac{1}{(2d)^{\gamma}},$

$$
\Vert\widehat{\theta}-\theta\Vert_{2}\leq\frac{3\lambda_{n}\sqrt{k}}{2}=\frac{6\sqrt{2(1+\gamma)}}{\mu}\sqrt{\frac{\sigma^{2}k\log(2d)}{n}}.
$$
</details>

<details>
<summary>Proof</summary>

Note that $\frac{2}{n}X_{j}^{T}\epsilon$  is sub-Gaussian with variance proxy $\sigma_{j}^{2}=\frac{4}{n^{2}}\sum_{i=1}^{n}X_{ij}^{2}\sigma^{2}=\sigma^{2}/n,$ so

$$
\mathbb{P}\left[\frac{2\Vert X^{T}\epsilon\Vert_{\infty}}{n}>t\right]\leq2d\exp\left(-\frac{nt^{2}}{2\sigma^{2}}\right).
$$

Solving $2d\exp\left(-\frac{nt^{2}}{2\sigma^{2}}\right)=\frac{1}{(2d)^{\gamma}}$ gives 

$$
t=2\sqrt{\frac{2(1+\gamma)\sigma^{2}\log(2d)}{n}}.
$$

Therefore, by choosing $\lambda_{n}$ to be this value, the condition $\lambda_{n}\geq\frac{2\Vert X^{T}\epsilon\Vert_{\infty}}{n}$ holds with probability at least $1-\frac{1}{(2d)^{\gamma}}.$ 
</details>