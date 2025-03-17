---
date: '2025-02-27T21:18:39+10:00'
draft: true
math: true
title: 'Hypothesis Testing and Le Cam's Method'
weight: 8
---

In a two-point test, we want to decide between the null hypothesis $H_{0}:X\sim P$ and the alternative hypothesis $H_{1}:X\sim Q$. The testing function is a function $\phi$ which maps the data $X$ to $\\{0,1\\}$. We define the Type-I error to be $P\phi:=\mathbb{E} _ {X\sim P}\phi(X)$ and the Type-II error to be $Q(1-\phi) := \mathbb{E} _ {X\sim Q}(1-\phi(X))$. The testing error is then $P\phi+Q(1-\phi)$, and the optimal testing error is $\inf_{\phi}(P\phi+Q(1-\phi))$. 


## Total variation distance

The total variation distance between two probability measures $P$ and $Q$ is

$$
\mathsf{TV}(P,Q)=\sup_{B}\left|P(B)-Q(B)\right|
$$

where the supremum is taken over all measurable sets $B$. 

{{% details title="Theorem" %}}
If $P$ and $Q$ are absolutely continuous with respect to the Lebesgue measure, we have

$$
\begin{aligned}
\mathsf{TV}(P,Q) & =P(\{p(x)>q(x)\})-Q(\{p(x)>q(x)\}) \\ &=\frac{1}{2}\int|p-q| \\ &=1-\int\min(p,q).
\end{aligned}
$$
{{% /details %}}

{{% details title="Proof" closed="true" %}}

Let $A=\\{p(x)>q(x)\\}$. Then $\mathsf{TV}(P,Q)\geq P(A)-Q(A)$ by definition. For all measurable sets $B$, we have

$$
\begin{aligned}
|P(B)-Q(B)| &= \left|\int_{B}(p-q)\right| \\
	&=\left|\int_{B\cap A}(p-q)+\int_{B\cap A^{c}}(p-q)\right| \\
	&=\left|\int_{B\cap A}(p-q)-\int_{B\cap A^{c}}(q-p)\right| \\
	&\leq\max\left(\int_{B\cap A}(p-q),\int_{B\cap A^{c}}(q-p)\right) \\
	&\leq\max\left(\int_{A}(p-q),\int_{A^{c}}(q-p)\right) \\
	&=\max\left(P(A)-Q(A),Q(A^{c})-P(A^{c})\right) \\
	&=P(A)-Q(A).
\end{aligned}
$$

This proves the first equality. For the second, we note that

$$
P(A)-Q(A)=\int_{\{p>q\}}(p-q)=\int_{\{p>q\}}|p-q|,
$$

$$
Q(A^{c})-P(A^{c})=\int_{\{p\leq q\}}(q-p)=\int_{\{p\leq q\}}|p-q|,
$$

so from $P(A)-Q(A)=Q(A^{c})-P(A^{c})$ it follows that 

$$
2(P(A)-Q(A))=\int_{\{p>q\}}|p-q|+\int_{\{p\leq q\}}|p-q|=\int|p-q|
$$

which implies the second equality. For the third equality, we note that

$$
\begin{aligned}
2-2\int\min(p,q) &=\left(\int p-\int\min(p,q)\right)+\left(\int q-\int\min(p,q)\right) \\
	&=\left(\int p-\int_{A}q-\int_{A^{c}}p\right)+\left(\int q-\int_{A}q-\int_{A^{c}}p\right) \\
	&=\left(\int_{A}p-\int_{A}q\right)+\left(\int_{A^{c}}q-\int_{A^{c}}p\right) \\
	&=\int_{A}|p-q|+\int_{A^{c}}|p-q| \\
	&=\int|p-q|.
\end{aligned}
$$
{{% /details %}}


{{% details title="Neyman-Pearson Lemma" %}}


The optimal testing error is given by

$$
\inf_{\phi}(P\phi+Q(1-\phi))=1-\mathsf{TV}(P,Q)=\int\min(p,q)
$$

which is achieved by the likelihood ratio test $\phi(X)=\mathbb{{1}}_{\\{p(x)<q(x)\\}}(X)$. 

{{% /details %}}


{{% details title="Proof" closed="true" %}}

For all $\phi$, we have 

$$
P\phi+Q(1-\phi) = \int p\phi+q(1-\phi)\geq\int\min(p,q),
$$

