---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Equivariant Estimators'
weight: 10
---

## Location equivariance

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

{{% details title="Theorem" %}}
For a location model $(P_{\theta}:\theta\in\mathbb{R}^{p})$, a location invariant loss $L(\widehat{\theta},\theta)$, and a location equivariant estimator $\widehat{\theta}$, the risk $\mathbb{E}_{\theta}L(\widehat{\theta},\theta)$ must be constant. 
{{% /details %}}

{{% details title="Proof" closed="true" %}}
For all $\theta\in\mathbb{R}^{p}$, we have $\mathbb{E} _ {\theta}L(\widehat{\theta},\theta)=\mathbb{E} _ {\theta}\rho(\widehat{\theta}-\theta)=\mathbb{E} _ {\theta}\rho(\widehat{\theta}(X_{1},\ldots,X_{n})-\theta)=\mathbb{E} _ {\theta}\rho(\widehat{\theta}(X_{1}-\theta,\ldots,X_{n}-\theta))=\mathbb{E} _ {0}\rho(\widehat{\theta}(X_{1},\ldots,X_{n})).$ 
{{% /details %}}

A minimal risk equivariant estimator (MREE) is an equivariant estimator which has the lowest risk among all equivariant estimators. The strategy to finding the minimal risk location equivariant estimator is to start with a pilot estimator $\delta_{0}(X)$ which can be any location equivariant estimator. Then we set

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

{{< callout >}}
Suppose that $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\theta,1)$. Let $\delta_{0}(X)=\overline{X}$. Then $\mathbb{E} _ {0}(\overline{X}|Y) = \mathbb{E} _ {0}(\overline{X}) = 0$, so $\delta(X)=\overline{X}$ is MREE. 
{{< /callout >}}

{{< callout >}}
Suppose that $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}E(\theta,b)$ where $b$ is known. The density is given by $P_{\theta}(x)= b^{-1}e^{-\frac{(x-\theta)}{b}}1_{\\{x>\theta\\}}.$ Let $\delta_{0}(X)=X_{(1)}$. Then since $Y$ is ancillary, $\mathbb{E} _ {0}(X_{(1)}|Y) = \mathbb{E} _ {0}(X_{(1)})$. To evaluate this expectation, write $X_{i}=\theta+bZ_{i}$ where $Z_{i} \sim E(0,1)$. Then $X_{(1)}=\theta+bZ_{(1)}$. We have 

$$
\mathbb{P}(Z_{(1)}\leq t)=1-\mathbb{P}(Z_{(1)}>t)=1-\prod_{i=1}^{t}\mathbb{P}(Z_{i}>t)=1-e^{-nt}.
$$

The density of $Z_{(1)}$ is then $ne^{-nt}1_{\\{t>0\\}}$ which has mean $\frac{1}{n}$. Therefore, $\mathbb{E} _ {0}(X_{(1)}) = \frac{b}{n}$, which gives the MREE

$$
\delta(X)=X_{(1)} - \frac{b}{n}.
$$
{{< /callout >}}

The following should be obvious. 

{{% details title="Lemma" %}}
Suppose that $\rho(t)=t^{2}$. 

* If $\delta(X)$ is location equivariant, then its bias $b$ is constant and $\delta(X)-b$ has smaller risk. 

* The minimal risk equivariant estimator is unbiased. 

* If UMVUE exists and is location equivariant, then the MREE and UMVUE coincide. 
{{% /details %}}

### Pitman estimator

Suppose that $\rho(t)=t^{2}$ and we have the pilot estimator $\delta_{0}(X)=X_{n}$. Then $\delta(X) = X _ {n} - \mathbb{E} _ {0}(X_{n}|Y)$. Let 

$$
Z=\left(\begin{array}{c}
Y\\
X_{n}
\end{array}\right)=\left(\begin{array}{c}
X_{1}-X_{n}\\
\vdots\\
X_{n-1}-X_{n}\\
X_{n}
\end{array}\right).
$$

