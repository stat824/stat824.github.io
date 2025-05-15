# Cramer-Rao lower bound

We know from previous discussions that the maximum likelihood estimator is not always optimal (for example, see discussion on James-Stein estimator.) But what about asymptotically as $n\to\infty$? Maximum likelihood estimators are asymptotically efficient in the sense that their asymptotical variances achieve the Cramer-Rao lower bound under the regularity conditions for asymptotical normality to hold. We state and prove the Cramer-Rao lower bound for 1-dimensional parameter space. The same result holds in higher dimensional parameter space. 

Let us start with the one sample version of the Cramer-Rao lower bound.

<details open>
<summary>Cramer-Rao Lower Bound</summary>

Suppose $X\sim P_{\theta}$ has a score function and Fisher information. If $\widehat{\theta}$ is unbiased, then $\operatorname{Var}_{\theta}[\widehat{\theta}]\geq I_{\theta}^{-1}.$

</details>

<details>
<summary>Proof</summary>

We have 

$$
\operatorname{Var}_{\theta}[\widehat{\theta}]I_{\theta}=\int p_{\theta}(\widehat{\theta}-\theta)^{2}\int p_{\theta}\left(\frac{\frac{\partial}{\partial\theta}p_{\theta}}{p_{\theta}}\right)^{2}\geq\left(\int(\widehat{\theta}-\theta)\frac{\partial}{\partial\theta}p_{\theta}\right)^{2}=\left(\frac{\partial}{\partial\theta}\mathbb{E}_{\theta}[\widehat{\theta}]\right)^{2}=1.
$$

</details>



The Cramer-Rao lower bound for an estimator based on $n$ independent observations $X_1, \ldots, X_n$ can be obtained by viewing $(X_1, \ldots, X_n)$ as a single observation from the product distribution $P_\theta^n.$ This gives the following.

<details open>
<summary>Corollary</summary>

If $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}P_{\theta},$ then for any unbiased estimator $\widehat{\theta},$ we have $\operatorname{Var}_{\theta}[\widehat{\theta}]\geq(nI_{\theta})^{-1}.$

</details>


