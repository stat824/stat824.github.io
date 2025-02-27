---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Minimal Sufficiency and Completeness'
weight: 3
---

We say that a statistic $S$ is minimal sufficient if it is sufficient and for every sufficient $T$, there is a measurable function $f$ such that $S=f(T)$. 

## Sub-family method
How do we find minimal sufficient statistic? The first method is called the sub-family method. 

{{% details title="Lemma" %}}
Suppose that $\Theta_{0}\subseteq\Theta$ and $S$ is minimal sufficient for $(P_{\theta}:\theta\in\Theta_{0})$ and sufficient for $(P_{\theta}:\theta\in\Theta)$. Then $S$ is minimal sufficient for $(P_{\theta}:\theta\in\Theta)$. 
{{% /details %}}

{{% details title="Proof" closed="true" %}}
Suppose that $T$ is sufficient for $(P_{\theta}:\theta\in\Theta)$. Then $T$ is sufficient for $(P_{\theta}:\theta\in\Theta_{0})$, so since $S$ is minimal sufficient for $(P_{\theta}:\theta\in\Theta_{0})$, it follows that $S$ is a function of $T$. 
{{% /details %}}

{{% details title="Theorem" %}}
For a discrete or continuous statistical model $(P_{\theta}:\theta\in\{\theta_{0},\ldots,\theta_{d}\})$ with finite parameter space and common support, 

$$
T(X)=\left(\frac{p(X|\theta_{1})}{p(X|\theta_{0})},\frac{p(X|\theta_{2})}{p(X|\theta_{0})},\ldots,\frac{p(X|\theta_{d})}{p(X|\theta_{0})}\right)
$$

is a minimal sufficient statistic. 
{{% /details %}}

{{% details title="Proof" closed="true" %}}
For $j=1,\ldots,d$, we have $p(x|\theta_{j})=T_{j}(x)p(x|\theta_{0})$, so if we define

$$
g_{\theta_{j}}(T(x))=\begin{cases}
1 & \text{if }j=0,\\
T_{j}(x) & \text{if }j=1,\ldots,d,
\end{cases}\quad\text{and}\quad h(x)=p(x|\theta_{0}),
$$

we see that $T$ is sufficient by the factorization theorem. For any sufficient $T'$, the factorization theorem implies the likelihood ratio is a function of $T'$, so $T$ is a function of $T'$. 
{{% /details %}}

{{< callout >}}

Let $X_{1},\ldots,X_{n}\overset{\text{iid}}{\sim}P_{\theta}$ where $P_{\theta}=\text{Ber}(\theta)$ and $\theta\in[0,1]$. Consider $\theta_{0}=0.5$ and $\theta_{1}=0.6$. Then

$$
\frac{p(X|\theta_{1})}{p(X|\theta_{0})}=\frac{\theta_{1}^{\sum_{i=1}^{n}X_{i}}(1-\theta_{1})^{n-\sum_{i=1}^{n}X_{i}}}{\theta_{0}^{\sum_{i=1}^{n}X_{i}}(1-\theta_{0})^{n-\sum_{i=1}^{n}X_{i}}}=\left(\frac{\theta_{1}(1-\theta_{0})}{\theta_{0}(1-\theta_{1})}\right)^{\sum_{i=1}^{n}X_{i}}\left(\frac{1-\theta_{1}}{1-\theta_{0}}\right)^{n}=\left(\frac{3}{2}\right)^{\sum_{i=1}^{n}X_{i}}\left(\frac{4}{5}\right)^{n}.
$$

This statistic is equivalent to $T(X)=\sum_{i=1}^{n}X_{i}$, so by the previous theorem we see that $T(X)$ is minimal sufficient for the sub-family $(P_{\theta}:\theta\in\{0.5,0.6\})$. We have seen before that $T(X)$ is sufficient for $(P_{\theta}:\theta\in[0,1])$, so the sub-family lemma yields that $T(X)$ is minimal sufficient for $(P_{\theta}:\theta\in[0,1])$.

{{< /callout >}}