Then $X_{1}=Z_{1}+Z_{n},\ldots,X_{n-1}=Z_{n-1}+Z_{n}, X_{n}=Z_{n},$ so 

$$
\frac{\partial X}{\partial Z}=\left(\begin{array}{cc}
I_{n-1} & 1_{n-1}^{T}\\
0 & 1
\end{array}\right),
$$

and we have

$$
\begin{aligned}
P_{Z,0}(z_{1},\ldots,z_{n}) &=P_{X,0}(x_{1},\ldots,x_{n})\left|\frac{\partial X}{\partial Z}\right| \\
	&=P_{X,0}(x_{1},\ldots,x_{n}) \\
	&=\prod_{i=1}^{n}f(x_{i}) \\
	&=f(y_{1}+x_{n})\cdots f(y_{n-1}+x_{n})f(x_{n}).
\end{aligned}
$$

Then

$$
\mathbb{E}_{0}(X_{n}|Y)=\frac{\int tf(Y_{1}+t)\cdots f(Y_{n-1}+t)f(t)\,dt}{\int f(Y_{1}+t)\cdots f(Y_{n-1}+t)f(t)\,dt}.
$$

Using $\delta(X) = X _ {n} - \mathbb{E} _ {0}(X_{n}|Y)$, we have

$$
\begin{aligned}
\delta(X) &=\frac{\int(X_{n}-t)f(Y_{1}+t)\cdots f(Y_{n-1}+t)f(t)\,dt}{\int f(Y_{1}+t)\cdots f(Y_{n-1}+t)f(t)\,dt} \\
	&=\frac{\int uf(X_{1}-u)\cdots f(X_{n}-u)\,du}{\int f(X_{1}-u)\cdots f(X_{n}-u)\,du}.
\end{aligned}
$$

The formula

$$
\delta(X)=\frac{\int u\prod_{i=1}^{n}f(X_{i}-u)\,du}{\int\prod_{i=1}^{n}f(X_{i}-u)\,du}
$$

is called the Pitman estimator. 

{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Unif}(\theta-\frac{b}{2},\theta+\frac{b}{2})$. Then the density is $P_{\theta}(x)=b^{-1}1_{\{\theta-\frac{b}{2}<x<\theta+\frac{b}{2}\}}$. Then

$$
\begin{aligned}
\prod_{i=1}^{n} f(X_{i} - u) &= \prod_{i=1}^{n} b^{-1} 1_{\{u-\frac{b}{2} < X_{i} < u+\frac{b}{2}\}} \\
	&=b^{-n}1_{\{u-\frac{b}{2} < X_{(1)}\}}1_{\{X_{(n)} < u+\frac{b}{2}\}} \\
	&=b^{-n}1_{\{X_{(n)} - \frac{b}{2} < u < X_{(1)} + \frac{b}{2}\}}.
\end{aligned}
$$

Therefore, the MREE is

$$
\delta(X) = \frac{\int_{X_{(n)}-\frac{b}{2}}^{X_{(1)}+\frac{b}{2}}u\,du}{\int_{X_{(n)}-\frac{b}{2}}^{X_{(1)}+\frac{b}{2}}\,du}=\frac{1}{2}\frac{(X_{(1)}+\frac{b}{2})^{2}-(X_{(n)}-\frac{b}{2})^{2}}{(X_{(1)}+\frac{b}{2})-(X_{(n)}-\frac{b}{2})}=\frac{X_{(1)}+X_{(n)}}{2}.
$$
{{< /callout >}}

## Location-scale equivariance

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

