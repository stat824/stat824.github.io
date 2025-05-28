# The restricted subspace property

Suppose now we have observations $Y$ given by $Y=X\theta ,$ where $X\in\mathbb{R}^{n\times d}$ is a fixed design matrix with $n\ll d.$ Since there is no noise, instead of bounding the risk of an estimator, we can instead hope to recover the exact solution. Our goal is to find the sparsest solution to $Y=X\theta.$ This is equivalent to 

$$
\min\left\{ \Vert\theta\Vert_{0}:Y=X\theta\right\} .
$$

This optimization problem is computationally intractable. One possible solution to this issue is to replace the objective with a convex approximation such as $\Vert\theta\Vert_{1}.$ 

<details open>
<summary>Definition</summary>
The optimization problem

$$
\min\left\{ \Vert\theta\Vert_{1}:Y=X\theta\right\} .
$$

is called the basis pursuit linear program.

</details>

Does the solution to the basis pursuit program recover the sparsest solution $\theta^{\ast}$? The answer depends on the null space of $X$ since the output to the basis pursuit linear program will find the minimizer of the $\ell^{1}$ norm in the affine subspace $\theta^{\ast}+\operatorname{null}(X).$ 


<details open>
<summary>Definition</summary>

For a subset $S\subset [d],$ define the critical cone

$$
\mathbb{C}(S):=\left\{ \Delta\in\mathbb{R}^{d}:\Vert\Delta_{S^{c}}\Vert_{1}\leq\Vert\Delta_{S}\Vert_{1}\right\} .
$$

A matrix $X$ is said to satisfy the restricted nullspace property with respect to $S$ if

$$
\operatorname{null}(X)\cap\mathbb{C}(S)=\{0\}.
$$
</details>


Another way to state the restricted nullspace property is that every non-zero vector $\Delta\in\operatorname{null}(X)$ satisfies $\Vert\Delta_{S^{c}}\Vert_{1}>\Vert\Delta_{S}\Vert_{1}.$ Intuitively, if $S$ is the support of $\theta^{\ast}$ and $X$ satisfies the restricted nullspace property with respect to $S,$ moving from $\theta^{\ast}$ along $\operatorname{null}(X)$ increases the $\ell^{1}$ norm. Thus, the solution to the basis pursuit program will be exactly $\theta^{\ast}.$

<details open>
<summary>Theorem</summary>

Let $S \subset [d]$ and $X\in\mathbb{R}^{n\times d}.$ The following are equivalent:

1. $X$ satisfies the restricted nullspace property with respect to $S.$

2. For any $Y\in\mathbb{R}^{n},$ any $\theta^{\ast}\in\mathbb{R}^{d}$ with $\operatorname{supp}(\theta^{\ast})=S$ and $Y=X\theta^{\ast}$ is the unique solution to the basis pursuit program $\min\left\{ \Vert\theta\Vert_{1}:Y=X\theta\right\} .$ 
</details>

<details>
<summary>Proof</summary>

**Proof of (1) $\Rightarrow$ (2):** Assume that $X\in\mathbb{R}^{n\times d}$ satisfies the restricted nullspace property with respect to $S\subset[d].$ Let $Y\in\mathbb{R}^{n}.$ Let $\widehat{\theta}$ be a solution to the basis pursuit linear program $\min\left\{ \Vert\theta\Vert_{1}:Y=X\theta\right\}$ and let $\theta^{\ast}$ satisfy $\operatorname{supp}(\theta^{\ast})=S$ and $Y=X\theta^{\ast}.$ Now define $\Delta$ so that $\widehat{\theta}=\theta^{\ast}+\Delta .$ We will show that $\Delta\in\operatorname{null}(X)\cap\mathbb{C}(S)$ and hence $\Delta=0$ by our assumption. First note that

$$
\begin{aligned}
\Vert\theta_{S}^{\ast}\Vert_{1}	&= \Vert\theta^{\ast}\Vert_{1} \\
	&\geq\Vert\widehat{\theta}\Vert_{1} \\ 
	&=\Vert\theta^{\ast}+\Delta\Vert_{1} \\
	&=\Vert\theta^{\ast}+\Delta_{S}\Vert_{1}+\Vert\Delta_{S^{c}}\Vert_{1} \\
	&\geq\Vert\theta_{S}^{\ast}\Vert_{1}-\Vert\Delta_{S}\Vert_{1}+\Vert\Delta_{S^{c}}\Vert_{1}.
\end{aligned}
$$

Rearranging gives $\Vert\Delta_{S^c}\Vert_{1}\leq\Vert\Delta_{S}\Vert_{1},$ and thus $\Delta\in\mathbb{C}(S).$ The fact that $\Delta\in\operatorname{null}(X)$ follows from the observations that $Y=X\theta^{\ast}$ and $Y=X\widehat{\theta},$ so $0=X(\widehat{\theta}-\theta^{\ast})=X\Delta .$ Since $X$ satisfies the restricted nullspace property with respect to $S,$ it follows that $\Delta=0,$ giving $\theta^{\ast}=\widehat{\theta}.$

**Proof of (2) $\Rightarrow$ (1):** Let $S\subset[d]$ and assume that for all $Y\in\mathbb{R}^{n},$ each $S$-sparse vector $\theta$ satisfying $Y=X\theta$ is the unique solution to the basis pursuit linear program $\min\left\{ \Vert\theta\Vert_{1}:Y=X\theta\right\} .$ We need to show that $\mathbb{C}(S)\cap\operatorname{null}(X)=\{0\}.$ Suppose that $\theta^{\ast}\in\operatorname{null}(X)\backslash\{0\}.$ Consider the basis pursuit problem 

$$
\min\left\{ \Vert\beta\Vert_{1}:X\beta=Y\right\} ,\quad Y=X\left(\begin{array}{c}
\theta_{S}^{\ast}\\
0
\end{array}\right).
$$

Since $\widehat{\beta}=(\theta_{S}^{\ast},0)^{T}$ is $S$-sparse and satisfies $X\widehat{\beta}=Y,$ it must be the unique solution to the basis pursuit linear program. Since $X\theta^{\ast}=0,$ it follows that 


$$
X\left(\begin{array}{c}
\theta_{S}^{\ast}\\
0
\end{array}\right)+X\left(\begin{array}{c}
0\\
\theta_{S^{c}}^{\ast}
\end{array}\right)=0\implies X\left(\begin{array}{c}
\theta_{S}^{\ast}\\
0
\end{array}\right)=X\left(\begin{array}{c}
0\\
-\theta_{S^{c}}^{\ast}
\end{array}\right).
$$

Therefore, 

$$
\widetilde{\beta}=\left(\begin{array}{c}
0\\
-\theta_{S^{c}}^{\ast}
\end{array}\right)
$$

also satisfies $X\widetilde{\beta}=Y.$ Since $\widehat{\beta}$ is the unique solution to the basis pursuit program, it follows that 

$$
\Vert \widehat{\beta} \Vert_1 < \Vert \widetilde{\beta} \Vert_1 \implies \Vert\theta_{S}^{\ast}\Vert_{1}<\Vert\theta_{S^{c}}^{\ast}\Vert_{1}.
$$

This implies that $\theta^{\ast}\not\in\mathbb{C}(S).$
</details>

