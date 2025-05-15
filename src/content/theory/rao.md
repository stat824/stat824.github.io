# Rao-Blackwell Theorem

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}P_{\theta}$, and let $\widehat{\theta}=\widehat{\theta}(X_{1},\ldots,X_{n})$ be an estimator of the parameter $\theta$. Let $L(\widehat{\theta},\theta)$ be a loss function which quantifies the accuracy of the estimator. Then the risk function is

$$
R(\widehat{\theta},\theta)=\mathbb{E}_{\theta}L(\widehat{\theta},\theta)=\int L(\widehat{\theta}(x),\theta)p(x|\theta)\,dx.
$$

In other words, $R(\widehat{\theta},\theta)$ is the average deviation of $\widehat{\theta}$ from the true parameter value if the true parameter value is taken to be $\theta$.

<details open>
<summary>Rao-Blackwell Theorem</summary>

Assume $L(\cdot,\theta)$ is convex. Let $\widehat{\theta}$ be an estimator and let $T$ be a sufficient statistic. Then the estimator $\widetilde{\theta}=\mathbb{E}_{\theta}(\widehat{\theta}|T)$ satisfies $R(\widetilde{\theta},\theta)\leq R(\widehat{\theta},\theta).$
</details>

<details>
<summary>Proof</summary>

By Jensen's inequality, we have $L(\widetilde{\theta},\theta)=L(\mathbb{E} _ {\theta}(\widehat{\theta}|T),\theta)\leq \mathbb{E} _ {\theta}(L(\widehat{\theta},\theta)|T)$, and taking expectation of both sides gives $R(\widetilde{\theta},\theta)\leq R(\widehat{\theta},\theta)$.
</details>

In other words, conditioning on a sufficient statistic can improve the risk. 
