# Low-dimensional error bound

Let $X_{1},\ldots,X_{n}$ be i.i.d. copies of a centered random vector $X\in\mathbb{R}^{d}$ such that $\mathbb{E}[X^{T}X]=\Sigma$ for some unknown matrix $\Sigma\succ0$ called the covariance matrix. A natural candidate to estimate $\Sigma$ is the empirical covariance matrix

$$
\widehat{\Sigma}=\frac{1}{n}\sum_{i=1}^{n}X_{i}^{T}X_{i}.
$$

We consider the problem of estimating $\Sigma$ from $\widehat{\Sigma}.$ 

<details open>
<summary>Theorem</summary>

Let $Y\in\mathbb{R}^{d}$ be a zero-mean random vector such that $\mathbb{E}[YY^{T}]=I_{d},$ and $Y\sim\operatorname{subG}_{d}(1).$ Let $X_{1},\ldots,X_{n}$ be $n$ independent copies of the sub-Gaussian random vector $X=\Sigma^{1/2}Y.$ Then $\mathbb{E}[X]=0,$ $\mathbb{E}[XX^{T}]=\Sigma ,$ and $X\sim\operatorname{subG}_{d}(\Vert\Sigma\Vert_{\operatorname{op}}).$ Moreover, for any $\delta \in (0,1),$ we have

$$
\Vert\widehat{\Sigma}-\Sigma\Vert_{\operatorname{op}}\lesssim\Vert\Sigma\Vert_{\operatorname{op}}\left(\sqrt{\frac{d+\log(1/\delta)}{n}}\lor\frac{d+\log(1/\delta)}{n}\right)
$$

with probability at least $1-\delta . $
</details>

<details>
<summary>Proof</summary>

It is easy to see that $\mathbb{E}[X]=0$ and we have $\mathbb{E}[XX^{T}]=\mathbb{E}[\Sigma^{1/2}YY^{T}\Sigma^{1/2}]=\Sigma^{1/2}I_{d}\Sigma^{1/2}=\Sigma .$ To see that $X\sim\operatorname{subG}_{d}(\Vert\Sigma\Vert_{\operatorname{op}}),$ note that for any unit vector $u\in\mathcal{S}^{d-1}$ we have $\langle u,X\rangle=\langle u,\Sigma^{1/2}Y\rangle=\langle\Sigma^{1/2}u,Y\rangle\sim\operatorname{subG}(\Vert\Sigma^{1/2}u\Vert_{2}^{2}).$ Since $\Vert\Sigma^{1/2}u\Vert_{2}^{2}\leq\Vert\Sigma\Vert_{\text{op}},$ it follows that $\langle u,X\rangle\sim\operatorname{subG}(\Vert\Sigma\Vert_{\operatorname{op}})$ for every $u\in\mathcal{S}^{d-1},$ so we have $X\sim\operatorname{subG}_{d}(\Vert\Sigma\Vert_{\operatorname{op}}).$ To prove the concentration inequality, observe first that

$$
\begin{aligned}
\frac{\Vert\widehat{\Sigma}-\Sigma\Vert_{\text{op}}}{\Vert\Sigma\Vert_{\text{op}}}	&=\frac{\Vert\frac{1}{n}\sum_{i=1}^{n}X_{i}^{T}X_{i}-\Sigma\Vert_{\text{op}}}{\Vert\Sigma\Vert_{\text{op}}} \\
	&\leq\frac{\Vert\Sigma^{1/2}\Vert_{\text{op}}\Vert\frac{1}{n}\sum_{i=1}^{n}Z_{i}^{T}Z_{i}-I\Vert_{2}\Vert\Sigma^{1/2}\Vert_{\text{op}}}{\Vert\Sigma\Vert_{\text{op}}} \\
	&=\left\Vert\frac{1}{n}\sum_{i=1}^{n}Z_{i}^{T}Z_{i}-I\right\Vert_{\text{op}},
\end{aligned}
$$

where $Z_{i}=X_{i}\Sigma^{-1/2}.$ Therefore, without loss of generality, we can assume that $\Sigma=I_{d}.$ Let $\mathcal{N}_{1}$ be a $1/4$-net for $\mathcal{S}^{d-1}$ which we may choose to have cardinality $|\mathcal{N}_{1}|\leq 12^{d}.$ Similarly, let $\mathcal{N}_{2}$ be a $1/4$-net for $\mathcal{S}^{T-1}$ which has cardinality $|\mathcal{N}_{2}|\leq12^{T}.$ For any $u\in\mathcal{S}^{d-1},$ $v\in\mathcal{S}^{T-1},$ and any matrix $A\in\mathbb{R}^{d\times T},$

