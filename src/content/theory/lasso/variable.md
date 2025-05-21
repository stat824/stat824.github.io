# Variable selection with lasso

Under specific conditions, the Lasso can be used for variable selection. In other words, it can recover the support set $S=\operatorname{supp}(\theta^{\ast}).$ 

## Assumptions and statement of main result

We will make the following assumptions:

* **Lower eigenvalue:** There exists $c_{\min}>0$ such that

  $$
  \sigma_{\min}\left(\frac{X_{S}^{T}X_{S}}{n}\right)\geq c_{\min}.
  $$

* **Mutual incoherence:** There exists $\alpha\in[0,1)$ such that

  $$
  \max_{j\in S^{c}}\Vert(X_{S}^{T}X_{S})^{-1}X_{S}^{T}X_{j}\Vert_{1}\leq\alpha.
  $$

To see what mutual incoherence means, suppose that we tried to predict the column vector $X_{j}$ using a combination of the columns of $X_{S}.$ The best weight vector $\widehat{\omega}\in\mathbb{R}^{|S|}$ is the minimum 2-norm solution to the problem

$$
\min_{\omega}\Vert X_{j}-X_{S}\omega\Vert_{2}^{2},
$$

which is given by $\widehat{\omega}=X_{S}^{\dagger}X_{j}=(X_{S}^{T}X_{S})^{-1}X_{S}^{T}X_{j}.$ So the mutual incoherence is a bound on the 1-norm $\Vert\widehat{\omega}\Vert_{1}.$ If we want to minimize it, the best case scenario occurs when the column space of $X_{S}$ is orthogonal to $X_{j},$ in which case the optimal weight vector would be the zero vector. In general, we cannot expect this orthogonality to hold, so the mutual incoherence condition imposes a type of approximate orthogonality between the columns of $X_{S}$ and $X_{S^{c}}.$

<details open>
<summary>Theorem</summary>

Consider the linear model 

$$
Y=X\theta^{\ast}+\epsilon
$$

where $X\in\mathbb{R}^{n\times d}$ is a fixed design matrix and $\epsilon\in\mathbb{R}^{n}$ is any random noise (not necessarily sub-Gaussian). Let $S=\operatorname{supp}(\theta^{\ast})$ and assume that the design matrix $X$ satisfies the lower eigenvalue and the mutual incoherence conditions above. Then for any choice of $\lambda_{n}$ such that

$$
\lambda_{n}\geq\frac{2}{1-\alpha}\left\Vert X_{S^{c}}^{T}\Pi_{S^{\perp}}\frac{\epsilon}{n}\right\Vert _{\infty},
$$

where $\Pi_{S^{\perp}}=I_{n}-X_{S}(X_{S}^{T}X_{S})^{-1}X_{S}^{T}$ is the orthogonal projection onto $\operatorname{col}(X_{S})^{\perp},$ the regularized Lasso has the following properties:

1. **Uniqueness:** There is a unique optimal solution $\widehat{\theta}.$

2. **No false inclusion:** The solution $\widehat{\theta}$ has its support set contained within the true support set $S.$

3. **$\ell_{\infty}$-bound:** The error $\widehat{\theta}-\theta^{\ast}$ satisfies $\Vert\widehat{\theta} _ {S}-\theta _ {S}^{\ast}\Vert_{\infty}\leq B(\lambda_{n},X),$ where

   $$
   B(\lambda_{n},X)=\left\Vert \left(\frac{X_{S}^{T}X_{S}}{n}\right)^{-1}X_{S}^{T}\frac{\epsilon}{n}\right\Vert _{\infty}+\left\Vert \left(\frac{X_{S}^{T}X_{S}}{n}\right)^{-1}\right\Vert _{\infty}\lambda_{n}.
   $$

4. **No false exclusion:** The solution $\widehat{\theta}$ includes all indices $i\in S$ such that $\theta_{i}^{\ast}>B(\lambda_{n},X)$ and hence is variable selection consistent if $\min_{i\in S}|\theta_{i}^{\ast}|>B(\lambda_{n},X).$

</details>

## KKT conditions for the Lasso

As a reminder on convex optimization, given a convex function $f:\mathbb{R}^{d}\to\mathbb{R},$ we say that $z\in\mathbb{R}^{d}$ is a subgradient of $f$ at $\theta ,$ denoted by $z\in\partial f(\theta),$ if we have

