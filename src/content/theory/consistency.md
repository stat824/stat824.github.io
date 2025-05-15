# Consistency of MLE

Suppose that $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}P_{\theta^{\ast}}$. The maximum likelihood estimator is defined to be

$$
\widehat{\theta}=\argmax_{\theta}\sum_{i=1}^{n}\log p_{\theta}(X_{i}).
$$ 

Under identifiability and some empirical process condition, we will prove that the MLE $\widehat{\theta}$ is consistent, meaning that

$$
\mathbb{P}_{\theta^{\ast}}\left(\Vert\widehat{\theta}-\theta^{\ast}\Vert>\epsilon\right)\overset{n\to\infty}{\longrightarrow}0.
$$

The proof will be split into two parts. Firstly, we bound the probability in terms of the Kullback–Leibler divergence of $P_{\theta^\ast}$ and $P_{\widehat{\theta}}$. Then we finish off by applying a uniform law of large numbers. 

## Kullback–Leibler divergence

For any two distributions $P$ and $Q$ with densities $p$ and $q$, we define the Kullback–Leibler divergence $D(P\Vert Q)$ to be

$$
D(P\Vert Q)=\int p\log\frac{p}{q}.
$$

The KL divergence is always non-negative.

<details open>
<summary>Lemma</summary>

For any two probability distributions $P$ and $Q$, we have $D(P\Vert Q) \geq 0$.
</details>

<details>
<summary>Proof</summary>

We have

$$
D(P\Vert Q)=\int p\log\frac{p}{q}=\int qf(\frac{p}{q}),
$$

where $f(t)=t\log t$. Since $f$ is convex, by Jensen's inequality, we have

$$
\int qf(\frac{p}{q})	=\mathbb{E}_{X\sim Q}f\left(\frac{p(X)}{q(X)}\right)
	\geq f\left(\mathbb{E}_{X\sim Q}\frac{p(X)}{q(X)}\right)
	=f(1)
	=0.
$$
</details>

In fact, we have a strong result.

<details open>
<summary>Lemma</summary>

For any two probability distributions $P$ and $Q$, we have $D(P\Vert Q)\geq H^{2}(P,Q)$, where $H^{2}(P,Q)=\frac{1}{2}\int(\sqrt{p}-\sqrt{q})^{2}$ is the squared Hellinger distance, 
</details>

See homework for the proof of the above. 

## Identifiability

Another way to write the MLE is

$$
\widehat{\theta}=\argmin_{\theta}\frac{1}{n}\sum_{i=1}^{n}\log\frac{p_{\theta^{\ast}}(X_{i})}{p_{\theta}(X_{i})}.
$$

By the law of large numbers, for each fixed $\theta$, 

$$
\frac{1}{n}\sum_{i=1}^{n}\log\frac{p_{\theta^{\ast}}(X_{i})}{p_{\theta}(X_{i})}\overset{n\to\infty}{\longrightarrow}\int p_{\theta^{\ast}}\log\frac{p_{\theta^{\ast}}}{p_{\theta}}=D(P_{\theta^{\ast}}\Vert P_{\theta}).
$$

What is the minimizer of this limiting quantity? Of course, $\theta=\theta^{\ast}$ minimizes the expression, but there could be other values of $\theta$ that minimize the expression if we have $P_{\theta_{1}}=P_{\theta_{2}}$ for some $\theta_{1}\neq\theta_{2}$. To ensure that the MLE converges to the true parameter $\theta^\ast$, we must avoid such a situation. We need to assume $\theta_{1}\neq\theta_{2}\implies P_{\theta_{1}}\neq P_{\theta_{2}}.$ More precisely, we assume that for all $\epsilon>0$, there exists $\delta>0$ such that

$$
\Vert\theta_{1}-\theta_{2}\Vert>\epsilon\implies D(P_{\theta_{1}}\Vert P_{\theta_{2}})>\delta.
$$

We call this condition identifiability. Then given $\epsilon>0$, we have

$$
\mathbb{P}_{\theta^{\ast}}\left(\Vert\widehat{\theta}-\theta^{\ast}\Vert>\epsilon\right)	\leq\mathbb{P}_{\theta^{\ast}}\left(D(P_{\theta^{\ast}}\Vert P_{\widehat{\theta}})>\delta\right).
$$

## Uniform law of large numbers

We have 