$$
\begin{aligned}
 u^{T}Av	&\leq\max_{x\in\mathcal{N}_{1}}x^{T}Av+\frac{1}{4}\max_{u\in\mathcal{S}^{d-1}}u^{T}Av \\
	&\leq\max_{x\in\mathcal{N}_{1}}\max_{y\in\mathcal{N}_{2}}x^{T}Ay+\frac{1}{4}\max_{u\in\mathcal{S}^{d-1}}u^{T}Av+\frac{1}{4}\max_{u\in\mathcal{S}^{d-1}}u^{T}Av \\
	&=\max_{x\in\mathcal{N}_{1}}\max_{y\in\mathcal{N}_{2}}x^{T}Ay+\frac{1}{2}\max_{u\in\mathcal{S}^{d-1}}u^{T}Av,
\end{aligned}

$$

which yields

$$
\Vert A\Vert_{\text{op}}\leq2\max_{x\in\mathcal{N}_{1}}\max_{y\in\mathcal{N}_{2}}x^{T}Ay.
$$

Therefore, we have

$$
\Vert\widehat{\Sigma}-I_{d}\Vert_{\text{op}}\leq2\max_{x\in\mathcal{N}_{1}}\max_{y\in\mathcal{N}_{2}}x^{T}(\widehat{\Sigma}-I_{d})y.
$$

For any $t\geq0,$ by a union bound, 

$$
\mathbb{P}[\Vert\widehat{\Sigma}-I_{d}\Vert_{\text{op}}>t]\leq\sum_{(x,y)\in\mathcal{N}_{1}\times\mathcal{N}_{2}}\mathbb{P}\left[x^{T}(\widehat{\Sigma}-I_{d})y>\frac{t}{2}\right].
$$

Now that we have our net, we need to bound the probabilities of each of the components of this grid. Observe that

$$
x^{T}(\widehat{\Sigma}-I_{d})y=\frac{1}{n}\sum_{i=1}^{n}\left((X_{i}^{T}x)^{T}(X_{i}^{T}y)-\mathbb{E}\left[(X_{i}^{T}x)^{T}(X_{i}^{T}y)\right]\right).
$$

We have

$$
(X_{i}^{T}x)^{T}(X_{i}^{T}y)=\frac{Z_{+}^{2}-Z_{-}^{2}}{4}
$$

where $Z_{+}=X_{i}^{T}(x+y)$ and $Z_{-}=X_{i}^{T}(x-y).$ Since $X\sim\operatorname{subG}_{d}(1),$ we have $Z_{+},Z_{-}\sim\operatorname{subG}(4).$ The square of a $\operatorname{subG}(\sigma^{2})$ variable is sub-exponential with parameters $(256\sigma^{4},16\sigma^{2}),$ so we have $Z_{+}^{2},Z_{-}^{2}\sim\operatorname{subE}(64^{2},64).$ Therefore, $(X_{i}^{T}x)^{T}(X_{i}^{T}y)\sim\operatorname{subE}(512,64)$ and we have $x^{T}(\widehat{\Sigma}-I_{d})y\sim\operatorname{subE}(512/n,64/n).$ By the Chernoff bound for sub-exponential variables, we have

$$
\mathbb{P}\left[x^{T}(\widehat{\Sigma}-I_{d})y>\frac{t}{2}\right]\leq\exp\left(-\frac{n}{4}\left(\frac{t^{2}}{32^{2}}\land\frac{t}{32}\right)\right).
$$

The union bound gives

$$
\mathbb{P}[\Vert\widehat{\Sigma}-I_{d}\Vert_{\text{op}}>t]\leq144^{d}\exp\left(-\frac{n}{4}\left(\left(\frac{t}{32}\right)^{2}\land\frac{t}{32}\right)\right).
$$

In particular, the right hand side of the above inequality is at most $\delta\in(0,1)$ if 

$$
\frac{t}{32}\geq\left(\frac{4d}{n}\log(144)+\frac{4}{n}\log(1/\delta)\right)\lor\sqrt{\frac{4d}{n}\log(144)+\frac{4}{n}\log(1/\delta)}.
$$

</details>

Having a good estimator of $\Sigma$ is important in a variety of problems. Importantly, note that $\Sigma$ contains information about the projection of the vector $X$ onto any direction $u\in\mathcal{S}^{d-1}.$ Indeed, we have that $\operatorname{Var}(X^{T}u)=u^{T}\Sigma u,$ which can be readily estimated by $\widehat{\operatorname{Var}}(X^{T}u)=u^{T}\widehat{\Sigma}u.$ From the bound we have above, it follows that with probability at least $1-\delta$, 

$$
|\operatorname{Var}(X^{T}u)-\widehat{\operatorname{Var}}(X^{T}u)|	\leq|u^{T}(\widehat{\Sigma}-\Sigma)u|
	\lesssim\Vert\Sigma\Vert_{\operatorname{op}}\left(\sqrt{\frac{d+\log(1/\delta)}{n}}\lor\frac{d+\log(1/\delta)}{n}\right)
$$