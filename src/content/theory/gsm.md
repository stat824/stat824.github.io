# Estimation in the Gaussian sequence model

We study a prototypical high-dimensional problem to illustrate how concentration inequalities and structural assumptions can tame a seemingly intractable problem. Consider the Gaussian sequence model

$$
Y_{i}=\theta_{i}+\sigma_{n}\epsilon_{i},\quad\epsilon_{i}\sim N(0,1),\quad i=1,2,\ldots,n.
$$

What is a good estimator for the parameter $\theta\in\mathbb{R}^{n}$? A natural choice is to use $\widehat{\theta}=Y.$ There are good reasons to justify the use of this estimator: it is the MLE, the minimal-variance unbiased estimator, and it is minimax over the parameter space $\Theta=\mathbb{R}^{n}.$ But it has pretty terrible risk given by $\mathbb{E}[\Vert\widehat{\theta}-\theta\Vert_{2}^{2}]=n\sigma_{n}^{2}.$ To do better, we need to rely on assumptions on the structure of $\theta$ to inform the recovery. Can we do better if we make the assumption that only $k$ of the coordinates of $\theta$ are nonzero? Certainly it is possible for an “oracle” with knowledge of the underlying support $S\subset[d]$ to achieve better risk, using the estimator

$$
\widehat{\theta}_{j}^{0}=\begin{cases}
Y_{j} & \text{if }j\in S,\\
0 & \text{if }j\not\in S.
\end{cases}
$$

This estimator achieves the better risk $\mathbb{E}[\Vert\widehat{\theta}-\theta\Vert_{2}^{2}]=k\sigma_{n}^{2}.$ In most cases, this estimator cannot actually be implemented since we do not have access to the true support $S.$

## Hard thresholding

We can do almost as well as the oracle risk $k\sigma_{n}^{2}$ by guessing the support of $\theta$  and mimicking the oracle on the estimated support $\widehat{S}.$ A natural way to construct $\widehat{S}$ is to guess that $j\in S$ whenever $|Y_{j}|\geq\tau$ holds for some threshold $\tau > 0.$ This gives rise to the hard-thresholding estimator:

$$
\widehat{\theta}_{j}^{\tau}=\begin{cases}
Y_{j} & \text{if }|Y_{j}|\geq\tau,\\
0 & \text{if }|Y_{j}|<\tau.
\end{cases}
$$

We have the following bound on the risk of the hard thresholding estimator. 

<details open>
<summary>Theorem</summary>

Suppose that $\theta$ is $k$-sparse. There exist universal constants $C_{1},C_{2}>0$ such that

$$
\mathbb{E}[\Vert\widehat{\theta}^{\tau}-\theta\Vert^{2}]\leq k\sigma_{n}^{2}+C_{1}k(\tau^{2}+\sigma_{n}^{2})+C_{2}n\sigma_{n}^{2}\exp\left(-\frac{\tau^{2}}{4\sigma_{n}^{2}}\right).
$$
</details>

<details>
<summary>Proof</summary>

Let $S$ be the support of $\theta.$ We will first find an upper bound on $\mathbb{E}[(\widehat{\theta} _ {j}-\theta _ {j})^{2}]$ for $j\in S.$ Given $j\in S,$

$$
\mathbb{E}[(\widehat{\theta} _ {j}-\theta _ {j})^{2}]\leq\mathbb{E}[(Y_{j}-\theta_{j})^{2}]+\theta_{j}^{2}\mathbb{P}[|Y_{j}|\leq\tau].
$$

Consider first the case where $\theta_{j}\geq\tau.$ In this case,

$$
|Y_{j}|\leq\tau\implies\theta_{j}+\sigma_{n}\epsilon_{j}<\tau\implies\theta_{j}-\tau\leq-\sigma_{n}\epsilon_{j}\implies(|\theta_{j}|-\tau)_{+}\leq-\sigma_{n}\epsilon_{j}.
$$

Since $-\sigma_{n}\epsilon_{j}\sim N(0,\sigma_{n}^{2}),$ by the sub-Gaussian Chernoff bound, we have

$$
\mathbb{P}[|Y_{j}|\leq\tau]\leq\mathbb{P}\left[-\sigma_{n}\epsilon_{j}\geq(|\theta_{j}|-\tau)_{+}\right]\leq\exp\left(\frac{-(|\theta_{j}|-\tau)_{+}^{2}}{2\sigma_{n}^{2}}\right).
$$