$$
D(P_{\theta^{\ast}}\Vert P_{\widehat{\theta}})=\int p_{\theta^{\ast}}\log p_{\theta^{\ast}}-\int p_{\theta^{\ast}}\log p_{\widehat{\theta}}
$$

 and for large $n$, 

$$
\int p_{\theta^{\ast}}\log p_{\theta^{\ast}}\approx\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta^{\ast}}(X_{i})\quad\text{and}\quad\int p_{\theta^{\ast}}\log p_{\widehat{\theta}}\approx\frac{1}{n}\sum_{i=1}^{n}\log p_{\widehat{\theta}}(X_{i}).
$$

The key intuition is that because $\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta^{\ast}}(X_{i})$ is smaller than $\frac{1}{n}\sum_{i=1}^{n}\log p_{\widehat{\theta}}(X_{i})$ by definition of $\widehat{\theta}$, it is impossible for $\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta^{\ast}}(X_{i}) - \frac{1}{n}\sum_{i=1}^{n}\log p_{\widehat{\theta}}(X_{i}) > \delta $ to hold, so we should expect $\mathbb{P} _ {\theta^{\ast}}\left(D(P_{\theta^{\ast}}\Vert P_{\widehat{\theta}})>\delta\right)$ to approach 0 as the approximations get more precise. By the law of large numbers, we have

$$
\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta^{\ast}}(X_{i}) \underset{n \to \infty}{\overset{P_{\theta^{\ast}}}{\longrightarrow}} \int p_{\theta^{\ast}}\log p_{\theta^{\ast}}.
$$

However, for the other sum, we cannot directly apply the law of large numbers to obtain

$$
\frac{1}{n}\sum_{i=1}^{n}\log p_{\widehat{\theta}}(X_{i}) \underset{n \to \infty}{\overset{P_{\theta^{\ast}}}{\longrightarrow}} \int p_{\theta^{\ast}}\log p_{\widehat{\theta}}
$$

because $\log p_{\widehat{\theta}}(X_{1}),\log P_{\widehat{\theta}}(X_{2}),\ldots$ are not i.i.d. due to the dependence on $\widehat{\theta}$. Instead, we make use of the uniform law of large numbers

$$
\sup_{\theta \in \Theta}\left|\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta}(X_{i})-\int p_{\theta^{\ast}}\log p_{\theta}\right| \underset{n \to \infty}{\overset{P_{\theta^{\ast}}}{\longrightarrow}} 0
$$

which holds under some VC-dimension assumptions. We then have

$$
\begin{aligned}
D(P_{\theta^{\ast}}\Vert P_{\widehat{\theta}}) &=\int p_{\theta^{\ast}}\log p_{\theta^{\ast}}-\int p_{\theta^{\ast}}\log p_{\widehat{\theta}} \\
	&\leq\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta^{\ast}}(X_{i})-\frac{1}{n}\sum_{i=1}^{n}\log p_{\widehat{\theta}}(X_{i}) +\left|\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta^{\ast}}(X_{i})-\int p_{\theta^{\ast}}\log p_{\theta^{\ast}}\right| \\ &\qquad \qquad +\left|\frac{1}{n}\sum_{i=1}^{n}\log p_{\widehat{\theta}}(X_{i})-\int p_{\theta^{\ast}}\log p_{\widehat{\theta}}\right| \\
	&\leq\frac{1}{n}\sum_{i=1}^{n}(\log p_{\widehat{\theta}}(X_{i})-\log p _ {\widehat{\theta}}(X_{i}))+2\sup_{\theta}\left|\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta}(X_{i})-\int p_{\theta^{\ast}}\log p_{\theta}\right| \\
	&=2\sup_{\theta}\left|\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta}(X_{i})-\int p_{\theta^{\ast}}\log p_{\theta}\right|.
\end{aligned}
$$

Therefore, 

$$
\mathbb{P}_{\theta^{\ast}}\left(D(P_{\theta^{\ast}}\Vert P_{\widehat{\theta}})>\delta\right)\leq\mathbb{P}_{\theta^{\ast}}\left(2\sup_{\theta}\left|\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta}(X_{i})-\int p_{\theta^{\ast}}\log p_{\theta}\right|>\delta\right)
$$

which converges to 0 as $n\to\infty$ by the uniform law of large numbers. 


