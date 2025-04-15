---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Non-asymptotic Bounds for the Least Squares Estimator'
weight: 5
---

We now turn to the topic of high-dimensional linear models. Let $\theta^{\ast}\in\mathbb{R}^{d}$ be an unknown parameter. Suppose that we observe $Y\in\mathbb{R}^{n}$ and a matrix $X\in\mathbb{R}^{n\times d}$ such that

$$
Y=X\theta^{\ast}+\epsilon
$$

where $X\in\mathbb{R}^{n\times d}$ is a deterministic design matrix and $\epsilon\sim\operatorname{subG}(\sigma^{2})$ is sub-Gaussian noise with independent components. Our main focus will be the high-dimensional setting where $n<d$ (more parameters than observations). In this case, $Y=X\theta^{\ast}$ defines an underdetermined linear system. 

## Unconstrained least squares

Define the (unconstrained) least squares estimator $\widehat{\theta}^{\text{LS}}$ to be any vector

$$
\widehat{\theta}^{\text{LS}}\in\argmin_{\theta\in\mathbb{R}^{d}}\Vert Y-X\theta\Vert_{2}^{2}.
$$

Then we define $\widehat{\mu}^{\text{LS}}=X\widehat{\theta}^{\text{LS}}.$

{{% details title="Proposition" %}}

The least squares estimator $\widehat{\theta}^{\text{LS}}$ satisfies $X^T X \widehat{\theta}^{\text{LS}}=X^{T}Y.$ In particular, $\widehat{\theta}^{\text{LS}}$ can be chosen to be $\widehat{\theta}^{\text{LS}}=(X^{T}X)^{\dagger}X^{T}Y.$
{{% /details %}}

{{% details title="Proof" closed="true" %}}
Since $\theta\mapsto\Vert Y-X\theta\Vert_{2}^{2}$ is convex, a minimum is achieved whenever $\nabla_{\theta}\Vert Y-X\theta\Vert_{2}^{2}=0.$ Differentiating gives 

$$
\nabla_{\theta}\Vert Y-X\theta\Vert_{2}^{2}=0\implies X^{T}(Y-X\theta)=0\implies X^{T}X\theta=X^{T}Y.
$$
{{% /details %}}


{{% details title="Theorem" %}}
The least squares estimator $\widehat{\theta}^{\text{LS}}$ satisfies 

$$
\mathbb{E}\left[\operatorname{MSE}(X\widehat{\theta}^{\text{LS}})\right]=\frac{1}{n}\mathbb{E}[\Vert X\widehat{\theta}^{\text{LS}}-X\theta^{\ast}\Vert^{2}]\lesssim\sigma^{2}\frac{r}{n}
$$

where $r=\operatorname{rank}(X^{T}X).$ Moreover, for any $\delta>0,$ with probability at least $1-\delta ,$ we have

$$
\operatorname{MSE}(X\widehat{\theta}^{\text{LS}})=\frac{1}{n}\Vert X\widehat{\theta}^{\text{LS}}-X\theta^{\ast}\Vert^{2}\lesssim\sigma^{2}\frac{r+\log(1/\delta)}{n}.
$$
{{% /details %}}

{{% details title="Proof" closed="true" %}}

By definition of $\widehat{\theta}^{\text{LS}},$ we have

$$
\Vert Y-X\widehat{\theta}^{\text{LS}}\Vert_{2}^{2}\leq\Vert Y-X\theta^{\ast}\Vert_{2}^{2}=\Vert\epsilon\Vert_{2}^{2}.
$$

Moreover, 

$$
\begin{aligned}
\Vert Y-X\widehat{\theta}^{\text{LS}}\Vert_{2}^{2} &= \Vert X\theta^{\ast}+\epsilon-X\widehat{\theta}^{\text{LS}}\Vert_{2}^{2} \\ &=\Vert X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})\Vert_{2}^{2}+\Vert\epsilon\Vert_{2}^{2}-2\epsilon^{T}X(\theta^{\ast}-\widehat{\theta}^{\text{LS}}).
\end{aligned}
$$

Combining this with the first inequality, we get

$$
\Vert X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})\Vert_{2}^{2}\leq2\epsilon^{T}X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})=2\Vert X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})\Vert_{2}\frac{\epsilon^{T}X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})}{\Vert X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})\Vert_{2}}.
$$

Let $\Phi\in\mathbb{R}^{n\times r}$ be an orthonormal basis for the column space of $X.$ We can write $X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})=\Phi\nu$ for some $\nu\in\mathbb{R}^{r}.$ Then

$$
\frac{\epsilon^{T}X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})}{\Vert X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})\Vert_{2}}=\frac{\epsilon^{T}\Phi\nu}{\Vert\Phi\nu\Vert_{2}}=\frac{\epsilon^{T}\Phi\nu}{\Vert\nu\Vert_{2}}=\tilde{\epsilon}^{T}\frac{\nu}{\Vert\nu\Vert_{2}}\leq\sup_{u\in\mathcal{B}_{2}}\widetilde{\epsilon}^{T}u
$$

