# Thresholding of empirical covariance

Now, let’s look at high dimensional settings where the previous bound is not that great. This requires some assumptions on the structure of the matrix, such as sparsity. Suppose that the covariance matrix $\Sigma$ is known to be relatively sparse, but that the positions of the non-zero entries are not known. It is then natural to consider estimators based on thresholding. Given a parameter $\lambda>0$ the hard thresholding operator is given by $T_{\lambda}(u)=u1_{\{|u|>\lambda\}}.$ We write $T_{\lambda}(M)$ for the matrix obtained by applying $T_{\lambda}$ to each entry. It can be shown that $\Vert A\Vert_{\text{op}}\leq s$ whenever $\Sigma$ has at most s non-zero entries per row. The following result provides a guarantee for the thresholded sample covariance estimator.

<details open>
<summary>Theorem</summary>

Let $X_{1},\ldots,X_{n}$ be an i.i.d sequence of a zero-mean random vector with covariance matrix $\Sigma$ and suppose each $X_{ij}$ is sub-Gaussian with parameter at most $\sigma.$ If $n>\log(d),$ then for any $\delta>0,$ the thresholded sample covariance matrix $T_{\lambda_{n}}(\widehat{\Sigma})$ with $\lambda_{n}=8\sigma^{2}\sqrt{\frac{\log(d)}{n}}+\sigma^{2}\delta$ satisfies

$$
\mathbb{P}[\Vert T_{\lambda_{n}}(\widehat{\Sigma})-\Sigma\Vert_{\operatorname{op}}\geq2\Vert\Sigma\Vert_{\operatorname{op}}\lambda_{n}]\leq8e^{-\frac{n}{16}\min(\delta,\delta^{2})}.
$$

</details>
