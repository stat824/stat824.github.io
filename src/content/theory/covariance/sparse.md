# Sparse PCA

Consider again the spiked covariance model. In the high-dimensional case, where $d>n,$ the result we had for PCA is uninformative. As before, we resort to sparsity to overcome this limitation. We will assume that $v$ in the spiked covariance model is $k$-sparse. Therefore, a natural estimator of $v$ is given by 

$$
\widehat{v}\in\argmax\left\{ u^{T}\widehat{\Sigma}u:u\in\mathcal{S}^{d-1},\Vert u\Vert_{0}=k\right\} .
$$

<details open>
<summary>Theorem</summary>

Let $Y\in\mathbb{R}^{d}$ be a zero-mean random vector such that $\mathbb{E}[YY^{T}]=I_{d},$ and $Y\sim\operatorname{subG}_{d}(1).$ Let $X_{1},\ldots,X_{n}$ be $n$ independent copies of the sub-Gaussian random vector $X=\Sigma^{1/2}Y.$ Then $\mathbb{E}[X]=0,$ $\mathbb{E}[XX^{T}]=\Sigma ,$ and $X\sim\operatorname{subG}_{d}(\Vert\Sigma\Vert_{\operatorname{op}}).$ Assume that the covariance matrix satisfies the spiked covariance model $\Sigma=\theta vv^{T}+I_{d}$ for $v$ such that $\Vert v\Vert_{0}=k\leq\frac{d}{2}.$ Then the largest eigenvector $\widehat{v}$ of the empirical covariance matrix satisfies

$$
\min_{\epsilon\in\{\pm1\}}\Vert\epsilon\widehat{v}-v\Vert_{2}\lesssim\frac{1+\theta}{\theta}\left(\sqrt{\frac{k\log(ed/k)+\log(1/\delta)}{n}}\lor\frac{k\log(ed/k)+\log(1/\delta)}{n}\right)
$$

with probability at least $1-\delta .$ 
</details>

<details>
<summary>Proof</summary>

Following the same steps as in the proof of the Davis-Kahan $\sin(\theta)$ theorem, we get

$$
v^{T}\Sigma v-\widehat{v}^{T}\Sigma\widehat{v}\leq\langle\widehat{\Sigma}-\Sigma,\widehat{v}\widehat{v}^{T}-vv^{T}\rangle.
$$

Since both $\widehat{v}$ and $v$ are $k$-sparse, there exists a (random) set $S\subset[d]$ such that $|S|\leq2k$ and $(\widehat{v}\widehat{v}^{T}-vv^{T})_{ij}=0$ if $(i,j)\not\in S^{2}.$ It follows that

$$
\langle\widehat{\Sigma}-\Sigma,\widehat{v}\widehat{v}^{T}-vv^{T}\rangle=\langle\widehat{\Sigma}(S)-\Sigma(S),\widehat{v}(S)\widehat{v}(S)^{T}-v(S)v(S)^{T}\rangle
$$

where for any matrix $M,$ $M(S)$ is the is the $|S|\times|S|$ matrix with rows and columns indexed by $S$ (likewise for vectors). By Holder's inequality, 

$$
v^{T}\Sigma v-\widehat{v}^{T}\Sigma\widehat{v}\leq\Vert\widehat{\Sigma}(S)-\Sigma(S)\Vert_{\text{op}}\Vert\widehat{v}(S)\widehat{v}(S)^{T}-v(S)v(S)^{T}\Vert_{\text{nuc}}.
$$

By the same steps as before, we conclude

$$
\sin(\angle(\widehat{v},v))\leq\frac{2}{\theta}\sup_{S:|S|=2k}\Vert\widehat{\Sigma}(S)-\Sigma(S)\Vert_{\text{op}}.
$$

We now turn to providing an upper bound on $\sup \Vert\widehat{\Sigma}(S)-\Sigma(S)\Vert_{\text{op}}.$ By the arguments we used in the proof of the operator norm error bound for covariance estimation, we have

$$
\begin{aligned}
\mathbb{P}\left[\sup_{S:|S|=2k}\Vert\widehat{\Sigma}(S)-\Sigma(S)\Vert_{\text{op}}>t\Vert\Sigma\Vert_{\text{op}}\right]	&\leq\sum_{S:|S|=2k}\mathbb{P}\left[\Vert\widehat{\Sigma}(S)-\Sigma(S)\Vert_{\text{op}}>t\Vert\Sigma\Vert_{\text{op}}\right] \\
	&\leq\binom{d}{2k}144^{2k}\exp\left(-\frac{n}{4}\left(\left(\frac{t}{32}\right)^{2}\land\left(\frac{t}{32}\right)\right)\right).
\end{aligned}
$$

Using $\binom{n}{k}\leq\left(\frac{en}{k}\right)^{k},$ we can see that this quantity is upper bounded by

$$
\exp\left(-\frac{n}{4}\left(\left(\frac{t}{32}\right)^{2}\land\left(\frac{t}{32}\right)\right)+2k\log(144)+k\log\left(\frac{ed}{2k}\right)\right),
$$

which can be controlled to be less than or equal to $\delta$ by choosing 

$$
t\geq C\left(\sqrt{\frac{k\log(ed/k)+\log(1/\delta)}{n}}\lor\frac{k\log(ed/k)+\log(1/\delta)}{n}\right).
$$
</details>
