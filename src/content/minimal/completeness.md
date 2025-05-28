# Completeness

Another method of finding minimal sufficient statistics is called completeness. The idea is to remove ancillary information. For example, if $X_{1}$ and $X_{2}$ are i.i.d. $N(\theta,1)$, then we know that $(X_{1},X_{2})$ is not a minimal sufficient statistic because it is equivalent to $(X_{1}-X_{2},X_{1}+X_{2})$, and we know from before that $X_{1}+X_{2}$ is minimal sufficient. To be formal, we say that a statistic $A = A(X)$ is ancillary if its distribution does not depend on $\theta$, and we say it is first-order ancillary if $\mathbb{E} _ \theta A(X)$ does not depend on $\theta$. 

<details open>
<summary>Definition</summary>

A statistic $T=T(X)$ is complete if $\mathbb{E}_{\theta}f(T)=0$ for all $\theta\in\Theta$ implies $f(T(X))=0$ almost surely for all $\theta\in\Theta$. Equivalently, no non-constant function of $T$ is first-order ancillary. 

</details>

Then we have the following result.

<details open>
<summary>Bahadur's Theorem</summary>

If $T$ is sufficient and complete, then it is minimal sufficient.

</details>

<details>
<summary>Sketch of proof</summary>

Assume that a minimal sufficient statistic $U$ exists. By definition, we have $U=h(T)$ for some measurable function $h$. We want to show that $T$ is also a function of $U$. Define $g(u)=\mathbb{E} _ \theta[T|U=u]$. Note that $g$ does not depend on $\theta$  because $U$ is sufficient. Then $\mathbb{E} _ \theta g(h(T))=\mathbb{E} _ \theta g(U)=\mathbb{E} _ {\theta}\left[\mathbb{E} _ \theta \left[T|U\right]\right]=\mathbb{E} _ \theta T$, so $\mathbb{E}_{\theta}\left[g(h(T))-T\right]=0$. By completeness of $T$, it follows that $g(U)=g(h(T))=T$ almost surely. 

</details>

Let us look at a few concrete examples of how this can be used to find minimal sufficient statistics. 

<details open>
<summary>Example</summary>

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Ber}(\theta)$ where $\theta\in(0,1)$. Let $T(X)=\sum_{i=1}^{n}X_{i}\sim\text{Binomial}(n,\theta)$. Suppose $\mathbb{E}_{\theta}f(T(X))=0$ for all $\theta\in(0,1)$. Then 

$$
0=\sum_{i=1}^{n}f(i)\binom{n}{i}\theta^{i}(1-\theta)^{n-i}=(1-\theta)^{n}\sum_{i=1}^{n}f(i)\binom{n}{i}\left(\frac{\theta}{1-\theta}\right)^{i},
$$

so 

$$
\sum_{i=1}^{n}f(i)\binom{n}{i}\left(\frac{\theta}{1-\theta}\right)^{i}=0\quad\text{for all }\theta\in(0,1).
$$

Set $\beta=\frac{\theta}{1-\theta}$. Then 

$$
\sum_{i=1}^{n}f(i)\binom{n}{i}\beta^{i}=0\quad\text{for all }\beta>0.
$$

This means that the polynomial $p(x)=\sum_{i=1}^{n}f(i)\binom{n}{i}x^{i}=0$ has infinitely many roots, which can only occur if all coefficients vanish. Therefore, $f(i)=0$ for all $i=1,\ldots,n$. This shows that $T$ is complete.
</details>


<details open>
<summary>Example</summary>

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Unif}(0,\theta)$ where $\theta>0$. Let $T(X)=X_{(n)}$. Suppose $\mathbb{E}_{\theta}f(T(X))=0$ for all $\theta>0$. Then 

$$
G(\theta)=\int_{0}^{\theta}t^{n-1}f(t)\,dt=0\quad\text{for all }\theta>0.
$$

By the Lebesgue differentiation theorem, $G'(\theta)=\theta^{n-1}f(\theta)$ almost everywhere. Since $G=0$, we have $G'=0$, so $f=0$ almost everywhere.
</details>


<details open>
<summary>Example</summary>

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\theta,1)$ where $\theta\in\mathbb{R}$. Let $T(X)=\frac{1}{\sqrt{n}}\sum_{i=1}^{n}X_{i}\sim N(\theta,1)$. Suppose $\mathbb{E} _ {\theta} f(T(X)) = 0$ for all $\theta\in\mathbb{R}$. Then 

$$
\int_{\mathbb{R}}f(x)e^{-\frac{1}{2}(x-\theta)^{2}}\,dx=0\quad\text{for all }\theta\in\mathbb{R}.
$$

This implies the integrand vanishes almost everywhere on $\mathbb{R},$ so we must have $f=0$ almost everywhere. 
</details>

<details open>
<summary>Example</summary>

For full rank minimal exponential family $(P_{\eta}:\eta\in H)$, $T$ is complete. 
</details>