$$
f(\theta+\Delta)\geq f(\theta)+\langle z,\Delta\rangle\quad\text{for all }\Delta\in\mathbb{R}^{d}.
$$

Given the constrained optimization problem

$$
\min\{f(x):h_{i}(x)\leq0\text{ for }i=1,\ldots,m,\,g_{j}(x)=0\text{ for }j=1,\ldots,r\},
$$

the Karush-Kuhn-Tucker (KKT) conditions are: 

* Stationarity: $0\in\partial f(x)+\sum_{i=1}^{m}u_{i}\partial h_{i}(x)+\sum_{j=1}^{r}v_{j}\partial g_{j}(x)$

* Complementary: $u_{i}h_{i}(x)=0$ for all $i$

* Primal feasibility: $h_{i}(x)\leq0$ for all $i$ and $g_{j}(x)=0$ for all $j$

* Dual feasibility: $u_{i}\geq0$ for all $i$

The necessary and sufficient conditions for optimality of the Lasso are that it must satisfy the KKT conditions. For $f(\theta)=\Vert\theta\Vert_{1},$ it can be found that $z\in\partial f(\theta)$ if and only if $z_{j}=\operatorname{sign}(\theta_{j})$ for all $j=1,\ldots,d$ where we define $\operatorname{sign}(0)$ to refer to any number in $[-1,1].$ The KKT conditions give the following characterization of solutions to the Lasso program. 

<details open>
<summary>Lemma</summary>

Let $F(\theta)=\frac{1}{2n}\Vert X\theta-Y\Vert_{2}^{2},$ so that $\nabla F(\theta)=\frac{1}{n}X^{T}(X\widehat{\theta}-Y).$ The vector $\widehat{\theta}\in\mathbb{R}^{d}$ is a solution of the Lasso program with parameter $\lambda_{n}$ if and only if

$$
\begin{cases}
\nabla_{j}F(\widehat{\theta})=-\lambda_{n}\operatorname{sign}(\widehat{\theta}_{j}) & \text{if }\widehat{\theta}_{j}\neq0,\\
|\nabla_{j}F(\widehat{\theta})|\leq\lambda_{n} & \text{if }\widehat{\theta}_{j}=0.
\end{cases}
$$

Moreover, if $|\nabla_{j}F(\widehat{\theta})|<\lambda_{n}$ for some solution $\widehat{\theta},$ then $\widehat{\theta}_{j}=0$ for all solutions of this program. 
</details>

## The primal-dual witness construction 

For the Lasso, let us say that $(\widehat{\theta},\widehat{z})\in\mathbb{R}^{d}\times\mathbb{R}^{d}$ is primal-dual optimal if $\widehat{\theta}$ is a minimizer and $\widehat{z}\in\partial\Vert\widehat{\theta}\Vert_{1}.$ The proof of the theorem will be based on a constructive procedure, known as the primal-dual witness (PDW) method, which constructs such a pair. It involves the following procedure:

1. Set $\widehat{\theta}_{S^{c}}=0.$

2. Determine $(\widehat{\theta} _ {S},\widehat{z} _ {S})\in\mathbb{R}^{|S|}\times\mathbb{R}^{|S|}$ by solving the oracle subproblem


   $$
   \widehat{\theta}_{S}\in\argmin_{\theta\in\mathbb{R}^{|S|}}\left\{ \frac{1}{2n}\Vert Y-X_{S}\theta\Vert_{2}^{2}+\lambda_{n}\Vert\theta_{S}\Vert_{1}\right\}
   $$ 

   and then choosing $\widehat{z} _ {S}\in\partial\Vert\widehat{\theta} _ {S}\Vert _ {1}$ such that $\nabla f(\widehat{\theta} _ {S}) + \lambda_{n}\widehat{z} _ {S}=0,$ where $f(\theta)=\frac{1}{2n}\Vert Y-X_{S}\theta\Vert_{2}^{2}.$

3. Solve for $z_{S^{c}}\in\mathbb{R}^{d-|S|}$ via the condition $\nabla F(\widehat{\theta})+\lambda_{n}\widehat{z}=0$ and check if $\Vert\widehat{z} _ {S^{c}}\Vert _ {\infty}<1$ holds.



