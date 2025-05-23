# Empirical risk minimization with a finite dictionary

We consider again empirical risk minimization. Given a dictionary $\mathcal{H},$ recall that 

$$
 \widehat{h}_{n}^{\text{erm}} \in \argmin_{h\in\mathcal{H}}R_{n}(h).
$$

Under some general assumptions on $\mathcal{H}$ (of which finiteness is a special case), it cam be shown the classifier $\widehat{h}_{n}^{\text{erm}}$ satisfies an inequality of the form

$$
\mathbb{E}[R(\widehat{h}_{n}^{\text{erm}})]\leq\inf_{h\in\mathcal{H}}R(h)+\Delta_{n}(\mathcal{H})
$$

where $\Delta_{n}(\mathcal{H})$ tends to 0 as $n\to\infty.$ An inequality of this form is called an oracle inequality. Here, $\Delta_{n}(\mathcal{H})$ term controls the stochastic error. Sometimes, we may also want oracle inequalities of the form

$$
R(\widehat{h}_{n}^{\text{erm}})\leq\inf_{h\in\mathcal{H}}R(h)+\Delta_{n}(\mathcal{H},\delta)
$$

which occur with probability at least $1-\delta .$ The key to showing oracle inequalities is the following lemma.

<details open>
<summary>Lemma</summary>

Let $\mathcal{H}$ be a set of classifiers. The stochastic error of $\widehat{h}_{n}^{\operatorname{erm}}$ satisfies 

$$
R(\widehat{h}_{n}^{\operatorname{erm}})-\inf_{h\in\mathcal{H}}R(h)\leq2\sup_{h\in\mathcal{H}}|R_{n}(h)-R(h)|.
$$
</details>


<details>
<summary>Proof</summary>

Let $\epsilon>0$ and let $h_{\epsilon}\in\mathcal{H}$ be a classifier such that $R(h_{\epsilon})\leq\inf_{h\in\mathcal{H}}R(h)+\epsilon .$ Since $\widehat{h}_{n}^{\text{erm}}$ minimizes the empirical risk, we have

$$
\begin{aligned}
R(\widehat{h}_{n}^{\text{erm}})-\inf_{h}R(h)	&=R(\widehat{h}_{n}^{\text{erm}})-R_{n}(\widehat{h}_{n}^{\text{erm}})+R_{n}(\widehat{h}_{n}^{\text{erm}})-\inf_{h\in\mathcal{H}}R(h) \\
	&\leq R(\widehat{h}_{n}^{\text{erm}})-R_{n}(\widehat{h}_{n}^{\text{erm}})+R_{n}(h_{\epsilon})-\inf_{h\in\mathcal{H}}R(h) \\
	&\leq R(\widehat{h}_{n}^{\text{erm}})-R_{n}(\widehat{h}_{n}^{\text{erm}})+R_{n}(h_{\epsilon})-R(h_{\epsilon})+\epsilon \\
	&\leq2\sup_{h\in\mathcal{H}}|R_{n}(h)-R(h)|+\epsilon.
\end{aligned}
$$

Since $\epsilon>0$ can be chosen arbitrarily, the lemma follows. 

</details>

Thus, to show any oracle inequalities, it suffices to have an upper bound (either in expectation or in probability) on $\sup_{h\in\mathcal{H}}|R_{n}(h)-R(h)|.$ Consider now the simple case where $\mathcal{H}$ is a finite dictionary. The following theorem gives oracle inequalities with high probability and in expectation. 

<details open>
<summary>Theorem</summary>

Let $\mathcal{H}=\{h_{1},\ldots,h_{M}\}$ be a finite dictionary. Then for any $\delta\in(0,1),$ with probability at least $1-\delta ,$ the classifier $\widehat{h}_{n}^{\operatorname{erm}}$ satisfies

$$
R(\widehat{h}_{n}^{\operatorname{erm}})\leq\min_{j=1,\ldots,M}R(h_{j})+\sqrt{\frac{2}{n}\log\left(\frac{2M}{\delta}\right)}.
$$

Moreover, 

$$
\mathbb{E}[R(\widehat{h}_{n}^{\operatorname{erm}})]\leq\min_{j=1,\ldots,M}R(h_{j})+2\sqrt{\frac{\log(2M)}{2n}}.
$$
</details>

<details>
<summary>Proof</summary>

Let $\delta\in(0,1)$ be fixed. From the lemma above, we have

$$
\mathbb{P}\left[R(\widehat{h}_{n}^{\operatorname{erm}})>R(h_{\mathcal{H}})+t\right]	\leq\mathbb{P}\left[\max_{j=1,\ldots,M}|R_{n}(h_{j})-R(h_{j})|>\frac{t}{2}\right].
$$

Using the fact that a Bernoulli random variable is $\frac{1}{4}$-sub-Gaussian, we note that $R_{n}(h_{j})$ is $\frac{1}{4n}$-sub-Gaussian, so a sub-Gaussian maximal inequality gives

$$
\mathbb{P}\left[\max_{j=1,\ldots,M}|R_{n}(h_{j})-R(h_{j})|>\frac{t}{2}\right]\leq2Me^{-\frac{nt^{2}}{2}}.
$$

Choosing $t=\sqrt{\frac{2}{n}\log\left(\frac{2M}{\delta}\right)}$ yields the desired high probability bound. For the second bound, another application of a sub-Gaussian maximal inequality gives

$$
\mathbb{E}[R(\widehat{h}_{n}^{\operatorname{erm}})]-\min_{j=1,\ldots,M}R(h_{j})	\leq2\mathbb{E}\left[\max_{j=1,\ldots,M}|R_{n}(h_{j})-R(h_{j})|\right]\leq2\sqrt{\frac{\log(2M)}{2n}}.
$$
</details>

