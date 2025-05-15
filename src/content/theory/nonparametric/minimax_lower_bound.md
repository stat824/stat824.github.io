# Minimax lower bound for Gaussian sequence model

Now we want to prove the minimax lower bound for the Gaussian sequence problem. Recall that we have observations $X_{j}\sim N(\theta_{j},\frac{1}{n})$, $j\in\mathbb{N}$, where $\theta\in\Theta_{\alpha}(R)=\{\theta:\sum_{j=1}^{\infty}j^{2\alpha}\theta_{j}^{2}\leq R^{2}\}$. We want to show that

$$
\inf_{\hat{\theta}}\sup_{\theta\in\Theta_{\alpha}(R)}\mathbb{E}_{\theta}\Vert\hat{\theta}-\theta\Vert^{2}\geq cn^{\frac{-2\alpha}{2\alpha+1}}.
$$

Let us define $\Theta_{0}=\{\theta:\theta_{j}\in\{0,\frac{1}{\sqrt{n}}\}\text{ for }j=1,\ldots,k,\theta_{j}=0\text{ for }j>k\}$. Then $|\Theta_{0}|=2^{k}$. To ensure that $\Theta_{0}\subseteq\Theta_{\alpha}(R)$, we note that

$$
\sum_{j=1}^{\infty}j^{2\alpha}\theta_{j}^{2}\leq\frac{1}{n}\sum_{j=1}^{k}j^{2\alpha}\leq\frac{k^{2\alpha+1}}{n}.
$$

Solving $\frac{k^{2\alpha+1}}{n}\leq R^{2}$ gives $k\asymp n^{\frac{1}{2\alpha+1}}$. Let us introduce the notation $\theta_{-j}$ to denote $(\theta_1, \ldots, \theta_{j-1}, \theta_{j+1}, \ldots, \theta_k)$. We also write $\operatornamewithlimits{ave}_{x\in S} f(x)$ to denote the average of $f(x)$ over $x \in S$ where $S$ is a finite set. Then

$$
\begin{aligned}
\inf_{\widehat{\theta}}\sup_{\theta\in\Theta_{\alpha}(R)}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2} &\geq\inf_{\widehat{\theta}}\sup_{\theta\in\Theta_{0}}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2} \\
	&\geq\inf_{\widehat{\theta}}\operatornamewithlimits{ave}_{\theta\in\Theta_{0}}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2} \\
	&\geq\inf_{\widehat{\theta}}\operatornamewithlimits{ave}_{\theta\in\Theta_{0}}\sum_{j=1}^{k}(\widehat{\theta}_{j}-\theta_{j})^{2} \\
	&=\inf_{\widehat{\theta}}\sum_{j=1}^{k}\operatornamewithlimits{ave}_{\theta\in\Theta_{0}}\mathbb{E}_{\theta}(\widehat{\theta}_{j}-\theta_{j})^{2} \\
	&=\inf_{\widehat{\theta}}\sum_{j=1}^{k}\operatornamewithlimits{ave}_{\theta_{-j}}\left[\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=0)}(\widehat{\theta}_{j})^{2}+\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=\frac{1}{\sqrt{n}})}(\widehat{\theta}_{j}-\frac{1}{\sqrt{n}})^{2}\right] \\
	&\geq\sum_{j=1}^{k}\operatornamewithlimits{ave}_{\theta_{-j}}\inf_{\widehat{\theta}_{j}}\left[\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=0)}(\widehat{\theta}_{j})^{2}+\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=\frac{1}{\sqrt{n}})}(\widehat{\theta}_{j}-\frac{1}{\sqrt{n}})^{2}\right].
\end{aligned}
$$

Using the same argument as in the proof of Le Cam's method to estimate the infimum, we have

$$
\inf_{\widehat{\theta}_{j}}\left[\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=0)}(\widehat{\theta}_{j})^{2}+\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=\frac{1}{\sqrt{n}})}(\widehat{\theta}_{j}-\frac{1}{\sqrt{n}})^{2}\right] \geq \frac{1}{4n}\int p_{(\theta_{-j},\theta_{j}=0)}\land p_{(\theta_{-j},\theta_{j}=\frac{1}{\sqrt{n}})}.
$$

The integral represents the optimal test error for testing the hypotheses $H_0 : \theta_j = 0$ versus $H_1 : \theta_j = \frac{1}{\sqrt{n}}$. Since only the $\theta_{j}$ differs between the two hypotheses, this is equivalent to testing $H_{0}:X_{j}\sim N(0,\frac{1}{n})$ versus $H_{1}:X_{j}\sim N(\frac{1}{\sqrt{n}},\frac{1}{n})$. Therefore, letting $P=N(0,\frac{1}{n})$ and $Q=N(\frac{1}{\sqrt{n}},\frac{1}{n})$, we have

$$
\inf_{\widehat{\theta}}\sup_{\theta\in\Theta_{\alpha}(R)}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2}\geq \frac{1}{4n} \sum_{j=1}^{k} \inf_{\phi}(P\phi+Q(1-\phi)).
$$

From a previous example, we know that the optimal testing error for this test satisfies 

$$
\inf_{\phi}(P\phi+Q(1-\phi))\geq C
$$

where $C=\mathbb{P}(N(0,1)>\frac{1}{2})$. Therefore, 

$$
\inf_{\widehat{\theta}}\sup_{\theta\in\Theta_{\alpha}(R)}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2}\geq\frac{k}{n} \asymp n^{-\frac{2\alpha}{2\alpha+1}}.
$$