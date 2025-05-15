# The rigorous argument

We will now give the rigorous argument which does not assume the existence of the second derivative of the log-likelihood. Instead of taking second derivative first and then apply the law of large numbers as we did above, we will apply the law of large numbers first. The key idea is that in some cases, the expectation operator can exhibit a smoothing property that allows $L(\theta):=\mathbb{E} _ {\theta^{\ast}}\log p _ {\theta}(X)$ to be twice differentiable even if the log-density is not. In this case, we have the second order Taylor expansion

$$
L(\theta^{\ast}+t)=L(\theta^{\ast})-\frac{t^{2}}{2}I_{\theta^{\ast}}+o(t^{2}).
$$

Let $L _ {n}(\theta)=\frac{1}{n}\sum_{i=1}^{n}\log p_{\theta}(X_{i})$ and define the empirical process operator $\nu_{n}$ by

$$
\nu_{n}f=\frac{1}{\sqrt{n}}\sum_{i=1}^{n}(f(X_{i})-\mathbb{E}_{\theta^{\ast}}f(X)).
$$

<details open>
<summary>Definition</summary>

We say that stochastic differentiability is satisfied if for every sequence $(U_{n})$ of shrinking neighborhoods of 0, 

$$
\sup_{t\in U_{n}}\frac{|\nu_{n}r(\cdot,t)|}{1+\sqrt{n}|t|}\overset{P_{\theta^{\ast}}}{\longrightarrow}0
$$

where $r$ is the remainder term in the first order expansion $\log p_{\theta^{\ast}+t}(X)=\log p_{\theta^{\ast}}(X)+tS_{\theta^{\ast}}(X)+|t|r(X,t).$ 
</details>

We will prove the following.

<details open>
<summary>Theorem</summary>

Assume that:

1. $\Vert\widehat{\theta}-\theta^{\ast}\Vert=o_{P_{\theta^{\ast}}}(1).$ 

2. Stochastic differentiability holds.

3. $L(\theta)$ has the second order expansion $L(\theta^{\ast}+t)=L(\theta^{\ast})-\frac{t^{2}}{2}I_{\theta^{\ast}}+o(t^{2})$ where $I_{\theta^{\ast}}=\mathbb{E}\left(S_{\theta^{\ast}}(X)\right)^{2}.$ 

Then $\sqrt{n}(\widehat{\theta}-\theta^{\ast})\rightsquigarrow N\left(0,I_{\theta^{\ast}}^{-1}\right).$
</details>

These assumptions are quite technical. Later on, we will give a simple condition which replaces the need to assume that $L(\theta)$ has the second order expansion above.

### Step 1: Derive a quadratic expansion for $L _ {n}(\theta)$

We have

$$
\begin{aligned}
L_{n}(\theta^{\ast}+t) &= L(\theta^{\ast}+t)+\frac{1}{\sqrt{n}}\nu_{n}\log p_{\theta^{\ast}+t} \\
	&=L(\theta^{\ast})-\frac{t^{2}}{2}I_{\theta^{\ast}}+o(t^{2})+\frac{1}{\sqrt{n}}\nu_{n}\left(\log p_{\theta^{\ast}}+tS_{\theta^{\ast}}+|t|r(\cdot,t)\right) \\
	&=\left(L(\theta^{\ast})+\frac{1}{\sqrt{n}}\nu_{n}\log p_{\theta^{\ast}}\right)+\frac{t}{\sqrt{n}}\nu_{n}S_{\theta^{\ast}}-\frac{t^{2}}{2}I_{\theta^{\ast}}+o(t^{2})+\frac{|t|}{\sqrt{n}}\nu_{n}r(\cdot,t) \\
	&=L_{n}(\theta^{\ast})+\frac{t}{n}\sum_{i=1}^{n}S_{\theta^{\ast}}(X_{i})-\frac{t^{2}}{2}I_{\theta^{\ast}}+o(t^{2})+\frac{|t|}{\sqrt{n}}\nu_{n}r(\cdot,t).
\end{aligned}
$$

This is almost the same expansion as we had from the intuitive argument. 

### Step 2: Show that $\widehat{\theta}$ is $\sqrt{n}$-consistent

Let $\widehat{t}=\widehat{\theta}-\theta^{\ast}.$ Then

$$
L_{n}(\theta^{\ast}+\widehat{t})=L_{n}(\theta^{\ast})+\frac{\widehat{t}}{n}\sum_{i=1}^{n}S_{\theta^{\ast}}(X_{i})-\frac{\widehat{t}^{2}}{2}I_{\theta^{\ast}}+o_{P_{\theta^{\ast}}}(\widehat{t}^{2})+\frac{|\widehat{t}|}{\sqrt{n}}\nu_{n}r(\cdot,\widehat{t}).
$$

Since $|\widehat{t}|=o_{P_{\theta^{\ast}}}(1)$ by consistency, we have

$$
\frac{|\nu_{n}r(\cdot,\widehat{t})|}{1+\sqrt{n}|\widehat{t}|}\leq\sup_{t\in U_{n}}\frac{|\nu_{n}r(\cdot,t)|}{1+\sqrt{n}|t|}=o_{P_{\theta^{\ast}}}(1).
$$

Therefore, 

$$
\frac{|\widehat{t}|}{\sqrt{n}}|\nu_{n}r(\cdot,\widehat{t})|\leq\frac{|\widehat{t}|}{\sqrt{n}}(o_{P_{\theta^{\ast}}}(1)+o_{P_{\theta^{\ast}}}(\sqrt{n}|\widehat{t}|))=o_{P_{\theta^{\ast}}}\left(\frac{|\widehat{t}|}{\sqrt{n}}\right)+o_{P_{\theta^{\ast}}}(\widehat{t}^{2}).
$$

