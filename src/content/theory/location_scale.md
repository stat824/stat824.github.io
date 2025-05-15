# Location-scale equivariance

We say $(P_{\theta,\tau}:\theta\in\mathbb{R},\tau>0)$ is a location-scale family if $X\sim P_{\theta,\tau}\iff\frac{X-\theta}{\tau}\sim P_{0,1}$. If densities exist, then

$$
P_{\theta,\tau}(x)=\frac{1}{\tau}f\left(\frac{x-\theta}{\tau}\right)
$$

where $f(x)=P_{0,1}(x)$. An estimator $\widehat{\theta}(X)=\widehat{\theta}(X_{1},\ldots,X_{n})$ is said to be location-scale equivariant if 

$$
\widehat{\theta}(aX+b)=a\widehat{\theta}(X)+b
$$

for all $a>0$ and $b\in\mathbb{R}$. We say the loss function $L$ is location-scale invariant if

$$
L(a\widehat{\theta}+b,a\theta+b,a\tau)=L(\widehat{\theta},\theta,\tau).
$$

Similar to location invariance, we have $L(\widehat{\theta},\theta,\tau)=L(\widehat{\theta}-\theta,0,\tau)=L(\frac{\widehat{\theta}-\theta}{\tau},0,1)=:\rho(\frac{\widehat{\theta}-\theta}{\tau})$, so the loss function can be written as a function of $\frac{\widehat{\theta}-\theta}{\tau}.$ Also, the risk of a location-scale equivariant estimator is constant, since

$$
\mathbb{E}_{\theta,\tau}\rho\left(\frac{\widehat{\theta}(X)-\theta}{\tau}\right)=\mathbb{E}_{\theta,\tau}\rho\left(\widehat{\theta}\left(\frac{X-\theta}{\tau}\right)\right)=\mathbb{E}_{0,1}\rho\left(\widehat{\theta}\left(X\right)\right).
$$

How do we find a minimal risk location-scale eqivariant estimator $\delta(X)$? Again, we start with pilot estimators, but this time we need two. Suppose that $\delta_{0}(X)$ and $\delta_{1}(X)$ are pilot estimators satisfying

$$
\delta_{0}(aX+b)=a\delta_{0}(X)+b,\quad \delta_{1}(aX+b)=a\delta_{1}(X).
$$

Then letting $u(X):=\frac{\delta(X)-\delta_{0}(X)}{\delta_{1}(X)}$, we have

$$
\begin{aligned}
u(aX+b)	&= \frac{\delta(aX+b)-\delta_{0}(aX+b)}{\delta_{1}(aX+b)} \\
	&= \frac{a\delta(X)+b-a\delta_{0}(X)-b}{a\delta_{1}(X)} \\
	&= \frac{\delta(X)-\delta_{0}(X)}{\delta_{1}(X)}.
\end{aligned}
$$

Therefore, $u(aX+b)=u(X)$, and we have

$$
\begin{aligned}
u(X_{1},\ldots,X_{n}) &= u(X_{1}-X_{n},\ldots,X_{n-1}-X_{n},0) \\
	&=u\left(\frac{X_{1}-X_{n}}{|X_{n-1}-X_{n}|},\ldots,\frac{X_{n-1}-X_{n}}{|X_{n-1}-X_{n}|},0\right).
\end{aligned}
$$
Let $Z=\left(\frac{X_{1}-X_{n}}{|X_{n-1}-X_{n}|},\ldots,\frac{X_{n-1}-X_{n}}{|X_{n-1}-X_{n}|}\right)^{T}$ and write $u(X)=w(Z)$. Note that $Z$ is ancillary of $(\theta,\tau).$ We have 

$$
\delta(X)=\delta_{0}(X)-w(Z)\delta_{1}(X).
$$

The risk is

$$
\begin{aligned}
\mathbb{E}_{0,1}\rho(\delta(X))	&= \mathbb{E}_{0,1}\rho(\delta_{0}(X)-w(Z)\delta_{1}(X)) \\
	&=\mathbb{E}_{0,1}\left[\mathbb{E}_{0,1}(\rho(\delta_{0}(X)-w(Z)\delta_{1}(X))|Z)\right],
\end{aligned}
$$

so to minimize the risk we need to take

$$
w(Z)=\argmin_{a}\mathbb{E}_{0,1}\left(\rho(\delta_{0}(X))-a\delta_{1}(X)|Z\right).
$$

If $\rho(t)=t^{2}$, then

$$
\begin{aligned}
w(Z) &= \argmin_{a}\mathbb{E}_{0,1}\left[\left(\delta_{0}(X)-a\delta_{1}(X)\right)^{2}|Z\right] \\
	&=\argmin_{a}\left[a^{2}\mathbb{E}_{0,1}(\delta_{1}(X)^{2}|Z)-2a\mathbb{E}_{0,1}(\delta_{0}(X)\delta_{1}(X)|Z)\right] \\
	&=\frac{\mathbb{E}_{0,1}(\delta_{0}(X)\delta_{1}(X)|Z)}{\mathbb{E}_{0,1}(\delta_{1}(X)^{2}|Z)}.
\end{aligned}
$$

Therefore, 

$$
\delta(X)=\delta_{0}(X)-\delta_{1}(X)\frac{\mathbb{E}_{0,1}(\delta_{0}(X)\delta_{1}(X)|Z)}{\mathbb{E}_{0,1}(\delta_{1}(X)^{2}|Z)}.
$$