How do we find a minimal risk location-scale eqivariant estimator $\delta(X)$? Again, we start with pilot estimators, but this time we need two. Suppose that $\delta_{0}(X)$ and \delta_{1}(X) are pilot estimators satisfying\delta_{0}(aX+b)	=a\delta_{0}(X)+b,
\delta_{1}(aX+b)	=a\delta_{1}(X).Then letting u(X):=\frac{\delta(X)-\delta_{0}(X)}{\delta_{1}(X)}, we haveu(aX+b)	=\frac{\delta(aX+b)-\delta_{0}(aX+b)}{\delta_{1}(aX+b)}
	=\frac{a\delta(X)+b-a\delta_{0}(X)-b}{a\delta_{1}(X)}
	=\frac{\delta(X)-\delta_{0}(X)}{\delta_{1}(X)}.Therefore, u(aX+b)=u(X), and we haveu(X_{1},\ldots,X_{n})	=u(X_{1}-X_{n},\ldots,X_{n-1}-X_{n},0)
	=u\left(\frac{X_{1}-X_{n}}{|X_{n-1}-X_{n}|},\ldots,\frac{X_{n-1}-X_{n}}{|X_{n-1}-X_{n}|},0\right).Let Z=\left(\frac{X_{1}-X_{n}}{|X_{n-1}-X_{n}|},\ldots,\frac{X_{n-1}-X_{n}}{|X_{n-1}-X_{n}|}\right)^{T} and write u(X)=w(Z). Note that Z is ancillary of (\theta,\tau). We have \delta(X)=\delta_{0}(X)-w(Z)\delta_{1}(X).The risk is\mathbb{E}_{0,1}\rho(\delta(X))	=\mathbb{E}_{0,1}\rho(\delta_{0}(X)-w(Z)\delta_{1}(X))
	=\mathbb{E}_{0,1}\left[\mathbb{E}_{0,1}(\rho(\delta_{0}(X)-w(Z)\delta_{1}(X))|Z)\right],so to minimize the risk we need to takew(Z)=\argmin_{a}\mathbb{E}_{0,1}\left(\rho(\delta_{0}(X))-a\delta_{1}(X)|Z\right).If \rho(t)=t^{2}, thenw(Z)	=\argmin_{a}\mathbb{E}_{0,1}\left[\left(\delta_{0}(X)-a\delta_{1}(X)\right)^{2}|Z\right]
	=\argmin_{a}\left[a^{2}\mathbb{E}_{0,1}(\delta_{1}(X)^{2}|Z)-2a\mathbb{E}_{0,1}(\delta_{0}(X)\delta_{1}(X)|Z)\right]
	=\frac{\mathbb{E}_{0,1}(\delta_{0}(X)\delta_{1}(X)|Z)}{\mathbb{E}_{0,1}(\delta_{1}(X)^{2}|Z)}.Therefore, \delta(X)=\delta_{0}(X)-\delta_{1}(X)\frac{\mathbb{E}_{0,1}(\delta_{0}(X)\delta_{1}(X)|Z)}{\mathbb{E}_{0,1}(\delta_{1}(X)^{2}|Z)}.