We say that the PDW construction succeeds if the vector $z_{S^{c}}$ constructed in Step 3 satisfies the condition $\Vert\widehat{z} _ {S^{c}}\Vert _ {\infty}<1,$ which would imply $|\nabla_{j}F(\widehat{\theta})|<\lambda_{n}$ for all $j\in S^{c}$ and hence we can use the lemma to conclude there is no false inclusion. Note that we do not actually have access to the set $S,$ so this is a purely hypothetical construction. But this is not a problem as we only need to show that the Lasso program has a unique optimal solution which can be constructed in this way. We will then use properties of this construction to show that the results of the theorem hold for the optimal solution. 

<details open>
<summary>Lemma</summary>

If the lower eigenvalue condition holds, then success of the PDW construction implies that the vector $(\widehat{\theta}_{S},0)$ is the unique optimal solution of the Lasso.

</details>

<details>
<summary>Proof</summary>

If the PDW construction succeeds, then $\widehat{\theta}=(\widehat{\theta} _ {S},0)$ is an optimal solution with associated subgradient vector $\widehat{z}\in\mathbb{R}^{d}$ satisfying $\Vert\widehat{z} _ {S^{c}}\Vert _ {\infty}<1$ and $\langle\widehat{z},\widehat{\theta}\rangle=\Vert\widehat{\theta}\Vert _ {1}.$ Suppose that $\widetilde{\theta}$ is another optimal solution. Then we must have $F(\widehat{\theta})+\lambda_{n}\Vert\widehat{\theta}\Vert_{1}=F(\widetilde{\theta})+\lambda_{n}\Vert\widetilde{\theta}\Vert_{1},$ so writing $\Vert\widehat{\theta}\Vert_{1}=\langle\widehat{z},\widehat{\theta}\rangle$  and subtracting $\langle\widehat{z},\widetilde{\theta}\rangle$ from both sides, we get


$$
F(\widehat{\theta})-\lambda_{n}\langle\widehat{z},\widetilde{\theta}-\widehat{\theta}\rangle=F(\widetilde{\theta})+\lambda_{n}(\Vert\widetilde{\theta}\Vert_{1}-\langle\widehat{z},\widetilde{\theta}\rangle).
$$

But we have $\lambda_{n}\widehat{z}=-\nabla F(\widehat{\theta}),$ which implies

$$
-F(\widetilde{\theta})+F(\widehat{\theta})+\langle\nabla F(\widehat{\theta}),\widetilde{\theta}-\widehat{\theta}\rangle=\lambda_{n}(\Vert\widetilde{\theta}\Vert_{1}-\langle\widehat{z},\widetilde{\theta}\rangle).
$$

By the convexity of $F,$ the left-hand side is non-positive, which implies that $\Vert\widetilde{\theta}\Vert_{1}\leq\langle\widehat{z},\widetilde{\theta}\rangle .$ But we also have $\langle\widehat{z},\widetilde{\theta}\rangle\leq\Vert\widehat{z}\Vert_{\infty}\Vert\widetilde{\theta}\Vert _ {1},$ so we must have $\Vert\widetilde{\theta}\Vert_{1}=\langle\widehat{z},\widetilde{\theta}\rangle .$ Since $\Vert z _ {S^{c}}\Vert _ {\infty}<1,$ this equality can only occur only if $\widetilde{\theta}_{j}=0$ for all $j\in S^{c}.$ Thus, all optimal solutions are supported only on $S,$ and hence can be obtained by solving the oracle subproblem. Given the lower eigenvalue condition, this subproblem is strictly convex, and so has a unique minimizer. 
</details>

We now need to show that the vector $\widehat{z} _ {S^{c}}$ constructed in Step 3 always satisfies the condition $\Vert\widehat{z} _ {S^{c}}\Vert _ {\infty}<1.$ Note that since $\widehat{\theta} _ {S^{c}}=\theta _ {S^{c}}^{\ast}=0,$ the condition $\nabla F(\widehat{\theta})+\lambda_{n}\widehat{z}=0,$ or $\frac{1}{n}X^{T}(X\widehat{\theta}-Y)+\lambda_{n}\widehat{z}=0,$ can be written in block matrix form as

