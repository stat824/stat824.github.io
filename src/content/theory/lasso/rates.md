# Slow and fast rates for the lasso

Apart from the error in the parameter, sometimes we may also be interested in the prediction error

$$
\frac{1}{n}\mathbb{E}[\Vert Y-X\widehat{\theta}\Vert_{2}^{2}]=\frac{1}{n}\mathbb{E}[\Vert X(\theta^{\ast}-\widehat{\theta})\Vert_{2}^{2}]+\sigma^{2}.
$$

Prediction error bounds are much easier to obtain in the sense that it is possible to obtain a bound with only minimal assumptions on the design matrix.

<details open>
<summary>Theorem</summary>

Consider the regularized Lasso with $\lambda_{n}\geq2\Vert\frac{X^{T}\epsilon}{n}\Vert_{\infty}.$

1. Any optimal solution $\widehat{\theta}$ satisfies

   $$
   \frac{\Vert X(\theta^{\ast}-\widehat{\theta})\Vert_{2}^{2}}{n}\leq 6\Vert\theta^{\ast}\Vert_{1}\lambda_{n}.
   $$

2. If the design matrix $X$ satisfies the $\operatorname{RE}(3,\mu)$ property over $S=\operatorname{supp}(\theta^{\ast}),$ then

   $$
   \frac{\Vert X(\theta^{\ast}-\widehat{\theta})\Vert_{2}^{2}}{n}\leq\frac{9k\lambda_{n}^{2}}{\mu}
   $$

   where $k=|S|.$

</details>

<details>
<summary>Proof</summary>

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
	&\leq\frac{\lambda_{n}}{2}(4 \Vert\theta^\ast\Vert_{1})+\lambda_{n}\Vert\theta^{\ast}\Vert_{1} \\
	&\leq\frac{6\lambda_{n}}{2}\Vert\theta^{\ast}\Vert_{1}
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
</details>



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