<details open>
<summary>Example</summary>

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}E(\theta,b).$ Recall that $P_{\theta,b}(x)=\frac{1}{b}e^{-(x-\theta)/b}1_{\\{x\geq\theta\\}}.$ Then $(\delta_{0}(X),\delta_{1}(X))=(X_{(1)},\sum_{i=1}^{n}(X_{i}-X_{(1)}))$ is complete and sufficient for $(\theta,b)$. By Basu's theorem, $(\delta_{0}(X),\delta_{1}(X))$ is independent of $Z$. Also, Basu's theorem implies that $X_{(1)}$ and $\sum_{i=1}^{n}(X_{i}-X_{(1)})$ are independent because $X_{(1)}$ is complete and sufficient for $\theta$  but $\sum_{i=1}^{n}(X_{i}-X_{(1)})$ is ancillary for $\theta.$ Therefore, 

$$
\frac{\mathbb{E}_{0,1}(\delta_{0}(X)\delta_{1}(X)|Z)}{\mathbb{E}_{0,1}(\delta_{1}(X)^{2}|Z)}=\frac{\mathbb{E}_{0,1}(\delta_{0}(X))\mathbb{E}(\delta_{1}(X))}{\mathbb{E}_{0,1}(\delta_{1}(X)^{2})}.
$$

Recall from a previous example that $\mathbb{E}(X_{(1)})=\frac{1}{n}$. The first moments of $\delta_{0}(X)$ and $\delta_{1}(X)$ can be easily derived. For the second moment of $\delta_{1}(X)$, we will derive the full distribution of $\delta_{1}(X)$. We have

$$
\begin{aligned}
f_{X_{(1)},\ldots,X_{(n)}}(x_{1},\ldots,x_{n}) &= n!f_{X_{1},\ldots,X_{n}}(x_{1},\ldots,x_{n})1_{\{0\leq x_{1}\leq x_{2}\leq\cdots\leq x_{n}\}} \\
	&=n!e^{-\sum_{i=1}^{n}x_{i}}1_{\{0\leq x_{1}\leq x_{2}\leq\cdots\leq x_{n}\}}.
\end{aligned}
$$

Let us now make the change of variable $Y_{1}=nX_{(1)}$, $Y_{2}=(n-1)(X_{(2)}-X_{(1)})$, $Y_{3}=(n-2)(X_{(3)}-X_{(2)}),\ldots,Y_{n}=X_{(n)}-X_{(n-1)}.$ Then

$$
\left|\frac{\partial Y}{\partial X_{(1,\ldots,n)}}\right|=n!
$$

so we have

$$
\begin{aligned}
f_{Y_{1},\ldots,Y_{n}}(y_{1},\ldots,y_{n}) &= f_{X_{(1)},\ldots,X_{(n)}}(x_{1},\ldots,x_{n})\left|\frac{\partial X}{\partial Y}\right| \\ &=e^{-\sum_{i=1}^{n}x_{i}}1_{\{0\leq x_{1}\leq x_{2}\leq\cdots\leq x_{n}\}}.
\end{aligned}
$$

Since $\sum_{i=1}^{n}X_{i}=\sum_{i=1}^{n}Y_{i}$, it follows that

$$
f_{Y_{1},\ldots,Y_{n}}(y_{1},\ldots,y_{n})=e^{-\sum_{i=1}^{n}y_{i}}1_{\{y_{1}\geq0,\ldots,y_{n}\geq0\}}=\prod_{i=1}^{n}e^{-y_{i}}1_{\{y_{i}\geq0\}}.
$$

This shows that $Y_{1},\ldots,Y_{n}\overset{\text{i.i.d.}}{\sim}E(0,1)$. Then 

$$
\delta_{1}(X)=\sum_{i=1}^{n}(X_{i}-X_{(1)})=\sum_{i=1}^{n}X_{i}-nX_{(1)}=\sum_{i=2}^{n}Y_{i}.
$$

Therefore, $\mathbb{E} _ {0,1}(\delta_{1}(X))=n-1$ and 

$$
\begin{aligned}
\mathbb{E}_{0,1}(\delta _ {1}(X)^{2}) &=\operatorname{Var}_{0,1}(\delta_{1}(X))+(\mathbb{E}_{0,1}\delta_{1}(X))^{2} \\
	&=n-1+(n-1)^{2} \\
	&=n(n-1).
\end{aligned}
$$

It follows that

$$
\frac{\mathbb{E}_{0,1}(\delta_{0}(X))\mathbb{E}(\delta_{1}(X))}{\mathbb{E}_{0,1}(\delta_{1}(X)^{2})}=\frac{\frac{1}{n}(n-1)}{n(n-1)}=\frac{1}{n^{2}},
$$

and we have the MREE

$$
\delta(X)=X_{(1)}-\frac{1}{n^{2}}\sum_{i=1}^{n}(X_{i}-X_{(1)}).
$$
</details>




Sometimes, it is possible to get minimal risk location-scale equivariant estimators from a minimal risk location equivariant estimator. The following should be obvious.

<details open>
<summary>Lemma</summary>

Suppose that $\delta(X)$ is the minimal risk location equivariant estimator for $\theta$ when $\tau$ is known, $\delta(X)$ does not depend on $\tau$, and $\delta(X)$ is also location-scale equivariant. Then $\delta(X)$ is the minimal risk location-scale equivariant estimator for $\theta$ when $\tau$ is unknown. 
</details>


<details open>
<summary>Example</summary>

Suppose that $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\theta,\sigma^{2})$. Then $\delta(X)=\overline{X}$ is the minimal risk location equivariant estimator for $\theta$ when $\sigma^{2}$ is known, $\delta(X)$ does not depend on $\sigma^{2}$, and $\delta(X)$ is location-scale equivariant, so $\overline{X}$ is also the minimal risk location-scale equivariant estimator for $\theta$ when $\sigma^{2}$ is unknown. 
</details>
