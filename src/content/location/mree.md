# Minimal risk equivariant estimators

A family of distributions $(P_{\theta}:\theta\in\mathbb{R}^{p})$ is called a location model if $X\sim P_{\theta}\iff X-\theta\sim P_{0}$. Assuming densities exist, it is easy to verify that

$$
P_{\theta}(x)=f(x-\theta)
$$

where $f(x)=P_{0}(x)$. We say that an estimator $\widehat{\theta}(X)=\widehat{\theta}(X_{1},\ldots,X_{n})$ is location equivariant if

$$
\widehat{\theta}(X + c)=\widehat{\theta}(X)+c.
$$

We assume that the loss function $L$ is location invariant, meaning that 

$$
L(\widehat{\theta}+c,\theta+c)=L(\widehat{\theta},\theta).
$$

As a consequence of location invariance, we have $L(\widehat{\theta},\theta)=L(\widehat{\theta}-\theta,0)=:\rho(\widehat{\theta}-\theta)$, so the loss function can be written as a function of the $\widehat{\theta} - \theta$. 

<details open>
<summary>Theorem</summary>

For a location model $(P_{\theta}:\theta\in\mathbb{R}^{p})$, a location invariant loss $L(\widehat{\theta},\theta)$, and a location equivariant estimator $\widehat{\theta}$, the risk $\mathbb{E}_{\theta}[L(\widehat{\theta},\theta)]$ must be constant. 
</details>

<details>
<summary>Proof</summary>

For all $\theta\in\mathbb{R}^{p}$, we have $\mathbb{E} _ {\theta}L(\widehat{\theta},\theta)=\mathbb{E} _ {\theta}\rho(\widehat{\theta}-\theta)=\mathbb{E} _ {\theta}\rho(\widehat{\theta}(X_{1},\ldots,X_{n})-\theta)=\mathbb{E} _ {\theta}\rho(\widehat{\theta}(X_{1}-\theta,\ldots,X_{n}-\theta))=\mathbb{E} _ {0}\rho(\widehat{\theta}(X_{1},\ldots,X_{n})).$ 
</details>

We are particularly interested in equivariant estimators with the lowest risk. 

<details open>
<summary>Definition</summary>

A minimal risk equivariant estimator (MREE) is an equivariant estimator which has the lowest risk among all equivariant estimators. 

</details>

The strategy to finding the minimal risk location equivariant estimator is to start with a pilot estimator $\delta_{0}(X)$ which can be any location equivariant estimator. Then we set

$$
\delta(X)=\delta_{0}(X)-u(X).
$$

Note that $u(X+c)=\delta_{0}(X+c)-\delta(X+c)=\delta_{0}(X)+c-\delta(X)-c=\delta_{0}(X)-\delta(X)=u(X)$. Taking $c=-X_{n}$, we have

$$
u(X_{1},\ldots,X_{n})=u(X_{1}-X_{n},\ldots,X_{n-1}-X_{n},0).
$$

Let $Y=(X_{1}-X_{n},\ldots,X_{n-1}-X_{n})$ and write $u(X)=v(Y)$. Then the risk of $\delta(X)$ is

$$
\mathbb{E}_{\theta}\rho(\delta(X)-\theta)=\mathbb{E}_{0}\rho(\delta(X))=\mathbb{E}_{0}\rho(\delta_{0}(X)-v(Y))
$$

We can write this expectation as $\mathbb{E} _ {0}[\mathbb{E} _ {0}(\rho(\delta_{0}(X)-v(Y))|Y)]$, so to minimize the risk we should choose

$$
v(Y)=\argmin_{a}\mathbb{E}_{0}(\rho(\delta_{0}(X)-a)|Y).
$$

In particular, when $\rho(t)=t^{2}$, $v(Y)=\mathbb{E} _ {0}(\delta_{0}(X)|Y)$. 

<details open>
<summary>Example</summary>

Suppose that $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\theta,1)$. Let $\delta_{0}(X)=\overline{X}$. Then $\mathbb{E} _ {0}(\overline{X}|Y) = \mathbb{E} _ {0}(\overline{X}) = 0$, so $\delta(X)=\overline{X}$ is MREE. 
</details>

<details open>
<summary>Example</summary>

Suppose that $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}E(\theta,b)$ where $b$ is known where the density is given by $P_{\theta}(x)= b^{-1}e^{-\frac{(x-\theta)}{b}}1(x > \theta).$ Let $\delta_{0}(X)=X_{(1)}$. Then since $Y$ is ancillary, $\mathbb{E} _ {0}(X_{(1)}|Y) = \mathbb{E} _ {0}(X_{(1)})$. To evaluate this expectation, write $X_{i}=\theta+bZ_{i}$ where $Z_{i} \sim E(0,1)$. Then $X_{(1)}=\theta+bZ_{(1)}$. We have 

$$
\mathbb{P}(Z_{(1)}\leq t)=1-\mathbb{P}(Z_{(1)}>t)=1-\prod_{i=1}^{t}\mathbb{P}(Z_{i}>t)=1-e^{-nt}.
$$

The density of $Z_{(1)}$ is then $ne^{-nt}1_{\\{t>0\\}}$ which has mean $\frac{1}{n}$. Therefore, $\mathbb{E} _ {0}(X_{(1)}) = \frac{b}{n}$, which gives the MREE

$$
\delta(X)=X_{(1)} - \frac{b}{n}.
$$
</details>

We also have the following connection between the MREE and UMVUE.

<details open>
<summary>Lemma</summary>

Suppose that $\rho(t)=t^{2}$. If the UMVUE exists and is location equivariant, then the MREE and UMVUE coincide. 

</details>

<details>
<summary>Proof</summary>

Let $\delta(X)$ denote any location equivariant estimator. The bias is given by $\mathbb{E}_\theta [\delta(X) - \theta] = \mathbb{E}_\theta [\delta(X - \theta)] = \mathbb{E}_0[\delta(X)],$ which is constant. Denote the bias by $b.$ Then note that $R(\delta(X), \theta) = \mathbb{E}_\theta[(\delta(X) - \theta)^2] = \operatorname{Var}_\theta [\delta(X) - \theta] + b^2 = R(\delta(X) - b, \theta) + b^2,$ so $\delta(X) - b$ has smaller risk than $\delta(X).$ It follows that the MREE must be unbiased. Since the risk for an unbiased estimator under squared loss is equal to its variance, it follows that the MREE and UMVUE coincide. 

</details>