which shows that the optimal testing error is bounded below by $1-\mathsf{TV}(P,Q)=\int\min(p,q)$. For the upper bound, we have

$$
\inf_{\phi} (P\phi+Q(1-\phi)) \leq P(\{ p < q \}) + Q(\{ p \geq q \})=1-\mathsf{TV}(P,Q).
$$

{{% /details %}}

## Le Cam's two point method

Le Cam's two point method gives us a way to lower bound the minimax risk. The idea is basically that

$$
\inf_{\hat{\theta}}\sup_{\theta\in\Theta}R(\hat{\theta},\theta)\geq\inf_{\hat{\theta}}\sup_{\theta\in\{\theta_{1},\theta_{2}\}}R(\hat{\theta},\theta).
$$

{{% details title="Le Cam's Method" %}}
If we consider the squared loss function, then

$$
\inf_{\hat{\theta}}\sup_{\theta\in\{\theta_{1},\theta_{2}\}}\mathbb{E}_{\theta}(\hat{\theta}-\theta)^{2}\geq\frac{(\theta_{1}-\theta_{2})^{2}}{4}\int\min(p_{\theta_{1}},p_{\theta_{2}}).
$$
{{% /details %}}

{{% details title="Proof" closed="true" %}}
We have

$$
\begin{aligned}
\inf_{\hat{\theta}}\sup_{\theta\in\{\theta_{1},\theta_{2}\}}\mathbb{E}_{\theta}(\hat{\theta}-\theta)^{2} &\geq\inf_{\hat{\theta}}\left(\frac{1}{2}\mathbb{E}_{\theta_{1}}(\hat{\theta}-\theta_{1})^{2}+\frac{1}{2}\mathbb{E}_{\theta_{2}}(\hat{\theta}-\theta_{2})^{2}\right) \\
	&=\frac{1}{2}\inf_{\hat{\theta}}\int\left[(\hat{\theta}-\theta_{1})^{2}p_{\theta_{1}}+(\hat{\theta}-\theta_{2})^{2}p_{\theta_{2}}\right] \\
	&\geq\frac{1}{2}\inf_{\hat{\theta}}\int\left[(\hat{\theta}-\theta_{1})^{2}+(\hat{\theta}-\theta_{2})^{2}\right]\min(p_{\theta_{1}},p_{\theta_{2}}) \\
	&\geq\frac{1}{2}\inf_{\hat{\theta}}\int\frac{1}{2}(\theta_{1}-\theta_{2})^{2}\min(p_{\theta_{1}},p_{\theta_{2}}) \\
	&=\frac{1}{4}(\theta_{1}-\theta_{2})^{2}\int\min(p_{\theta_{1}},p_{\theta_{2}}).
\end{aligned}
$$
{{% /details %}}

To get the sharpest lower bound, we should choose $\theta_{1}$ and $\theta_{2}$ to be as far away as possible. 

{{< callout >}}

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\theta,1)$ where $\theta\in\mathbb{R}$. Let $\theta_{1}=0$ and $\theta_{2}=\frac{1}{\sqrt{n}}$. Then by Le Cam's two point method and the Neyman-Pearson lemma, we have

$$
\begin{aligned}
\inf_{\hat{\theta}}\sup_{\theta\in\{\theta_{1},\theta_{2}\}}\mathbb{E}_{\theta}(\hat{\theta}-\theta)^{2} &\geq\frac{1}{4n}\inf_{\phi}\left(P_{0}^{n}\phi+P_{\frac{1}{\sqrt{n}}}^{n}(1-\phi)\right) \\
	&\geq\frac{1}{4n}P_{0}^{n}( \{ p_{0}^{n} < p_{\frac{1}{\sqrt{n}}}^{n}\}) \\
	&=\frac{1}{4n}P_{0}^{n}\left(\left\{ \prod_{i=1}^{n}\frac{e^{-\frac{1}{2}(X_{i}-\frac{1}{\sqrt{n}})^{2}}}{e^{-\frac{1}{2}X_{i}^{2}}}>1\right\} \right) \\
	&=\frac{1}{4n}P_{0}^{n}\left(\left\{ \sum_{i=1}^{n}\left[\left(X_{i}-\frac{1}{\sqrt{n}}\right)^{2}-X_{i}^{2}\right]<0\right\} \right) \\
	&=\frac{1}{4n}P_{0}^{n}\left(\left\{ \frac{1}{\sqrt{n}}\sum_{i=1}^{n}X_{i}>\frac{1}{2}\right\} \right) \\
	&=\frac{1}{4n}\mathbb{P}(N(0,1)>\frac{1}{2}),
