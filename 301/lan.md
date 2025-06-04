# Local asymptotic normality

<details open>
<summary>Definition</summary>

Let us say that a statistical model $(P_{\theta}:\theta\in\Theta)$ satisfies local asymptotic normality (LAN) at $\theta$ if

$$
\log\prod_{i=1}^{n}\frac{p_{\theta+h/\sqrt{n}}(X_{i})}{p_{\theta}(X_{i})}=\frac{h}{\sqrt{n}}\sum_{i=1}^{n}S_{\theta}(X_{i})-\frac{h^{2}}{2}I_{\theta}+o_{P_{\theta}}\left(1\right)
$$

for any $h$ independent of $n$. 
</details>

Let $\widehat{\theta}$ be the maximum likelihood estimator. Then LAN at $\theta^{\ast}$ along with consistency and stochastic differentiability together guarantee that $\sqrt{n}(\widehat{\theta}-\theta^{\ast})\rightsquigarrow N(0,I_{\theta^{\ast}}^{-1}).$ 

<details open>
<summary>Definition</summary>

Let us say that the parametric family $(P_{\theta}:\theta\in\Theta)$ satisfies differentiability in quadratic mean (DQM) at $\theta$ if

$$
\int\left(\frac{\sqrt{p_{\theta+t}(x)}-\sqrt{p_{\theta}(x)}}{t}-\frac{1}{2}\sqrt{p_{\theta}(x)}S_{\theta}(x)\right)^{2}\to0\quad\text{as }t\to0.
$$
</details>

It is easy to show that the pointwise derivative $\frac{\partial}{\partial\theta}\sqrt{p_{\theta}(x)}$ is given by $\frac{1}{2}\sqrt{p_{\theta}(x)}S_{\theta}(x).$ Therefore, DQM simply asserts that the map $\theta\mapsto\sqrt{p_{\theta}}$ is Fréchet differentiable in $L^{2}$ at $\theta.$ Remarkably, DQM implies LAN. This means that we can essentially replace the second order expansion assumption for asymptotic normality of MLE with a first order differentiability condition. 

<details open>
<summary>Theorem</summary>

Suppose that DQM holds at $\theta$. Then $\mathbb{E} _ {\theta}S_{\theta}(X)=0$ and LAN holds at $\theta$  with $I_{\theta}=\mathbb{E} _ {\theta}(S_{\theta}(X))^{2}.$
</details>

### Part 1: Show that $\mathbb{E} _ {\theta}S _ {\theta}(X)=0$

Let $h$ be independent of $n$. Taking $t=h/\sqrt{n}$, we see that DQM holds at $\theta$ if and only if

$$
\int\left(\sqrt{n}\left(\sqrt{p_{\theta+h/\sqrt{n}}}-\sqrt{p_{\theta}}\right)-\frac{1}{2}h\sqrt{p_{\theta}}S_{\theta}\right)^{2}=o(1).
$$

We have

$$
\mathbb{E}_{\theta}S_{\theta}(X) =\int p_{\theta}S_{\theta}=2\int\frac{1}{2}h\sqrt{p_{\theta}}S_{\theta}\sqrt{p_{\theta}}=I_{1}+I_{2},
$$

where 

$$
I_{1}=2\int\left(\frac{1}{2}h\sqrt{p_{\theta}}S_{\theta}-\sqrt{n}\left(\sqrt{p_{\theta+h/\sqrt{n}}}-\sqrt{p_{\theta}}\right)\right),
$$

and

$$
I_{2}=2\int\sqrt{n}\left(\sqrt{p_{\theta+h/\sqrt{n}}}-\sqrt{p_{\theta}}\right)\sqrt{p_{\theta}}.
$$

Then by the Cauchy-Schwarz inequality

$$
|I_{1}|\leq2\sqrt{\int\left(\frac{1}{2}h\sqrt{p_{\theta}}S_{\theta}-\sqrt{n}\left(\sqrt{p_{\theta+h/\sqrt{n}}}-\sqrt{p_{\theta}}\right)\right)^{2}}\sqrt{\int p_{\theta}}=o(1).
$$

Let $f_{n}=\sqrt{p_{\theta+h/\sqrt{n}}}-\sqrt{p_{\theta}}$ and $g_{n}=\frac{1}{2}\frac{h}{\sqrt{n}}\sqrt{p_{\theta}}S_{\theta}.$ Then