$$
\frac{1}{n}\left(\begin{array}{cc}
X_{S}^{T}X_{S} & X_{S}^{T}X_{S^{c}}\\
X_{S^{c}}^{T}X_{S} & X_{S^{c}}^{T}X_{S^{c}}
\end{array}\right)\left(\begin{array}{c}
\widehat{\theta}_{S}-\theta_{S}^{\ast}\\
0
\end{array}\right)-\frac{1}{n}\left(\begin{array}{c}
X_{S}^{T}\epsilon\\
X_{S^{c}}^{T}\epsilon
\end{array}\right)+\lambda_{n}\left(\begin{array}{c}
\widehat{z}_{S}\\
\widehat{z}_{S^{c}}
\end{array}\right)=\left(\begin{array}{c}
0\\
0
\end{array}\right).
$$

From the second equation above, we get

$$
\widehat{z}_{S^{c}}=-\frac{1}{\lambda_{n}n}X_{S^{c}}^{T}X_{S}(\widehat{\theta}_{S}-\theta_{S}^{\ast})+X_{S^{c}}^{T}\left(\frac{\epsilon}{\lambda_{n}n}\right).
$$

Similarly, from the first equation, we get

$$
\widehat{\theta}_{S}-\theta_{S}^{\ast}=(X_{S}^{T}X_{S})^{-1}X_{S}^{T}\epsilon-\lambda_{n}n(X_{S}^{T}X_{S})^{-1}\widehat{z}_{S}.
$$

Substituting this into the expression for $\widehat{z} _ {S^{c}}$ we had just obtained, we get

$$
\widehat{z}_{S^{c}}=\underbrace{X_{S^{c}}^{T}X_{S}(X_{S}^{T}X_{S})^{-1}\widehat{z}_{S}}_{A_{S}}+\underbrace{X_{S^{c}}^{T}[I-X_{S}(X_{S}^{T}X_{S})^{-1}X_{S}^{T}]\frac{\epsilon}{\lambda_{n}n}}_{B_{S^{c}}}.
$$

By the triangle inequality, we have $\Vert\widehat{z} _ {S^{c}}\Vert _ {\infty}\leq\Vert A _ {S}\Vert _ {\infty}+\Vert B _ {S^{c}}\Vert _ {\infty}.$ By mutual incoherence, we have $\Vert A _ {S}\Vert _ {\infty}\leq\alpha .$ By our choice of regularization parameter, we have $\Vert B_{S^{c}}\Vert_{\infty}\leq\frac{1}{2}(1-\alpha).$ Putting together the pieces, we conclude that $\Vert\widehat{z} _ {S^{c}}\Vert _ {\infty}\leq\frac{1}{2}(1+\alpha)<1.$ Finally, we note that the $\ell_{\infty}$-bound follows from writing 

$$
\widehat{\theta}_{S}-\theta_{S}^{\ast}=\left(\frac{X_{S}^{T}X_{S}}{n}\right)^{-1}X_{S}^{T}\frac{\epsilon}{n}-\lambda_{n}\left(\frac{X_{S}^{T}X_{S}}{n}\right)^{-1}\widehat{z}_{S}
$$

and then applying the triangle inequality. 

## The case of sub-Gaussian noise

Let us now consider the special case where the noise is sub-Gaussian, where we can say something more concrete. 

<details open>
<summary>Corollary</summary>

Consider the linear model 

$$
Y=X\theta^{\ast}+\epsilon
$$

where $X\in\mathbb{R}^{n\times d}$ is a fixed design matrix, $\theta^\ast$ is $S$-sparse, and the components of the noise vector $\epsilon\in\mathbb{R}^{n}$ are zero-mean independent and identically distributed $\sigma^{2}$-sub-Gaussian variables. Assume that $X$ satisfies the lower eigenvalue and the mutual incoherence assumptions. Suppose also that $\max_{j=1,\ldots,d}\Vert X_{j}\Vert_{2}/\sqrt{n}\leq C$ and choose

$$
\lambda_{n}=\frac{2C\sigma}{1-\alpha}\left(\sqrt{\frac{2\log(d-k)}{n}}+\delta\right)
$$

for some $\delta>0,$ where $k=|S|.$ Then with probability at least $1-4e^{-\frac{n\delta^{2}}{2}},$ the optimal solution $\widehat{\theta}$ to the Lasso program is unique with its support contained within $S$ and satisfies the $\ell_{\infty}$-error bound