\end{aligned}
$$

so we have the lower bound

$$
\inf_{\hat{\theta}}\sup_{\theta\in\mathbb{R}}\mathbb{E}_{\theta}(\hat{\theta}-\theta)^{2}\geq Cn^{-1}
$$

where $C=\frac{\mathbb{P}(N(0,1)>\frac{1}{2})}{4}$. 

{{< /callout >}}

{{< callout >}}

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Unif}(0,\theta)$ where $\theta\in [0,1]$. Let $\widehat{\theta}=X_{(n)}$. Then

$$
\mathbb{E}_{\theta}(\hat{\theta}-\theta)^{2} = \int_{0}^{\theta}(t-\theta)^{2}\theta^{-n}nt^{n-1}\,dt =\frac{2\theta^{2}}{(n+1)(n+2)},
$$

so 

$$
\sup_{\theta\in[0,1]}\mathbb{E}_{\theta}(\hat{\theta}-\theta)^{2}=\frac{2}{(n+1)(n+2)}=O(n^{-2}).
$$

This gives an upper bound on the minimax rate. For the lower bound, we can use Le Cam's method. Let $\theta_{1}=1$ and $\theta_{2}=1-\frac{1}{n}$. Then


$$
\begin{aligned}
\inf_{\hat{\theta}}\sup_{\theta\in\{\theta_{1},\theta_{2}\}}\mathbb{E}_{\theta}(\hat{\theta}-\theta)^{2} &\geq\frac{1}{4n^{2}}\int p_{1}^{n}\land p_{1-\frac{1}{n}}^{n} \\
	&\geq\frac{1}{8n^{2}}\left(\int\sqrt{p_{1}^{n}p_{1-\frac{1}{n}}^{n}}\right)^{2} \\
	&=\frac{1}{8n^{2}}\left(\int\sqrt{\prod_{i=1}^{n}p_{1}(x_{i})p_{1-\frac{1}{n}}(x_{i})}\right)^{2} \\
	&=\frac{1}{8n^{2}}\left(\int\sqrt{p_{1}(x_{1})p_{1-\frac{1}{n}}(x_{1})}\right)^{2n} \\
	&=\frac{1}{8n^{2}}\left(\int_{0}^{1-\frac{1}{n}}\sqrt{\frac{1}{1-\frac{1}{n}}}\right)^{2n} \\
	&=\frac{1}{8n^{2}}\left(1-\frac{1}{n}\right)^{n}.
\end{aligned}
$$

This gives

$$
\inf_{\hat{\theta}}\sup_{\theta\in\mathbb{R}}\mathbb{E}_{\theta}(\hat{\theta}-\theta)^{2}\asymp n^{-2}.
$$

{{< /callout >}}

## Minimax lower bound for Gaussian sequence model

Now we want to prove the minimax lower bound for the Gaussian sequence problem. Recall that we have observations $X_{j}\sim N(\theta_{j},\frac{1}{n})$, $j\in\mathbb{N}$, where $\theta\in\Theta_{\alpha}(R)=\\{\theta:\sum_{j=1}^{\infty}j^{2\alpha}\theta_{j}^{2}\leq R^{2}\\}$. We want to show that

$$
\inf_{\hat{\theta}}\sup_{\theta\in\Theta_{\alpha}(R)}\mathbb{E}_{\theta}\Vert\hat{\theta}-\theta\Vert^{2}\geq cn^{\frac{-2\alpha}{2\alpha+1}}.
$$

Let us define $\Theta_{0}=\\{\theta:\theta_{j}\in\\{0,\frac{1}{\sqrt{n}}\\}\text{ for }j=1,\ldots,k,\theta_{j}=0\text{ for }j>k\\}$. Then $|\Theta_{0}|=2^{k}$. To ensure that $\Theta_{0}\subseteq\Theta_{\alpha}(R)$, we note that

$$
\sum_{j=1}^{\infty}j^{2\alpha}\theta_{j}^{2}\leq\frac{1}{n}\sum_{j=1}^{k}j^{2\alpha}\leq\frac{k^{2\alpha+1}}{n}.
$$