$$
\begin{aligned}
|I_{2}|	&=2\sqrt{n}\left|\int\sqrt{p_{\theta+h/\sqrt{n}}p_{\theta}}-1\right| \\
	&=\sqrt{n}H^{2}(P_{\theta+h.\sqrt{n}},P_{\theta}) \\
	&=\sqrt{n}\left|\int f_{n}^{2}\right| \\
	&=\sqrt{n}\int(f_{n}-g_{n}+g_{n})^{2} \\
	&=\sqrt{n}\int g_{n}^{2}+\sqrt{n}\int(f_{n}-g_{n})^{2}+2\sqrt{n}\int(f_{n}-g_{n})g_{n}.
\end{aligned}
$$

We have

$$
\sqrt{n}\int g_{n}^{2}=\sqrt{n}\int\frac{1}{4}\frac{h^{2}}{n}p_{\theta}S_{\theta}^{2}=\frac{h^{2}}{4n}I_{\theta} = o(1).
$$

The DQM condition is equivalent to $\int(f_{n}-g_{n})^{2}=o(n^{-1}),$ so we have

$$
\sqrt{n}\int(f_{n}-g_{n})^{2}=o(n^{-1/2}).
$$

Applying the Cauchy-Schwarz inequality, we get

$$
2\sqrt{n}\int(f_{n}-g_{n})g_{n}\leq2\sqrt{n}\sqrt{\int(f_{n}-g_{n})^{2}}\sqrt{\int g_{n}^{2}} = o(1).
$$

We conclude that $\mathbb{E} _ {\theta}S_{\theta}(X) = 0.$

### Part 2: Show that LAN holds at $\theta$

Note that DQM can equivalently by stated as

$$
\int p_{\theta}\left(\sqrt{\frac{p_{\theta+h/\sqrt{n}}}{p_{\theta}}}-1-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}\right)^{2}=o(n^{-1}).
$$

Let $W_{i}=\sqrt{\frac{p_{\theta+h/\sqrt{n}}(X_{i})}{p_{\theta}(X_{i})}}-1.$ Then 

$$
\log\prod_{i=1}^{n}\frac{p_{\theta+h/\sqrt{n}}(X_{i})}{p_{\theta}(X_{i})}	=2\log\prod_{i=1}^{n}\left(\sqrt{\frac{p_{\theta+h/\sqrt{n}}(X_{i})}{p_{\theta}(X_{i})}}-1+1\right)=2\sum_{i=1}^{n}\log(W_{i}+1).
$$

Using the Taylor expansion $\log(x+1)=x-\frac{x^{2}}{2}+o(1),$ we have

$$
2\sum_{i=1}^{n}\log(W_{i}+1)=2\sum_{i=1}^{n}W_{i}-\sum_{i=1}^{n}W_{i}^{2}+o_{P_{\theta}}(1).
$$

We will analyze the convergence of $\sum_{i=1}^{n}W_{i}$ and $\sum_{i=1}^{n}W_{i}^{2}$ in probability.

#### Convergence of $\sum_{i=1}^{n}W_{i}$

Let $c_{n}=\sqrt{n}\left(\sqrt{p_{\theta+h/\sqrt{n}}}-\sqrt{p_{\theta}}\right)$ and $c=\frac{1}{2}h\sqrt{p_{\theta}}S_{\theta}.$ Since $c_{n}=\sqrt{n}f_{n}$ and $c=\sqrt{n}g_{n},$ it follows from $\int(f_{n}-g_{n})^{2}=o(n^{-1})$ that $\int(c_{n}-c)^{2}=o(1).$ Then

$$
\begin{aligned}
\mathbb{E}_{\theta}\sum_{i=1}^{n}W_{i} &=n\left(\int\sqrt{p_{\theta}p_{\theta+h/\sqrt{n}}}-1\right) \\
	&=-\frac{n}{2}\int\left(\sqrt{p_{\theta+h/\sqrt{n}}}-\sqrt{p_{\theta}}\right)^{2} \\
	&=-\frac{1}{2}\int c_{n}^{2} \\ 
	&=-\frac{1}{2}\int(c_{n}-c+c)^{2} \\
	&=-\frac{1}{2}\int c^{2}-\frac{1}{2}\int(c_{n}-c)^{2}-\int(c_{n}-c)c \\
	&=-\frac{1}{2}\int c^{2}-\int(c_{n}-c)c+o(1).
\end{aligned}
$$

Then

$$
-\frac{1}{2}\int c^{2}=-\frac{1}{2}\int\frac{1}{4}h^{2}p_{\theta}S_{\theta}^{2}=-\frac{1}{8}h^{2}I_{\theta},
$$

and by the Cauchy-Schwarz inequality we have

$$
\left|\int(c_{n}-c)c\right|\leq\sqrt{\int(c_{n}-c)^{2}}\sqrt{\int c^{2}}=o(1).
$$

Therefore, $\mathbb{E} _ {\theta}\sum_{i=1}^{n}W_{i}=-\frac{1}{8}h^{2}I_{\theta}+o(1).$ Since $\mathbb{E} _ {\theta}S_{\theta}(X_{i})=0,$ it follows that

