---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Gaussian Sequence Model'
weight: 7
---

## The problem of density estimation

Let $(\varphi _ {j}) _ {j=1}^{\infty}$ be the orthonormal basis for $L^{2}([0,1])$ given by $\\{ 1, \sqrt{2}\sin(2\pi j\cdot), \sqrt{2}\cos(2\pi j\cdot) : j=1,2,\ldots \\}.$ Given $\alpha>0$, we define the Sobolev ball

$$
S_{\alpha}(R)=\left\{ f\in L^{2}([0,1]),\,f=\sum_{j}\theta_{j}\varphi_{j},\,f\geq0,\:\int f=1,\,\sum_{j}j^{2\alpha}\theta_{j}^{2}\leq R^{2}\right\} .
$$

The parameter $\alpha$ is called the smoothness parameter because for a function $f\in C^{\alpha}([0,1])$ with Fourier series expansion $f(x)=a_{0}+\sum_{j=1}^{\infty}\left(a_{j}\sin(2\pi jx)+b_{j}\cos(2\pi jx)\right)$, we have

$$
\Vert f^{(\alpha)}\Vert^{2}=a_{0}^{2}+\frac{1}{2}\sum_{j=1}^{\infty}(2\pi j)^{2\alpha}(a_{j}^{2}+b_{j}^{2}).
$$

Let $f_{1},\ldots,f_{n}\overset{\text{iid}}{\sim}f\in S_{\alpha}(R)$. Then estimating $f$ is equivalent to estimating the coefficients $\theta_{j}$. Since $\theta_{j}=\int f\varphi_{j}$, by the central limit theorem, we have

$$
\frac{1}{n}\sum_{i=1}^{n}\int f_{i}\varphi_{j}\overset{d}{\approx}N\left(\theta_{j},\frac{\text{Var}(\int f_{j}\varphi_{j})}{n}\right).
$$

However, instead of considering density estimation directly, we can consider an asymptotically equivalent model known as the Gaussian sequence model. Most nonparametric models such as the white noise model and nonparametric regression are asymptotically equivalent to the Gaussian sequence model. 

## Gaussian sequence model

In the Gaussian sequence model, we have observations $X_{j}=\theta_{j}+\frac{1}{\sqrt{n}}Z_{j}$ where $Z_{j}\overset{\text{iid}}{\sim}N(0,1)$ for $j=1,2,\ldots$ and $\theta=(\theta_{j})\in\Theta_{\alpha}(R)=\\{\theta:\sum_{j}j^{2\alpha}\theta_{j}^{2} \leq R^2\\}$. 

{{< callout type="info" >}}
Note that in the Gaussian sequence model, the observations are independent but not identically distributed. However, you can think of each observation to be the average of i.i.d. sequences $Y_1, \ldots, Y_n$ where $Y_{ij} = \theta_j + Z_{ij}$ and $Z_{ij} \overset{\text{iid}}{\sim} N(0,1)$.  
{{< /callout >}}

Consider the estimator $\widehat{\theta}$ where

$$
\widehat{\theta}_{j}=\begin{cases}
X_{j} & \text{if }j\leq k,\\
0 & \text{if }j>k.
\end{cases}
$$

Then the risk is

$$
\mathbb{E} _ \theta \Vert\widehat{\theta} - \theta\Vert^{2}	=\sum_{j=1}^{k}\mathbb{E}(X_{j}-\theta_{j})^{2}+\sum_{j>k}\theta_{j}^{2}=\frac{k}{n}+\sum_{j>k}\theta_{j}^{2}\leq\frac{k}{n}+\frac{R^{2}}{k^{2\alpha}}.
$$

If $k$ is small then $R^{2}k^{-2\alpha}$ is large while if $k$ is large then $kn^{-1}$ is large, so the threshold $k$ should be chosen to balance the two terms. Setting the terms to be equal, we find that $k\asymp n^{\frac{1}{2\alpha+1}}$. With this choice, we have

$$
\mathbb{E} _ \theta \Vert\widehat{\theta}-\theta\Vert^{2}\leq Cn^{-\frac{2\alpha}{2\alpha+1}}.
$$