where $\widetilde{\epsilon}=\Phi^{T}\epsilon.$ Therefore, 

$$
\Vert X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})\Vert_{2}^{2}\leq4\left(\sup_{u\in\mathcal{B}_{2}}\widetilde{\epsilon}^{T}u\right)^{2}.
$$

For $u\in\mathcal{S}^{r-1},$ we have $\Vert\Phi u\Vert_{2}=\Vert u\Vert_{2}=1,$ so 

$$
\mathbb{E}\left[e^{s\widetilde{\epsilon}^{T}u}\right]=\mathbb{E}\left[e^{s\epsilon^{T}\Phi u}\right]\leq e^{s^{2}\sigma^{2}/2},
$$

which shows that $\widetilde{\epsilon}\sim\operatorname{subG} _ {r}(\sigma^{2}).$ Using the bounds on moments for sub-Gaussian variables, we have

$$
4\mathbb{E}\left[\sup_{u\in\mathcal{B}_{2}}(\widetilde{\epsilon}^{T}u)^{2}\right]\leq4\sum_{i=1}^{r}\mathbb{E}[\widetilde{\epsilon}_{i}^{2}]\le4rc^{2}\frac{4!}{2^{2}}\sigma^{2}\lesssim\sigma^{2}r.
$$

For the probability, recall from a proof in the previous lecture that if $X\sim\operatorname{subG}_{d}(\sigma^{2})$ then 

$$
\mathbb{P}\left[\max_{\theta\in\mathcal{B}_{2}}\theta^{T}X\leq\sigma\sqrt{8d\log(6)}+2\sigma\sqrt{2\log(1/\delta)}\right]\geq1-\delta.
$$

Using this result, we get that

$$
\mathbb{P}\left[\max_{u\in\mathcal{B}_{2}}(\widetilde{\epsilon}^{T}u)^{2}\lesssim\sigma^{2}(r+\log(1/\delta))\right]\geq1-\delta 
$$

which yields the required probability bound. 

{{% /details %}}

{{< callout type="info" >}}
The inequality $\Vert Y-X\widehat{\theta}^{\text{LS}}\Vert_{2}^{2}\leq\Vert Y-X\theta^{\ast}\Vert_{2}^{2}=\Vert\epsilon\Vert_{2}^{2}$ is known as the fundamental inequality. 
{{< /callout >}}

Note that in the traditional case where $d\leq n,$ we have

$$
\Vert\theta^{\ast}-\widehat{\theta}^{\text{LS}}\Vert_{2}^{2}\leq\frac{\operatorname{MSE}(X\widehat{\theta}^{\text{LS}})}{\lambda_{\min}\left(\frac{X^{T}X}{n}\right)},
$$

so we could use the MSE bound we just proved to bound the difference on the regression coefficient. In the high-dimensional case, it is not possible to bound this error without more structural assumptions. 

## Sparsity constraints

In high dimensions, because the system is underdetermined, we need to inform the recovery of $\theta^{\ast}$ by assuming some structure on $\theta.$ The most common assumption made is that of sparsity. There are several variations around this theme. 

- Hard sparsity: Here, we assume that the support set $S(\theta^{\ast})=\\{j\in [d]:\theta_{j}^{\ast}\neq0\\}$ has cardinality $s\ll d.$ 

- Weak sparsity: Assuming that the model is exactly supported on $s$ coefficients may be overly restrictive, so it is useful to consider various relaxations. Roughly speaking, $\theta^{\ast}$ is said to be weakly sparse if it can be closely approximated by a sparse vector. One family of weakly sparse vectors can be defined using the $\ell_{q}$-norm. Consider the $\ell_{q}$-norm ball of radius $R_{q},$ given by

	$$
\mathbb{B}_{q}(R_{q})=\left\{ \theta\in\mathbb{R}^{d}:\sum_{j=1}^{d}|\theta_{j}|^{q}\leq R_{q}^{q}\right\} .
$$

	In the special case $q=0,$ any vector $\theta^{\ast}\in\mathbb{B} _ {0}(R _ {0})$ can have at most $R_{0}$ non-zero entries, so this reduces to hard sparsity. 

As we will see later, dealing with sparsity constraints will often require developing different estimators depending on not just assumptions on $\theta$ but also on the design matrix $X$ and noise $\epsilon.$ 

## Constrained least squares

Suppose that we know a priori that $\theta$ lies in a symmetric convex set $K\subset\mathbb{R}^{d}$. In this case, a natural estimator of $\theta$ is the solution to the constrained least squares problem given by

$$
\widehat{\theta}_{K}^{\text{LS}}\in\argmin_{\theta\in K}\Vert Y-X\theta\Vert_{2}^{2}.
$$

Note that 

$$
\Vert X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})\Vert_{2}^{2}\leq2\epsilon^{T}X(\theta^{\ast}-\widehat{\theta}^{\text{LS}})\leq2\sup_{\theta\in K-K}(\epsilon^{T}X\theta).
$$