$$
\mathbb{E}_{\theta}\sum_{i=1}^{n}\left(W_{i}-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{i})\right)=-\frac{1}{8}h^{2}I_{\theta}+o(1).
$$

Also,

$$
\begin{aligned}
\operatorname{Var}_{\theta}\left(\sum_{i=1}^{n}\left(W_{i}-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{i})\right)\right)	&= n\operatorname{Var}_{\theta}\left(W_{1}-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{1})\right) \\
	&\leq n\mathbb{E}_{\theta}\left(W_{1}-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{1})\right)^{2} \\
	&=n\int p_{\theta}\left(\sqrt{\frac{p_{\theta+1/\sqrt{n}}}{p_{\theta}}}-1-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}\right)^{2} \\
	&=n\cdot o(n^{-1}) \\
	&=o(1).
\end{aligned}
$$

The variance converging to 0 implies that $\sum_{i=1}^{n}\left(W_{i}-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{i})\right)$ converges in probability to its mean, so we have

$$
\sum_{i=1}^{n}W_{i}-\frac{1}{2}\frac{h}{\sqrt{n}}\sum_{i=1}^{n}S_{\theta}(X_{i})=-\frac{1}{8}h^{2}I_{\theta}+o_{P_{\theta}}(1).
$$

Rearranging gives

$$
\sum_{i=1}^{n}W_{i}=\frac{1}{2}\frac{h}{\sqrt{n}}\sum_{i=1}^{n}S_{\theta}(X_{i})-\frac{1}{8}h^{2}I_{\theta}+o_{P_{\theta}}(1).
$$

#### Convergence of $\sum_{i=1}^{n}W_{i}^{2}$ 

We have

$$
\begin{aligned}
\sum_{i=1}^{n}W_{i}^{2}	&=\sum_{i=1}^{n}\left(W_{i}-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{i})+\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{i})\right)^{2} \\
	&=\sum_{i=1}^{n}\left(W_{i}-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{i})\right)^{2}+\sum_{i=1}^{n}\left(\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{i})\right)^{2} \\ &\qquad \qquad \qquad +2\sum_{i=1}^{n}\left(W_{i}-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{i})\right)\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{i}).
\end{aligned}
$$

Call the three terms $S_{1}$, $S_{2}$, and $S_{3}.$ For the first term, we have already found that

$$
\mathbb{E}_{\theta}S_{1}=n\mathbb{E}_{\theta}\left(W_{1}-\frac{1}{2}\frac{h}{\sqrt{n}}S_{\theta}(X_{1})\right)^{2}=o(1).
$$

Therefore, $S_{1}=o_{P_{\theta}}(1).$ For the second term, by the law of large numbers we have

$$
S_{2}=\frac{h^{2}}{4}\frac{1}{n}\sum_{i=1}^{n}S_{\theta}(X_{i})^{2}=\frac{h^{2}}{4}I_{\theta}+o_{P_{\theta}}(1)=o_{P_{\theta}}(1).
$$

For the third term, by the Cauchy-Schwarz inequality we have

$$
\left|S_{3}\right|\leq2\sqrt{S_{1}}\sqrt{S_{2}}=o_{P_{\theta}}(1).
$$

Thus, we have

$$
\sum_{i=1}^{n}W_{i}^{2}=\frac{h^{2}}{4}I_{\theta}+o_{P_{\theta}}(1).
$$

#### Conclude

Putting everything together, we have

$$
\begin{aligned}
\log\prod_{i=1}^{n}\frac{p_{\theta+h/\sqrt{n}}(X_{i})}{p_{\theta}(X_{i})} &= 2\sum_{i=1}^{n}W_{i}-\sum_{i=1}^{n}W_{i}^{2}+o_{P_{\theta}}(1) \\
	&=2\left(\sum_{i=1}^{n}W_{i}\right)-\sum_{i=1}^{n}W_{i}^{2}+o_{P_{\theta}}(1) \\
	&=2\left(\frac{1}{2}\frac{h}{\sqrt{n}}\sum_{i=1}^{n}S_{\theta}(X_{i})-\frac{1}{8}h^{2}I_{\theta}+o_{P_{\theta}}(1)\right)-\left(\frac{h^{2}}{4}I_{\theta}+o_{P_{\theta}}(1)\right)+o_{P_{\theta}}(1) \\
	&=\frac{h}{\sqrt{n}}\sum_{i=1}^{n}S_{\theta}(X_{i})-\frac{1}{2}h^{2}I_{\theta}+o_{P_{\theta}}(1)
\end{aligned}
$$

which shows that LAN holds at $\theta.$ 