This rate is optimal in the sense that the minimax risk is

$$
\inf_{\widehat{\theta}}\sup_{\theta\in\Theta_{\alpha}(R)}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2}=(1+o(1))C_{\alpha,R}n^{-\frac{2\alpha}{\alpha+1}},
$$

where $C_{\alpha,R}$ is called the Pinsker constant. However, an issue with this estimator is that the choice of the threshold $k$ requires knowledge of the smoothness parameter $\alpha$ which is not known. 

### Blockwise James-Stein estimator

Let us now consider the blockwise James-Stein estimator which does not require knowledge of the smoothness parameter. Let $\\{1,2,\ldots,n\\}=B_{1}\cup\cdots\cup B_{m}$, where $B_{\ell}=\{3^{\ell-1}+1,\ldots,3^{\ell}\}$ and $m=\log_{3} n$. Note that $X _ \ell \sim N(\theta _ {B _ \ell}, \frac{1}{n} I _ {|B_\ell|}).$ Consider the estimator

$$
\widehat{\theta}=\left(\begin{array}{c}
\widehat{\theta}_{B_{1}}\\
\widehat{\theta}_{B_{2}}\\
\vdots\\
\widehat{\theta}_{B_{m}}\\
0
\end{array}\right),\quad\widehat{\theta}_{B_{\ell}}=\left(1-\frac{|B_{\ell}|-2}{n\Vert X_{\ell}\Vert^{2}}\right) X_{\ell}.
$$

Then by the oracle inequality we have

$$
\begin{aligned}
\mathbb{E} _ \theta \Vert\widehat{\theta}-\theta\Vert^{2} &=\sum_{j=1}^{m}\mathbb{E}_ \theta \Vert\widehat{\theta}_{B_{\ell}}-\theta_{B_{\ell}}\Vert^{2}+\sum_{j>m}\theta_{j}^{2} \\
	&\leq\sum_{\ell=1}^{m}\min\left(\frac{|B_{\ell}|}{n},\Vert\theta_{B_{\ell}}\Vert^{2}\right)+\frac{2m}{n}+\sum_{j>n}\theta_{j}^{2}.
\end{aligned}
$$

Note that

$$
\frac{2m}{n}=\frac{\log_{3}n}{n}=o\left(n^{-\frac{2\alpha}{\alpha+1}}\right)\quad\text{and}\quad\sum_{j>n}\theta_{j}^{2}\leq\frac{R^{2}}{n^{2\alpha}}=o\left(n^{-\frac{2\alpha}{\alpha+1}}\right).
$$

Choosing $L=\min\\{\ell\in\mathbb{N}:3^{\ell}\geq n^{\frac{1}{2\alpha+1}}\\}$, we have $3^{L-1}\leq n^{\frac{1}{2\alpha+1}}\leq3^{L}$, so

$$
\begin{aligned}
\sum_{\ell=1}^{m}\min\left(\frac{|B_{\ell}|}{n},\Vert\theta_{B_{\ell}}\Vert^{2}\right)	&\leq\sum_{\ell=1}^{L}\frac{|B_{\ell}|}{n}+\sum_{\ell=L+1}^{m}\Vert\theta_{B_{\ell}}\Vert^{2} \\
	&\leq\sum_{\ell=1}^{L}\frac{2}{3n}3^{\ell}+\sum_{j>3^{L}}|\theta_{j}|^{2} \\
	&\lesssim \frac{3^{L}}{n}+\sum_{j>n^{\frac{1}{2\alpha+1}}}|\theta_{j}|^{2} \\
	&\lesssim \frac{n^{\frac{1}{2\alpha+1}}}{n}+\left(n^{\frac{1}{2\alpha+1}} \\\right)^{-2\alpha} \\
	&\lesssim n^{-\frac{2\alpha}{2\alpha+1}}.
\end{aligned}
$$

Adding up all the terms, we get $\mathbb{E} _ \theta \Vert\widehat{\theta} - \theta\Vert^{2}\lesssim n^{-\frac{2\alpha}{2\alpha+1}}$. So the block-wise James-Stein estimator also achieves the minimax rate. 