By definition of $\widehat{\theta},$ $L_{n}(\theta^{\ast}+\widehat{t})\geq L_{n}(\theta^{\ast}),$ so

$$
0\leq\frac{\widehat{t}}{n}\sum_{i=1}^{n}S_{\theta^{\ast}}(X_{i})-\frac{\widehat{t}^{2}}{2}I_{\theta^{\ast}}+o_{P_{\theta^{\ast}}}(\widehat{t}^{2})+\frac{|\widehat{t}|}{\sqrt{n}}\nu_{n}r(\cdot,t).
$$

This gives

$$
\begin{aligned}
\frac{\widehat{t}^{2}}{2}I_{\theta^{\ast}} &\leq|\widehat{t}|\left|\frac{1}{n}\sum_{i=1}^{n}S_{\theta^{\ast}}(X_{i})\right|+\left|o_{P_{\theta^{\ast}}}(\widehat{t}^{2})\right|+\frac{|\widehat{t}|}{\sqrt{n}}\left|\nu_{n}r(\cdot,t)\right| \\
	&\leq|\widehat{t}|\left|\frac{1}{n}\sum_{i=1}^{n}S_{\theta^{\ast}}(X_{i})\right|+\left|o_{P_{\theta^{\ast}}}(\widehat{t}^{2})\right|+o_{P_{\theta^{\ast}}}\left(\frac{|\widehat{t}|}{\sqrt{n}}\right)
\end{aligned}
$$

which implies that

$$
\left(\frac{1}{2}I_{\theta^{\ast}}-o_{P_{\theta^{\ast}}}(1)\right)|\widehat{t}|\leq\left|\frac{1}{n}\sum_{i=1}^{n}S_{\theta^{\ast}}(X_{i})\right|+o_{P_{\theta^{\ast}}}\left(\frac{1}{\sqrt{n}}\right)=O_{P_{\theta^{\ast}}}\left(\frac{1}{\sqrt{n}}\right),
$$

so $|\widehat{t}|=O_{P_{\theta^{\ast}}}\left(\frac{1}{\sqrt{n}}\right).$ 

### Step 3: Show asymptotic normality

For any $|t|=O_{P_{\theta}^{\ast}}\left(\frac{1}{\sqrt{n}}\right)$, we have

$$
\begin{aligned}
L_{n}(\theta^{\ast}+t)	&= L_{n}(\theta^{\ast})+\frac{t}{n}\sum_{i=1}^{n}S_{\theta^{\ast}}(X_{i})-\frac{t^{2}}{2}I_{\theta^{\ast}}+o_{P_{\theta^{\ast}}}\left(\frac{1}{n}\right) \\
	&=L_{n}(\theta^{\ast})-\frac{1}{2}I_{\theta^{\ast}}\left(t-\frac{1}{n}\sum_{i=1}^{n}\frac{S_{\theta^{\ast}}(X_{i})}{I_{\theta^{\ast}}}\right)^{2}+\frac{1}{2}\frac{\left(\frac{1}{n}\sum_{i=1}^{n}S_{\theta^{\ast}}(X_{i})\right)^{2}}{I_{\theta^{\ast}}}+o_{P_{\theta^{\ast}}}\left(\frac{1}{n}\right).
\end{aligned}
$$

Let $\widetilde{t}=\sum_{i=1}^{n}S_{\theta^{\ast}}(X_{i})/I_{\theta^{\ast}}.$ Since both $|\widehat{t}|=O_{P_{\theta^{\ast}}}\left(\frac{1}{\sqrt{n}}\right)$ and $|\widetilde{t}|=O_{P_{\theta^{\ast}}}\left(\frac{1}{\sqrt{n}}\right)$ hold, the inequality $L_{n}(\theta^{\ast}+\widehat{t})\geq L_{n}(\theta^{\ast}+\widetilde{t})$ gives

$$
-\frac{1}{2}I_{\theta^{\ast}}\left(\widehat{t}-\frac{1}{n}\sum_{i=1}^{n}\frac{S_{\theta^{\ast}}(X_{i})}{I_{\theta^{\ast}}}\right)^{2}\geq o_{P_{\theta^{\ast}}}\left(\frac{1}{n}\right).
$$

This implies that 

$$
\frac{1}{2}I_{\theta^{\ast}}\left(\widehat{t}-\frac{1}{n}\sum_{i=1}^{n}\frac{S_{\theta^{\ast}}(X_{i})}{I_{\theta^{\ast}}}\right)^{2}=o_{P_{\theta^{\ast}}}\left(\frac{1}{n}\right)\implies\widehat{t}=\frac{1}{n}\sum_{i=1}^{n}\frac{S_{\theta^{\ast}}(X_{i})}{I_{\theta^{\ast}}}+o_{P_{\theta^{\ast}}}\left(\frac{1}{\sqrt{n}}\right).
$$

The central limit theorem now gives 

$$
\sqrt{n}(\widehat{\theta}-\theta^{\ast})=\frac{1}{\sqrt{n}}\sum_{i=1}^{n}\frac{S_{\theta^{\ast}}(X_{i})}{I_{\theta^{\ast}}}+o_{P_{\theta^{\ast}}}\left(1\right)\rightsquigarrow N(0,I_{\theta^{\ast}}^{-1}).
$$