Solving $\frac{k^{2\alpha+1}}{n}\leq R^{2}$ gives $k\asymp n^{\frac{1}{2\alpha+1}}$. Let us introduce the notation $\theta_{-j}$ to denote $(\theta_1, \ldots, \theta_{j-1}, \theta_{j+1}, \ldots, \theta_k)$. We also write $\operatornamewithlimits{ave}_{x\in S} f(x)$ to denote the average of $f(x)$ over $x \in S$ where $S$ is a finite set. Then

$$
\begin{aligned}
\inf_{\widehat{\theta}}\sup_{\theta\in\Theta_{\alpha}(R)}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2} &\geq\inf_{\widehat{\theta}}\sup_{\theta\in\Theta_{0}}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2} \\
	&\geq\inf_{\widehat{\theta}}\operatornamewithlimits{ave}_{\theta\in\Theta_{0}}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2} \\
	&\geq\inf_{\widehat{\theta}}\operatornamewithlimits{ave}_{\theta\in\Theta_{0}}\sum_{j=1}^{k}(\widehat{\theta}_{j}-\theta_{j})^{2} \\
	&=\inf_{\widehat{\theta}}\sum_{j=1}^{k}\operatornamewithlimits{ave}_{\theta\in\Theta_{0}}\mathbb{E}_{\theta}(\widehat{\theta}_{j}-\theta_{j})^{2} \\
	&=\inf_{\widehat{\theta}}\sum_{j=1}^{k}\operatornamewithlimits{ave}_{\theta_{-j}}\left[\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=0)}(\widehat{\theta}_{j})^{2}+\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=\frac{1}{\sqrt{n}})}(\widehat{\theta}_{j}-\frac{1}{\sqrt{n}})^{2}\right] \\
	&\geq\sum_{j=1}^{k}\operatornamewithlimits{ave}_{\theta_{-j}}\inf_{\widehat{\theta}_{j}}\left[\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=0)}(\widehat{\theta}_{j})^{2}+\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=\frac{1}{\sqrt{n}})}(\widehat{\theta}_{j}-\frac{1}{\sqrt{n}})^{2}\right].
\end{aligned}
$$

Using the same argument as in the proof of Le Cam's method to estimate the infimum, we have

$$
\inf_{\widehat{\theta}_{j}}\left[\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=0)}(\widehat{\theta}_{j})^{2}+\frac{1}{2}\mathbb{E}_{(\theta_{-j},\theta_{j}=\frac{1}{\sqrt{n}})}(\widehat{\theta}_{j}-\frac{1}{\sqrt{n}})^{2}\right] \geq \frac{1}{4n}\int p_{(\theta_{-j},\theta_{j}=0)}\land p_{(\theta_{-j},\theta_{j}=\frac{1}{\sqrt{n}})}.
$$

The integral represents the optimal test error for testing the hypotheses $H_0 : \theta_j = 0$ versus $H_1 : \theta_j = \frac{1}{\sqrt{n}}$. Since only the $\theta_{j}$ differs between the two hypotheses, this is equivalent to testing $H_{0}:X_{j}\sim N(0,\frac{1}{n})$ versus $H_{1}:X_{j}\sim N(\frac{1}{\sqrt{n}},\frac{1}{n})$. Therefore, letting $P=N(0,\frac{1}{n})$ and $Q=N(\frac{1}{\sqrt{n}},\frac{1}{n})$, we have

$$
\inf_{\widehat{\theta}}\sup_{\theta\in\Theta_{\alpha}(R)}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2}\geq \frac{1}{4n} \sum_{j=1}^{k} \inf_{\phi}(P\phi+Q(1-\phi)).
$$

From an example above, we know that the optimal testing error for this test satisfies 

$$
\inf_{\phi}(P\phi+Q(1-\phi))\geq 4c
$$

where $4c=\mathbb{P}(N(0,1)>\frac{1}{2})$. Therefore, 

$$
\inf_{\widehat{\theta}}\sup_{\theta\in\Theta_{\alpha}(R)}\mathbb{E}_{\theta}\Vert\widehat{\theta}-\theta\Vert^{2}\geq\frac{k}{n} \asymp n^{-\frac{2\alpha}{2\alpha+1}}.
$$