As an application of the sub-family lemma, we can prove the following fact about minimal exponential families.
{{% details title="Theorem" %}}
If $(P_{\theta}:\theta\in H)$ is a minimal exponential family in canonical form 

$$
p(x|\eta)=\exp\left(\langle\eta,T(x)\rangle-A(\eta)\right)h(x),
$$

then $T(X)$ is minimal sufficient. 
{{% /details %}}

{{% details title="Proof" closed="true" %}}

Since the exponential family is minimal, we can find $\eta_{0},\ldots,\eta_{d}\in H$ such that

$$
\left(\begin{array}{c}
(\eta_{1}-\eta_{0})^{T}\\
(\eta_{2}-\eta_{1})^{T}\\
\vdots\\
(\eta_{d}-\eta_{0})^{T}
\end{array}\right)\in\mathbb{R}^{d\times d}
$$

has full rank. To see this, note that if the exponential family is full rank, then $H$ is an open rectangle, so it immediately follows. If the exponential family is curved, then this follows from the non-zero curvature of the function which relates the components of $\eta$. Then we know that

$$
\left(\frac{p(X|\eta_{1})}{p(X|\eta_{0})},\ldots,\frac{p(X|\eta_{d})}{p(X|\eta_{0})}\right)
$$

is minimal sufficient for $(P_{\eta}:\eta\in\{\eta_{1},\ldots,\eta_{d}\})$. Note that

$$
\frac{p(X|\eta_{j})}{p(X|\eta_{0})}=\frac{\exp\left(\langle\eta_{j},T(X)\rangle-A(\eta_{j})\right)}{\exp\left(\langle\eta_{0},T(X)\rangle-A(\eta_{0})\right)}=\exp\left(\left\langle \eta_{j}-\eta_{0},T(X)\right\rangle -A(\eta_{j})+A(\eta_{0})\right),
$$

which is equivalent to

$$
\left(\begin{array}{c}
\left\langle \eta_{1}-\eta_{0},T(x)\right\rangle \\
\left\langle \eta_{2}-\eta_{0},T(x)\right\rangle \\
\vdots\\
\left\langle \eta_{d}-\eta_{0},T(x)\right\rangle 
\end{array}\right)=\left(\begin{array}{c}
(\eta_{1}-\eta_{0})^{T}\\
(\eta_{2}-\eta_{0})^{T}\\
\vdots\\
(\eta_{d}-\eta_{0})^{T}
\end{array}\right)T(X),
$$

which is equivalent to $T(X)$. Since $T(X)$ is sufficient for the whole family $(P_{\eta}:\eta\in H)$, it follows from the sub-family lemma that $T(X)$ is minimal sufficient. 
{{% /details %}}


One of the restrictions of the sub-family method is that the support of all the distributions in the family must have the same support. This is not an issue for exponential families as the support depends only on the base measure $h(x)$, but it could be an issue for other distributions like $P_{\theta}=\text{Unif}(0,\theta)$. 

## Completeness

The second method of finding minimal sufficient statistics is called completeness. The idea is to remove ancillary information. For example, if $X_{1}$ and $X_{2}$ are iid $N(\theta,1)$, then we know that $(X_{1},X_{2})$ is not a minimal sufficient statistic because it is equivalent to $(X_{1}-X_{2},X_{1}+X_{2})$, and we know from before that $X_{1}+X_{2}$ is minimal sufficient. To be formal, we say that a statistic $A = A(X)$ is ancillary if its distribution does not depend on $\theta$, and we say it is first-order ancillary if $\mathbb{E} _ \theta A(X)$ does not depend on $\theta$. We also say a statistic $T=T(X)$ is complete if $\mathbb{E}_{\theta}f(T)=0$ for all $\theta\in\Theta$ implies $f(T(X))=0$ almost surely for all $\theta\in\Theta$. Equivalently, no non-constant function of $T$ is first-order ancillary. 

{{% details title="Bahadur's Theorem" %}}
If $T$ is sufficient and complete, then it is minimal sufficient.
{{% /details %}}

