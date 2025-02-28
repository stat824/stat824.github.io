---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Exponential Families'
weight: 2
---
We say that a continuous or discrete statistical model $(P_{\theta}:\theta\in\Theta)$ is an exponential family if

$$
p(x|\theta)=\exp\left(\sum_{j=1}^{d}\eta_{j}(\theta)T_{j}(x)-B(\theta)\right)h(x)
$$

where $\eta(\theta)$ is called the natural parameter, $T(x)$ is the sufficient statistic, 

$$
B(\theta)=\log\int\exp\left(\sum_{j=1}^{d}\eta_{j}(\theta)T_{j}(x)\right)h(x)\,d\mu(x)
$$

is the log-partition function, and $h(x)$ is the base measure. In the formula for $B(\theta)$ above, $\mu$ is either the Lebesgue measure or the counting measure. Given observations $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}p(x|\theta)=e^{\sum_{j=1}^{d}\eta_{j}(\theta)T_{j}(x)-B(\theta)}h(x)$, we have

$$
p(x_{1},\ldots,x_{n}|\theta)=\exp\left(\sum_{j=1}^{d}\eta_{j}(\theta)\left(\sum_{i=1}^{n}T_{j}(x_{i})\right)-nB(\theta)\right)\prod_{i=1}^{n}h(x_{i}),
$$

from which we see that a sufficient statistic is $T'=\sum_{i=1}^{n}T(x_{I})$. We say that an exponential family is in canonical form if 

$$
p(x|y)=\exp\left(\sum_{j=1}^{d}\eta_{j}T_{j}(x)-A(\eta)\right)h(x).
$$

Any exponential family can be reparameterized into canonical form. Here, 

$$
A(\eta)=\log\int\exp\left(\sum_{j=1}^{d}\eta_{j}T_{j}(x)\right)h(x)\,d\mu(x).
$$

We say an exponential family $(P_{\eta}:\eta\in H)$ in canonical form is minimal if the dimension $d$ cannot be reduced. 

{{< callout >}}
The family $p(x|\theta)=\exp(\eta_{1}T(x)+\eta_{2}(3T(x)+2)-A(\eta))$ is non-minimal, since $\exp(\eta_{1}T(x)+\eta_{2}(3T(x)+2)-A(\eta))=\exp((\eta_{1}+3\eta_{2})T(x)+2\eta_{2}-A(\eta)).$ 

Similarly, the family $p(x|\theta)=\exp\left(\eta T_{1}(x)+(4-5\eta)T_{2}(x)-A(\eta)\right)$ is non-minimal, since $\exp\left(\eta T_{1}(x)+(4-5\eta)T_{2}(x)-A(\eta)\right)=\exp\left(\eta(T_{1}(x)-5T_{2}(x))-A(\eta)\right)\exp\left(4T_{2}(x)\right).$
{{< /callout >}}



Essentially, minimality fails if the components of the sufficient statistic or the natural parameters are not linearly independent. There are two types of minimal exponential family $(P_{\eta}:\eta\in H)$: 

1. full rank, where $H$ contains an open $d$-dimensional rectangle;

2. curved exponential family, where $\eta_{1},\ldots,\eta_{d}$ are related in a non-linear way. 


{{< callout >}}
For $N(\mu,\sigma^{2})$, we have

$$
p(x|\mu,\sigma^{2})=\exp\left(-\frac{x^{2}}{2\sigma^{2}}+\frac{\mu}{\sigma^{2}}x-\frac{\mu^{2}}{2\sigma^{2}}-\frac{1}{2}\log(2\pi\sigma^{2})\right),
$$

so $T_{1}(x)=-x^{2}$, $T_{2}(x)=x$, $\eta_{1}=\frac{1}{2\sigma^{2}}$, $\eta_{2}=\frac{\mu}{\sigma^{2}}$. Let's consider different special cases. 

1. If $\mu=\sigma^{2}$, then $\eta_{2}=1$, so this is a non-minimal exponential family. 

2. If $\mu=\sqrt{\sigma^{2}}$, then $\eta_{1}=\frac{1}{2\sigma^{2}}$ and $\eta_{2}=\frac{1}{\sqrt{\sigma^{2}}}$, so $\eta^{2}=2\eta_{1}$. This is a minimal curved exponential family. 

3. If $\mu$ and $\sigma^{2}$ do not have constraints, then this is a full rank minimal exponential family. 
{{< /callout >}}