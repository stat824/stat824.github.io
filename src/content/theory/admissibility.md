# Admissibility

An estimator $\hat{\theta}$ is inadmissible if there exists $\tilde{\theta}$ such that 

1. $R(\tilde{\theta},\theta) \leq R(\hat{\theta},\theta)$ for all $\theta\in\Theta$, and

2. $R(\tilde{\theta},\theta_{0}) < R(\hat{\theta},\theta_{0})$ for some $\theta_{0}\in\Theta$.

Then we say $\hat{\theta}$ is admissible if it is not inadmissible. To put it bluntly, inadmissible estimators are those that are essentially useless. There are always other choices that are strictly better. 


## Bayes estimators

<details open>
<summary>Theorem</summary>

Assume that the loss function is continuous. If $\hat{\theta}$ is Bayes, then it is admissible.
</details>

<details>
<summary>Proof</summary>

We will prove the contrapositive. Suppose that $\hat{\theta}$ is inadmissible. Then there exists $\tilde{\theta}$ such that 
$R(\tilde{\theta},\theta)\leq R(\hat{\theta},\theta)$ for all $\theta\in\Theta$, and $R(\tilde{\theta},\theta_0) < R(\hat{\theta},\theta_0)$ for some $\theta_0 \in \Theta$. By continuity, there exists an open set $\Theta_{0}\ni\theta_{0}$ and $\epsilon>0$ such that $R(\tilde{\theta},\theta)<R(\hat{\theta},\theta)-\epsilon$ for all $\theta\in\Theta_{0}$. Then

$$
\begin{aligned}
\int_{\Theta}R(\tilde{\theta},\theta)\pi(\theta)\,d\theta &= \int_{\Theta_{0}}R(\tilde{\theta},\theta)\pi(\theta)\,d\theta+\int_{\Theta\backslash\Theta_{0}}R(\tilde{\theta},\theta)\pi(\theta)\,d\theta \\
	&<\int_{\Theta_{0}}R(\hat{\theta},\theta)\pi(\theta)\,d\theta+\int_{\Theta\backslash\Theta_{0}}R(\hat{\theta},\theta)\pi(\theta)\,d\theta \\ 
	&=\int_{\Theta}R(\hat{\theta},\theta)\pi(\theta)\,d\theta,
\end{aligned}
$$

so $\hat{\theta}$ cannot be Bayes. 
</details>


Is the converse true? That is, is it true that an admissible estimator must be Bayes? This is answered by the complete class theorem, which roughly states that if $\hat{\theta}$ is admissible, then there exists a sequence of priors $(\pi_{m})$ such that $\hat{\theta} _ {\pi_{m}}\to\hat{\theta}$. 

## Admissibility of the sample mean for normal mean estimation

<details open>
<summary>Theorem</summary>

Let $X_{1},\ldots,X_{n}\overset{\mathrm{i.i.d.}}{\sim}N(\theta,1), \theta\in\mathbb{R}$. Consider the loss function $L(\hat{\theta},\theta)=(\hat{\theta}-\theta)^{2}$. Then $\overline{X}$ is admissible.
</details>

<details>
<summary>Proof</summary>

The proof is by contradiction. Suppose that $\hat{\theta}=\overline{X}$ is inadmissible, so that there exists $\tilde{\theta}$ such that $R(\tilde{\theta},\theta)\leq\frac{1}{n}$ for all $\theta\in\mathbb{R}$, and $R(\tilde{\theta},\theta_{0})<\frac{1}{n}$ for some $\theta_{0}\in\mathbb{R}$. Then there exists $\epsilon>0$ and $(a,b)\ni\theta_{0}$ such that $R(\tilde{\theta},\theta_{0})<\frac{1}{n}-\epsilon$. Consider $\pi_{m}=N(0,m)$. Then the Bayes risk is

$$
\int_{\mathbb{R}}R(\hat{\theta}_{\pi_{m}},\theta)\pi_{m}(\theta)\,d\theta=\frac{1}{n+\frac{1}{m}},
$$

and we have

$$
\frac{1}{n}-\int_{\mathbb{R}}R(\hat{\theta}_{\pi_{m}},\theta)\pi_{m}(\theta)\,d\theta=\frac{1}{n}\cdot\frac{\frac{1}{m}}{n+\frac{1}{m}}\asymp\frac{1}{m}.
$$

Then

$$
\begin{aligned}
\frac{1}{n}-\int_{\mathbb{R}}R(\tilde{\theta},\theta) \pi_{m} (\theta)\,d\theta	&= \int_{(a,b)}\left(\frac{1}{n}-R(\tilde{\theta},\theta)\right)\pi_{m}(\theta)\,d\theta \\ 
&\qquad \qquad +\int_{\mathbb{R}\backslash(a,b)}\left(\frac{1}{n}-R(\tilde{\theta},\theta)\right)\pi_{m}(\theta)\,d\theta \\
	&\geq\epsilon\int_{(a,b)}\pi_{m}(\theta)\,d\theta \\
	&=\epsilon \mathbb{P}\left(\frac{a}{\sqrt{m}} < N(0,1) < \frac{b}{\sqrt{m}}\right) \\
	&=\epsilon\int_{\frac{a}{\sqrt{m}}}^{\frac{b}{\sqrt{m}}}\frac{1}{\sqrt{2\pi}}e^{-x^{2}/2}\,dx \\
	&\asymp\frac{1}{\sqrt{m}}.
\end{aligned}
$$

So there exists $m$ sufficiently large such that

$$
\frac{1}{n}-\int_{\mathbb{R}}R(\hat{\theta}_{\pi_{m}},\theta)\pi(\theta)\,d\theta<\frac{1}{n}-\int_{\mathbb{R}}R(\tilde{\theta},\theta)\pi_{m}(\theta)\,d\theta,
$$

which is equivalent to 

$$
\int_{\mathbb{R}}R(\tilde{\theta},\theta)\pi(\theta)\,d\theta<\int_{\mathbb{R}}R(\hat{\theta}_{\pi_{m}},\theta)\pi_{m}(\theta)\,d\theta.
$$

This is a contradiction as $\hat{\theta} _ {\pi_{m}}$ achieves the smallest Bayes risk by definition. 

</details>


Admissibility of $\overline{X} $ in higher dimensions is much more difficult. Let $X_{1},\ldots,X_{n}\overset{\mathrm{i.i.d.}}{\sim}N(\theta,I_{p})$ where $\theta\in\mathbb{R}^{p}$, and consider the loss function $L(\hat{\theta},\theta)=\Vert\hat{\theta}-\theta\Vert^{2}$. For $p=2$, admissibility of $\overline{X}$ was proved by Stein. The proof involves constructing much more complex priors. Surprisingly, $\overline{X}$ is no longer admissible if $p \geq 3$. Brown proved in 1971 that this phenomenon (aptly named Stein's paradox) is linked to the transience of the symmetric random walk in $p \geq 3$. 