{{% details title="Sketch of Proof" closed="true" %}}
Assume that a minimal sufficient statistic $U$ exists. By definition, we have $U=h(T)$ for some measurable function $h$. We want to show that $T$ is also a function of $U$. Define $g(u)=\mathbb{E} _ \theta[T|U=u]$. Note that $g$ does not depend on $\theta$  because $U$ is sufficient. Then $\mathbb{E} _ \theta g(h(T))=\mathbb{E} _ \theta g(U)=\mathbb{E} _ {\theta}\left[\mathbb{E} _ \theta \left[T|U\right]\right]=\mathbb{E} _ \theta T$, so $\mathbb{E}_{\theta}\left[g(h(T))-T\right]=0$. By completeness of $T$, it follows that $g(U)=g(h(T))=T$ almost surely. 
{{% /details %}}

{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{iid}}{\sim}\text{Ber}(\theta)$ where $\theta\in(0,1)$. Let $T(X)=\sum_{i=1}^{n}X_{i}\sim\text{Binomial}(n,\theta)$. Suppose $\mathbb{E}_{\theta}f(T(X))=0$ for all $\theta\in(0,1)$. Then 

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
{{< /callout >}}

{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{iid}}{\sim}\text{Unif}(0,\theta)$ where $\theta>0$. Let $T(X)=X_{(n)}$. Suppose $\mathbb{E}_{\theta}f(T(X))=0$ for all $\theta>0$. Then 

$$
G(\theta)=\int_{0}^{\theta}t^{n-1}f(t)\,dt=0\quad\text{for all }\theta>0.
$$

By the Lebesgue differentiation theorem, $G'(\theta)=\theta^{n-1}f(\theta)$ almost everywhere. Since $G=0$, we have $G'=0$, so $f=0$ almost everywhere.
{{< /callout >}}

{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{iid}}{\sim}N(\theta,1)$ where $\theta\in\mathbb{R}$. Let $T(X)=\frac{1}{\sqrt{n}}\sum_{i=1}^{n}X_{i}\sim N(\theta,1)$. Suppose \mathbb{E} _ \thetaf(T(X))=0$ for all $\theta\in\mathbb{R}$. Then 

$$
G(\theta)=\int_{\mathbb{R}}f(x)e^{-\frac{1}{2}(x-\theta)^{2}}\,dx=0\quad\text{for all }\theta\in\mathbb{R}.
$$

By the Lebesgue differentiation theorem, we have $G'(\theta)=f(\theta)e^{-\frac{1}{2}(x-\theta)^{2}}$ almost everywhere. Since $G=0$, we have $G'=0$, which implies that $f=0$ almost everywhere. 
{{< /callout >}}

{{< callout >}}
For full rank minimal exponential family $(P_{\eta}:\eta\in H)$, $T$ is complete. 
{{< /callout >}}

{{% details title="Basu's Theorem" %}}
Let $T$ be complete and sufficient. If $A$ is ancillary, then $T \mathrel{\bot\mkern-10mu\bot} A$. 
{{% /details %}}

{{% details title="Proof" closed="true" %}}
Let $B$ be a measurable set. We want to show that $\mathbb{P} _ {\theta}(A\in B|T=t) = \mathbb{P} _ {\theta}(A\in B)$ for all $t$. Set $c=\mathbb{P} _ \theta (A\in B)$. This does not depend on $\theta$ since $A$ is ancillary. Also, set $g(t)=\mathbb{P} _ \theta (A\in B|T=t)$, which also does not depend on $\theta$ since $T$ is sufficient. Then 

$$
\mathbb{E}_{\theta}(g(T)-c)=\mathbb{E}_{\theta}\mathbb{P}_{\theta}(A\in B|T)-\mathbb{P}_{\theta}(A\in B)=0\quad\text{for all }\theta\in\Theta,
$$

so by completeness we have $g(T)=c$ almost surely. 
{{% /details %}}

{{< callout >}}
Let $X_{1},\ldots,X_{n}\overset{\text{iid}}{\sim}N(\theta,1)$. Then $\overline{X} \mathrel{\bot\mkern-10mu\bot} \sum_{i=1}^{n}(X_{i}-\overline{X})^{2}$ by Basu's theorem. 
{{< /callout >}}