$$
\Vert\widehat{\theta}_{S}-\theta_{S}^{\ast}\Vert_{\infty}\leq\frac{\sigma}{\sqrt{c_{\min}}}\left(\sqrt{\frac{2\log k}{n}}+\delta\right)+\left\Vert \left(\frac{X_{S}^{T}X_{S}}{n}\right)^{-1}\right\Vert _{\infty}\lambda_{n}.
$$
</details>


<details>
<summary>Proof</summary>

By the theorem, we only need to show that the chosen $\lambda_{n}$ satisfies the bound

$$
\lambda_{n}\geq\frac{2}{1-\alpha}\left\Vert X_{S^{c}}^{T}\Pi_{S^{\perp}}\frac{\epsilon}{n}\right\Vert _{\infty}
$$

with probability at least $1-4e^{-\frac{n\delta^{2}}{2}}.$ It suffices to bound the maximum absolute value of the random variables

$$
Z_{j}=X_{j}^{T}\Pi_{S^{\perp}}\frac{\epsilon}{n}
$$

over $j \in S^c.$ Since $\Pi_{S^{\perp}}$ is an orthogonal projection matrix, we have 

$$
\Vert\Pi_{S^{\perp}}X_{j}\Vert_{2}\leq\Vert X_{j}\Vert_{2}\leq C\sqrt{n}.
$$

Therefore, each variable $Z_{j}$ is $C^{2}\sigma^{2}/n$-sub-Gaussian, giving

$$
\mathbb{P}\left[\max_{j\in S^{c}}|Z_{j}|\geq t\right]\leq2(d-k)e^{-\frac{nt^{2}}{2C^{2}\sigma^{2}}}.
$$

Plugging in our choice of $\lambda_{n},$ it can be checked that

$$
\mathbb{P}\left[\max_{j\in S^{c}}|Z_{j}|\geq\frac{(1-\alpha)\lambda_{n}}{2}\right]\leq4e^{-\frac{n\delta^{2}}{2}}.
$$

It remains to show the $\ell_{\infty}$-bound. By the theorem, we have

$$
\Vert\widehat{\theta}_{S}-\theta_{S}^{\ast}\Vert_{\infty}\leq\left\Vert \left(\frac{X_{S}^{T}X_{S}}{n}\right)^{-1}X_{S}^{T}\frac{\epsilon}{n}\right\Vert _{\infty}+\left\Vert \left(\frac{X_{S}^{T}X_{S}}{n}\right)^{-1}\right\Vert _{\infty}\lambda_{n}.
$$

We will focus on bounding the first quantity on the right. For each $i=1,\ldots,k,$ let $\widetilde{Z} _ {i}:=e _ {i}^{T}\left(\frac{1}{n}X _ {S}^{T}X _ {S}\right)^{-1}X _ {S}^{T}\frac{\epsilon}{n}.$ Since the components $\epsilon$ are i.i.d. $\sigma^{2}$-sub-Gaussian, the variable $\widetilde{Z}_{i}$ is sub-Gaussian with variance proxy

$$
\begin{aligned}
\frac{\sigma^{2}}{n^{2}}\left\Vert e_{i}^{T}\left(\frac{1}{n}X_{S}^{T}X_{S}\right)^{-1}X_{S}^{T}\right\Vert _{2}^{2}	&=\frac{\sigma^{2}}{n^{2}}e_{i}^{T}\left(\frac{1}{n}X_{S}^{T}X_{S}\right)^{-1}X_{S}^{T}X_{S}\left(\frac{1}{n}X_{S}^{T}X_{S}\right)^{-1}e_{i} \\
	&=\frac{\sigma^{2}}{n}e_{i}^{T}\left(\frac{1}{n}X_{S}^{T}X_{S}\right)^{-1}e_{i} \\
	&\leq\frac{\sigma^{2}}{n}\left\Vert \left(\frac{1}{n}X_{S}^{T}X_{S}\right)^{-1}\right\Vert _{2} \\
	&\leq\frac{\sigma^{2}}{nc_{\min}}.
\end{aligned}
$$

Consequently, for any $\delta>0,$ we have 

$$
\mathbb{P}\left[\max_{i=1,\ldots,s}|\widetilde{Z}_{i}|>\frac{\sigma}{\sqrt{c_{\min}}}\left(\sqrt{\frac{2\log k}{n}}+\delta\right)\right]\leq2e^{-\frac{n\delta^{2}}{2}}
$$

from which the claim follows.
</details>
