# Uniformly minimum variance unbiased estimators
We say that an estimator $\delta(X)$ is a uniformly minimum-variance unbiased estimator (UMVUE) for $g(\theta)$ if $\mathbb{E} _ {\theta}\delta(X)=g(\theta)$ for all $\theta\in\Theta$ and for any other estimator $\widetilde{\delta}(X)$ which is unbiased for $g(\theta)$, it holds that $\operatornamewithlimits{Var} _ {\theta}(\delta(X))\leq\operatornamewithlimits{Var} _ {\theta}(\widetilde{\delta}(X))$ for all $\theta\in\Theta$. 

<details open>
<summary>Lehmann-Scheffé Theorem</summary>

Suppose that $T$ is unbiased, sufficient, and complete for $\theta$. If $\delta(X)=h(T(X))$ is unbiased for $g(\theta)$, then

* $\delta(X)$ is the only function of $T(X)$ which is unbiased for $g(\theta)$,

* $\delta(X)$ is the unique UMVUE for $g(\theta)$.

</details>

<details>
<summary>Proof</summary>

Suppose that $\widetilde{h}(T(X))$ is also unbiased for $g(\theta)$. Then $\mathbb{E} _ {\theta}(\widetilde{h}(T(X))-h(T(X))) = 0$, so by completeness, it follows that $\widetilde{h}(T(X))=h(T(X))$ almost surely. To show the second statement, suppose that $\widetilde{\delta}(X)$ is unbiased for $g(\theta)$. Then $\mathbb{E} _ \theta (\widetilde{\delta}(X)|T(X))$ is also unbiased, so $\mathbb{E} _ \theta (\widetilde{\delta}(X)|T(X))=h(T(X))$. By the Rao-Blackwell theorem, 

$$
\mathbb{E}_{\theta}\left(\mathbb{E}_{\theta}(\widetilde{\delta}(X)|T(X))-g(\theta)\right)^{2}\leq\mathbb{E}_{\theta}\left(\widetilde{\delta}(X)-g(\theta)\right)^{2}.
$$

The left hand side is $\operatornamewithlimits{Var} _ {\theta}(h(T(X))$ and the right hand side is $\operatornamewithlimits{Var} _ {\theta}(\widetilde{\delta}(X))$. 

</details>


Suppose that we have a sufficient and complete $T(X)$. There are two methods to find UMVUEs:

1. Find a function $h$ such that $\mathbb{E} _ {\theta}h(T(X))=g(\theta)$ for all $\theta\in\Theta$.

2. Find $\delta(X)$ such that $\mathbb{E} _ {\theta}\delta(X)=g(\theta)$ for all $\theta\in\Theta$. The UMVUE is then $\mathbb{E}_ \theta (\delta(X)|T(X))$.

<details open>
<summary>Example</summary>

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Ber}(\theta)$ where $\theta\in(0,1)$. 

* UMVUE for $\theta$: The estimator $\widehat{\theta}=\overline{X}$ is unbiased, sufficient, and complete, it is the unique UMVUE.

* UMVUE for $\theta^{2}$: Since $\mathbb{E} _ \theta (X_{1}X_{2})=\theta^{2}$, the estimator $\delta(X)=\mathbb{E}(X_{1}X_{2}|\sum_{i=1}^{n}X_{i})$ is unbiased. Since $T(X) = \sum_{i=1}^{n}X_{i}$ is sufficient and complete for $\theta$, it follows that $\delta(X)$ is the UMVUE for $\theta^{2}$. 

</details>


<details open>
<summary>Example</summary>

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Unif}(0,\theta)$ where $\theta>0$. To find the UMVUE for $\theta$, we start with $\mathbb{E} _ {\theta}(2X_{1})=\theta$, so the UMVUE is $\mathbb{E} _ {\theta}(2X_{1}|X_{(n)})$. Since $X_{1}|X_{(n)}\sim\frac{1}{n}\delta_{X_{(n)}}+\left(1-\frac{1}{n}\right)\text{Unif}(0,X_{(n)})$, it follows that 

$$
\mathbb{E}_{\theta}(2X_{1}|X_{(n)})	=2\left(\frac{1}{n}X_{n}+\left(1-\frac{1}{n}\right)\frac{X_{n}}{2}\right)=\left(1+\frac{1}{n}\right)X_{(n)}.
$$
</details>


<details open>
<summary>Example</summary>

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\mu,\sigma^{2})$. A complete sufficient statistic is $\left(\sum_{i=1}^{n}X_{i},\sum_{i=1}^{n}X_{i}^{2}\right)$, which is equivalent to $\left(\overline{X},\sum_{i=1}^{n}(X_{i}-\overline{X})^{2}\right)$. The UMVUE for $\mu$ is $\overline{X}$, and the UMVUE for $\sigma^{2}$ is $\frac{1}{n-1}\sum_{i=1}^{n}(X_{i}-\overline{X})^{2}$. 

</details>

