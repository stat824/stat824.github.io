# Blockwise James-Stein estimator

Let us now consider the blockwise James-Stein estimator which does not require knowledge of the smoothness parameter. Let $\{1,2,\ldots,n\}=B_{1}\cup\cdots\cup B_{m}$, where $B_{\ell}=\{3^{\ell-1}+1,\ldots,3^{\ell}\}$ and $m=\log_{3} n$. Consider the estimator

$$
\widehat{\theta}=\left(\begin{array}{c}
\widehat{\theta}_{B_{1}}\\
\widehat{\theta}_{B_{2}}\\
\vdots\\
\widehat{\theta}_{B_{m}}\\
0
\end{array}\right),\quad\widehat{\theta}_{B_{\ell}}=\left(1-\frac{|B_{\ell}|-2}{n\Vert X_{\ell}\Vert^{2}}\right) X_{\ell}.
$$

Then by the oracle inequality we have

$$
\begin{aligned}
\mathbb{E} _ \theta \Vert\widehat{\theta}-\theta\Vert^{2} &=\sum_{\ell=1}^{m}\mathbb{E}_ \theta \Vert\widehat{\theta}_{B_{\ell}}-\theta_{B_{\ell}}\Vert^{2}+\sum_{j>m}\theta_{j}^{2} \\
	&\leq\sum_{\ell=1}^{m}\min\left(\frac{|B_{\ell}|}{n},\Vert\theta_{B_{\ell}}\Vert^{2}\right)+\frac{2m}{n}+\sum_{j>n}\theta_{j}^{2}.
\end{aligned}
$$

Note that

$$
\frac{2m}{n}=\frac{2\log_{3}n}{n}=o\left(n^{-\frac{2\alpha}{\alpha+1}}\right)\quad\text{and}\quad\sum_{j>n}\theta_{j}^{2}\leq\frac{R^{2}}{n^{2\alpha}}=o\left(n^{-\frac{2\alpha}{\alpha+1}}\right).
$$

Choosing $L=\min\{\ell\in\mathbb{N}:3^{\ell}\geq n^{\frac{1}{2\alpha+1}}\}$, we have $3^{L-1}\leq n^{\frac{1}{2\alpha+1}}\leq3^{L}$, so

$$
\begin{aligned}
\sum_{\ell=1}^{m}\min\left(\frac{|B_{\ell}|}{n},\Vert\theta_{B_{\ell}}\Vert^{2}\right)	&\leq\sum_{\ell=1}^{L}\frac{|B_{\ell}|}{n}+\sum_{\ell=L+1}^{m}\Vert\theta_{B_{\ell}}\Vert^{2} \\
	&\leq\sum_{\ell=1}^{L}\frac{2}{3n}3^{\ell}+\sum_{j>3^{L}}|\theta_{j}|^{2} \\
	&\lesssim \frac{3^{L}}{n}+\sum_{j>n^{\frac{1}{2\alpha+1}}}|\theta_{j}|^{2} \\
	&\lesssim \frac{n^{\frac{1}{2\alpha+1}}}{n}+\left(n^{\frac{1}{2\alpha+1}} \\\right)^{-2\alpha} \\
	&\lesssim n^{-\frac{2\alpha}{2\alpha+1}}.
\end{aligned}
$$

Adding up all the terms, we get $\mathbb{E} _ \theta \Vert\widehat{\theta} - \theta\Vert^{2}\lesssim n^{-\frac{2\alpha}{2\alpha+1}}$. So the block-wise James-Stein estimator also achieves the minimax rate. 