Since $K$ is symmetric and convex, we have $K-K=2K,$ so $2\sup_{\theta\in K-K}(\epsilon^{T}X\theta)=4\sup_{v\in XK}(\epsilon^{T}v).$ This quantity here can be understood as a measure of the size of $XK.$

### $\ell_{1}$ constrained least square

Let us consider a special case. Suppose that $K=\mathcal{B} _ {1}$ is the $\ell _ {1}$ unit ball of $\mathbb{R}^{d}.$ The $\ell _ {1}$ unit ball is a convex polytope with exactly $2d$ vertices given by $e_{1},-e_{1},\ldots,e_{d},-e_{d}$ where $e_{j}$ is the $j$th vector of the standard basis of $\mathbb{R}^{d}.$ The set $XK$ is also a convex polytope, with at most $2d$ vertices $X_{1},-X_{1},\ldots,X_{d},-X_{d}$ where $X_{j}$ is the $j$th column of $X.$

{{% details title="Theorem" %}}
Let $K=\mathcal{B} _ {1}$ and assume that $\theta^{\ast}\in\mathcal{B} _ {1}.$ Moreover, assume that the columns of $X$ are normalized in such a way that $\max_{j}\Vert X_{j}\Vert_{2}\leq\sqrt{n}.$ Then the constrained least squares estimator $\widehat{\theta}_{\mathcal{B} _ {1}}^{\text{LS}}$ satisfies

$$
\mathbb{E}\left[\operatorname{MSE}(X\widehat{\theta}_{\mathcal{B}_{1}}^{\text{LS}})\right]=\frac{1}{n}\mathbb{E}[\Vert X\widehat{\theta}_{\mathcal{B}_{1}}^{\text{LS}}-X\theta^{\ast}\Vert_{2}^{2}]\lesssim\sigma\sqrt{\frac{\log(d)}{n}}.
$$

Moreover, for any $\delta>0,$ with probability at least $1-\delta ,$ we have

$$
\operatorname{MSE}(X\widehat{\theta}_{\mathcal{B}_{1}}^{\text{LS}})=\frac{1}{n}\Vert X\widehat{\theta}_{\mathcal{B}_{1}}^{\text{LS}}-X\theta^{\ast}\Vert^{2}_2\lesssim\sigma\sqrt{\frac{\log(d/\delta)}{n}}.
$$
{{% /details %}}

{{% details title="Proof" closed="true" %}}
We have established that

$$
\Vert X\widehat{\theta}_{\mathcal{B}_{1}}^{\text{LS}}-X\theta^{\ast}\Vert^{2}\leq4\sup_{v\in X\mathcal{B}_{1}}(\epsilon^{T}v).
$$

Since $\epsilon\sim\operatorname{subG} _ {n}(\sigma^{2})$ and $\Vert X_{j}\Vert_{2}\leq\sqrt{n}$ for all $j,$ for any $z\in\mathcal{B} _ {1}$ we have $\Vert Xz\Vert_{2}=\Vert\sum_{i=1}^{d}z_{i}X_{i}\Vert_{2}\leq\sum_{i=1}^{d}|z_{i}|\Vert X_{i}\Vert_{2}\leq\sqrt{n}.$ Hence, we have $\epsilon^{T}v\sim\operatorname{subG}(n\sigma^{2})$ for all $v\in X\mathcal{B} _ {1}.$ By the theorem on the bound of the maximum of scalar products over a convex polytope, we have

$$
\mathbb{E}\left[\operatorname{MSE}(X\widehat{\theta}_{\mathcal{B}_{1}}^{\text{LS}})\right]\leq\frac{4}{n}\mathbb{E}\left[\sup_{v\in X\mathcal{B}_{1}}(\epsilon^{T}v)\right]\leq\frac{4\sqrt{n}\sigma\sqrt{2\log(2d)}}{n}\lesssim\sigma\sqrt{\frac{\log d}{n}}.
$$

Also, we have

$$
\mathbb{P}\left[\operatorname{MSE}(X\widehat{\theta}_{\mathcal{B}_{1}}^{\text{LS}})>t\right]\leq\mathbb{P}\left[\frac{4}{n}\sup_{v\in X\mathcal{B}_{1}}(\epsilon^{T}v)>t\right]\leq2de^{-\frac{nt^{2}}{32\sigma^{2}}}.
$$

To conclude, we note that $2de^{-\frac{nt^{2}}{32\sigma^{2}}}\leq\delta$ holds whenever $t^2 \geq \frac{32\sigma^{2}}{n}\left(\log(2d)+\log(1/\delta)\right).$

{{% /details %}}

{{< callout type="info" >}}
The results for the unconstrained case also apply to $\widehat{\theta} _ {\mathcal{B} _ {1}}^{\text{LS}}$ (you can follow the same proof and see that it indeed works). Thus, we have 

$$
\mathbb{E}\left[\operatorname{MSE}(X\widehat{\theta}_{\mathcal{B}_{1}}^{\text{LS}})\right]\lesssim\min\left(\frac{\sigma^{2}r}{n},\sigma\sqrt{\frac{\log(d)}{n}}\right).
$$
{{< /callout >}}