In the case where $\theta_{j}\leq-\tau,$ by similar reasoning we can also show $\mathbb{P}[|Y _ {j}|\leq\tau] \leq \exp\left(\frac{-(|\theta _ {j}|-\tau) _ {+}^{2}}{2\sigma _ {n}^{2}}\right).$ Finally, this inequality holds trivially in the case where $|\theta _ {j}|<\tau .$ Using the fact that for $u\geq0,$ there exists a constant $C_{1}$ such that $u^{2}\exp\left(\frac{-(u-\tau) _ {+}^{2}}{2\sigma _ {n}^{2}}\right)\leq C_{1}(\tau^{2}+\sigma_{n}^{2}),$ it follows that for $j\in S,$ we have

$$
\mathbb{E}[(\widehat{\theta}_{j}-\theta_{j})^{2}]\leq\sigma_{n}^{2}+\theta_{j}^{2}\exp\left(\frac{-(|\theta_{j}|-\tau)_{+}^{2}}{2\sigma_{n}^{2}}\right)\leq\sigma_{n}^{2}+C_{1}(\sigma_{n}^{2}+\tau^{2}).
$$

For $j\not\in S,$ note that

$$
\begin{aligned}
\mathbb{E}[(\widehat{\theta}_{j}-\theta_{j})^{2}] &= \mathbb{E}\left[|\sigma_{n}\epsilon_{j}|^{2}\mathbf{1}(|\epsilon_{j}|\geq\frac{\tau}{\sigma_{n}})\right] \\
	&\leq\sqrt{\mathbb{E}[\sigma_{n}^{4}\epsilon_{j}^{4}]\mathbb{P}\left[|\epsilon_{j}|\geq\frac{\tau}{\sigma_{n}}\right]} \\
	&=\sqrt{3}\sigma_{n}^{2}\sqrt{\mathbb{P}\left[|\epsilon_{j}|\geq\frac{\tau}{\sigma_{n}}\right]} \\
	&\leq\sqrt{3}\sigma_{n}^{2}\sqrt{2\exp\left(-\frac{\tau^{2}}{2\sigma_{n}^{2}}\right)} \\
	&=\sqrt{6}\sigma_{n}^{2}\exp\left(-\frac{\tau^{2}}{4\sigma_{n}^{2}}\right).
\end{aligned}
$$

The complete $\ell_{2}$ risk for the hard thresholding estimator is then bounded by

$$
\begin{aligned}
\mathbb{E}[\Vert\widehat{\theta}-\theta\Vert_{2}^{2}] &= \sum_{j\in S}\mathbb{E}[(\widehat{\theta}_{j}-\theta_{j})^{2}]+\sum_{j\not\in S}\mathbb{E}[(\widehat{\theta}_{j}-\theta_{j})^{2}] \\
	&\leq\sigma_{n}^{2}|S|+C_{1}|S|(\sigma_{n}^{2}+\tau^{2})+C_{2}|[n]\backslash S|\sigma_{n}^{2}\exp\left(-\frac{\tau^{2}}{4\sigma_{n}^{2}}\right) \\
	&\leq k\sigma_{n}^{2}+C_{1}k(\tau^{2}+\sigma_{n}^{2})+C_{2}n\sigma_{n}^{2}\exp\left(-\frac{\tau^{2}}{4\sigma_{n}^{2}}\right).
\end{aligned}
$$
</details>


We need to choose an appropriate value for $\tau.$ Since $\Vert\sigma_{n}\epsilon\Vert_{\infty}\lesssim\sigma_{n}\sqrt{2\log n},$ a reasonable approach is to set $\tau\approx\sigma_{n}\sqrt{2\log n}.$ In fact, one can check that the following holds. 

<details open>
<summary>Theorem</summary>

Let $\tau=2\sigma_{n}\sqrt{\log(n/k)}.$ Then

$$
\sup_{\Vert\theta\Vert_{0}\leq k}\mathbb{E}[\Vert\widehat{\theta}^{\tau}-\theta\Vert_{2}^{2}]\le Ck\sigma_{n}^{2}(1+\log(n/k))
$$

for some universal constant $C>0.$
</details>



## Soft thresholding

Instead of just chopping off observations, we can also shrink them. For $v\in\mathbb{R},$ define the soft thresholding operator to be