Example 6.6. Let X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}E(\theta,b). Recall that P_{\theta,b}(x)=\frac{1}{b}e^{-(x-\theta)/b}1_{\{x\geq\theta\}}. Then (\delta_{0}(X),\delta_{1}(X))=(X_{(1)},\sum_{i=1}^{n}(X_{i}-X_{(1)})) is complete and sufficient for (\theta,b). By Basu's theorem, (\delta_{0}(X),\delta_{1}(X)) is independent of Z. Also, Basu's theorem implies that X_{(1)} and \sum_{i=1}^{n}(X_{i}-X_{(1)}) are independent because X_{(1)} is complete and sufficient for \theta  but \sum_{i=1}^{n}(X_{i}-X_{(1)}) is ancillary for \theta . Therefore, \frac{\mathbb{E}_{0,1}(\delta_{0}(X)\delta_{1}(X)|Z)}{\mathbb{E}_{0,1}(\delta_{1}(X)^{2}|Z)}=\frac{\mathbb{E}_{0,1}(\delta_{0}(X))\mathbb{E}(\delta_{1}(X))}{\mathbb{E}_{0,1}(\delta_{1}(X)^{2})}.Recall from a previous example that \mathbb{E}(X_{(1)})=\frac{1}{n}. The first moments of \delta_{0}(X) and \delta_{1}(X) can be easily derived. For the second moment of \delta_{1}(X), we will derive the full distribution of \delta_{1}(X). We havef_{X_{(1)},\ldots,X_{(n)}}(x_{1},\ldots,x_{n})	=n!f_{X_{1},\ldots,X_{n}}(x_{1},\ldots,x_{n})1_{\{0\leq x_{1}\leq x_{2}\leq\cdots\leq x_{n}\}}
	=n!e^{-\sum_{i=1}^{n}x_{i}}1_{\{0\leq x_{1}\leq x_{2}\leq\cdots\leq x_{n}\}}.Let us now make the change of variable Y_{1}=nX_{(1)}, Y_{2}=(n-1)(X_{(2)}-X_{(1)}), Y_{3}=(n-2)(X_{(3)}-X_{(2)}),\ldots,Y_{n}=X_{(n)}-X_{(n-1)}. Then\left|\frac{\partial Y}{\partial X_{(1,\ldots,n)}}\right|=n!so we havef_{Y_{1},\ldots,Y_{n}}(y_{1},\ldots,y_{n})=f_{X_{(1)},\ldots,X_{(n)}}(x_{1},\ldots,x_{n})\left|\frac{\partial X}{\partial Y}\right|=e^{-\sum_{i=1}^{n}x_{i}}1_{\{0\leq x_{1}\leq x_{2}\leq\cdots\leq x_{n}\}}.Since \sum_{i=1}^{n}X_{i}=\sum_{i=1}^{n}Y_{i}, it follows thatf_{Y_{1},\ldots,Y_{n}}(y_{1},\ldots,y_{n})=e^{-\sum_{i=1}^{n}y_{i}}1_{\{y_{1}\geq0,\ldots,y_{n}\geq0\}}=\prod_{i=1}^{n}e^{-y_{i}}1_{\{y_{i}\geq0\}}.This shows that Y_{1},\ldots,Y_{n}\overset{\text{i.i.d.}}{\sim}E(0,1). Then \delta_{1}(X)=\sum_{i=1}^{n}(X_{i}-X_{(1)})=\sum_{i=1}^{n}X_{i}-nX_{(1)}=\sum_{i=2}^{n}Y_{i}.Therefore, \mathbb{E}_{0,1}(\delta_{1}(X))=n-1 and \mathbb{E}_{0,1}(\delta_{1}(X)^{2})	=\operatorname{Var}_{0,1}(\delta_{1}(X))+(\mathbb{E}_{0,1}\delta_{1}(X))^{2}
	=n-1+(n-1)^{2}
	=n(n-1).It follows that\frac{\mathbb{E}_{0,1}(\delta_{0}(X))\mathbb{E}(\delta_{1}(X))}{\mathbb{E}_{0,1}(\delta_{1}(X)^{2})}=\frac{\frac{1}{n}(n-1)}{n(n-1)}=\frac{1}{n^{2}},and we have the MREE\delta(X)=X_{(1)}-\frac{1}{n^{2}}\sum_{i=1}^{n}(X_{i}-X_{(1)}).



The following should be obvious. 

Lemma 6.7. If \delta(X) is the minimal risk location equivariant estimator for \theta  when \tau  is known, \delta(X) does not depend on \tau , and \delta(X) is also location-scale equivariant, then \delta(X) is the minimal risk location-scale equivariant estimator for \theta  when \tau  is unknown. 



Example 6.8. Suppose that X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\theta,\sigma^{2}). Then \delta(X)=\overline{X} is the minimal risk location equivariant estimator for \theta  when \sigma^{2} is known, \delta(X) does not depend on \sigma^{2}, and \delta(X) is location-scale equivariant, so \overline{X} is the minimal risk location-scale equivariant estimator for \theta  when \sigma^{2} is unknown. 