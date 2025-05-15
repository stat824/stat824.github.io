# Stein's unbiased risk estimator

Consider $X\sim N(\theta,I_{p})$ and let $\widehat{\theta}$ be an estimator. We want to find the UMVUE for the risk function $g(\theta)=\mathbb{E} _ {\theta}\Vert\widehat{\theta}-\theta\Vert^{2}$. Note that $X$ is complete and sufficient, so we want to write $\mathbb{E} _ {\theta}\Vert\widehat{\theta}-\theta\Vert^{2}$ as the expectation of some function of $X$. We have

$$
\begin{aligned}
\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2} &=\mathbb{E}_{\theta}\Vert\widehat{\theta}-X+X-\theta\Vert^{2} \\
	&=\mathbb{E}_{\theta}\left(\Vert\widehat{\theta}-X\Vert^{2}+\Vert X-\theta\Vert^{2}+2\langle X-\theta,\widehat{\theta}-X\rangle\right) \\
	&=\mathbb{E}_{\theta}\left(\Vert\widehat{\theta}-X\Vert^{2}+\Vert X-\theta\Vert^{2}-2\langle X-\theta,X\rangle+2\langle X-\theta,\widehat{\theta}\rangle\right).
\end{aligned}
$$

Writing $X=\theta+Z$ where $Z\sim N(0,I_{p})$, we have $\mathbb{E} _ {\theta}\Vert X-\theta\Vert^{2}=p$, $\mathbb{E} _ {\theta}\langle X-\theta,X\rangle=\mathbb{E} _ {\theta}\langle Z,\theta+Z\rangle=p$, and by Stein's lemma

$$
\mathbb{E}_{\theta}\langle X-\theta,\widehat{\theta}\rangle	=\mathbb{E}_{\theta}\langle Z,\widehat{\theta}(\theta+Z)\rangle=\mathbb{E}_{\theta}\sum_{j=1}^{p}\frac{\partial}{\partial z_{j}}\widehat{\theta}_{j}(\theta+Z)=\mathbb{E}_{\theta}\sum_{j=1}^{p}\frac{\partial}{\partial x_{j}}\widehat{\theta}_{j}.
$$

<details open>
<summary>Definition</summary>

We define Stein's unbiased risk estimator to be the estimator given by

$$
\operatorname{SURE}(\widehat{\theta})=\Vert\widehat{\theta}-X\Vert^{2}-p+2\sum_{j=1}^{p}\frac{\partial}{\partial x_{j}}\widehat{\theta}_{j}.
$$

</details>


From the computation above, we see that $\mathbb{E} _ {\theta}\Vert\widehat{\theta}-\theta\Vert^{2}=\mathbb{E} _ {\theta}\operatorname{SURE}(\widehat{\theta}).$ This is the UMVUE of the risk function. 

<details open>
<summary>Example</summary>

Let $\widehat{\theta} _ {c}=cX$. Then $\widehat{\theta} _ {c^{\ast}}$ where $c^{\ast}=\argmin_{c}\operatorname{SURE}(cX)$ will give something similar to the James-Stein estimator. 
</details>

<details open>
<summary>Example</summary>

Consider the linear model $Y\sim N(\theta,I_{n})$. Let $X\in\mathbb{R}^{n\times p}$ be a fixed full-rank design matrix and let $\widehat{\beta}=\argmin_{\beta}\Vert Y-X\beta\Vert^{2}$. Then $\widehat{\theta}=X\widehat{\beta}=HY$ where $H=X(X^{T}X)^{-1}X^{T}$. Then

$$
\sum_{i=1}^{n}\frac{\partial}{\partial y_{i}}\widehat{\theta}_{i}=\sum_{i=1}^{n}H_{ii}=\operatorname{Tr}(H)=p,
$$

which gives the Akaike information criterion

$$
\operatorname{SURE}(X\widehat{\beta})=\Vert Y-X\widehat{\beta}\Vert^{2}+2p-n.
$$
</details>