$$
S_{\lambda}(v)=\operatorname{sgn}(v)(|v|-\lambda)_{+}=\argmin_{u\in\mathbb{R}}\left\{ \frac{1}{2}(u-v)^{2}+\lambda|u|\right\} .
$$

Then for $v\in\mathbb{R}^{n},$ we can define analogously 

$$
S_{\lambda}(v)=\argmin_{u\in\mathbb{R}^{n}}\left\{ \frac{1}{2}\Vert u-v\Vert_{2}^{2}+\lambda\Vert u\Vert_{1}\right\} =(S_{\lambda}(v_{1}),\ldots,S_{\lambda}(v_{n}))^{T}.
$$

We then define the soft thresholding estimator by $\widehat{\theta}=S_{\lambda}(Y).$

<details open>
<summary>Theorem</summary>

Suppose that $\theta$ is $k$-sparse. If $\widehat{\theta}$ is the soft-thresholding estimator with $\lambda=\sqrt{2\sigma_{n}^{2}\log(n/k)},$ then

$$
\mathbb{E}[\Vert\widehat{\theta}-\theta\Vert_{2}^{2}]\leq Ck\sigma_{n}^{2}(1+\log(n/k)).
$$
</details>

<details>
<summary>Proof</summary>

If $\theta_{j}=0,$ then

$$
\begin{aligned}
\mathbb{E}[(\widehat{\theta}_{j}-\theta_{j})^{2}] &=\mathbb{E}[(\sigma_{n}|\epsilon_{j}|-\lambda)_{+}^{2}] \\
	&=\int_{0}^{\infty}\mathbb{P}[(\sigma_{n}|\epsilon_{j}|-\lambda)_{+}^{2}>\alpha]\,d\alpha \\
	&\leq\int_{0}^{\infty}\mathbb{P}[\sigma_{n}|\epsilon_{j}|-\lambda>\sqrt{\alpha}]\,d\alpha \\
	&=2\int_{\lambda}^{\infty}(t-\lambda)\mathbb{P}[\sigma_{n}|\epsilon_{j}|>t]\,dt \\
	&\leq2\int_{\lambda}^{\infty}t\mathbb{P}[\sigma_{n}|\epsilon_{j}|>t]\,dt \\
	&\leq4\int_{\lambda}^{\infty}t\exp\left(-\frac{t^{2}}{2\sigma_{n}^{2}}\right)\,dt \\
	&=4\sigma_{n}^{2}\exp\left(-\frac{\lambda^{2}}{2\sigma_{n}^{2}}\right).
\end{aligned}
$$

If $\theta_{j}\neq0,$ since $S_{\lambda}$ is 1-Lipschitz, we have

$$
\begin{aligned}
\mathbb{E}[(\widehat{\theta}_{j}-\theta_{j})^{2}] &= \mathbb{E}[(\widehat{\theta}_{j}-S_{\lambda}(\theta_{j})+S_{\lambda}(\theta_{j})-\theta_{j})^{2}] \\
	&\leq2\mathbb{E}[(\widehat{\theta}_{j}-S_{\lambda}(\theta_{j}))^{2}]+2(S_{\lambda}(\theta_{j})-\theta_{j})^{2} \\
	&=2\mathbb{E}[(S_{\lambda}(Y_{j})-S_{\lambda}(\theta_{j}))^{2}]+2(S_{\lambda}(\theta_{j})-\theta_{j})^{2} \\
	&\leq2\mathbb{E}[(Y_{j}-\theta_{j})^{2}]+2\lambda^{2} \\
	&=2\sigma_{n}^{2}+2\lambda^{2}.
\end{aligned}
$$
Combining these two cases and substituting in $\lambda=\sqrt{2\sigma_{n}^{2}\log(n/k)},$ we have

$$
\begin{aligned}
\mathbb{E}[\Vert\widehat{\theta}-\theta\Vert_{2}^{2}] &\leq 2k(\sigma_{n}^{2}+\lambda^{2})+4n\sigma_{n}^{2}\exp\left(-\frac{\lambda^{2}}{2\sigma_{n}^{2}}\right) \\
	&=2k(\sigma_{n}^{2}+2\sigma_{n}^{2}\log(n/k))+4k\sigma_{n}^{2} \\
	&\leq Ck\sigma_{n}^{2}(1+\log(n/k)). 
\end{aligned}
$$
</details>
