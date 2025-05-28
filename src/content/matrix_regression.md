# Low-rank matrix regression

For two matrices $A,B\in\mathbb{R}^{d_{1}\times d_{2}},$ we consider the trace inner product $\langle A,B\rangle=\operatorname{tr}(A^{T}B)=\sum_{i=1}^{d_{1}}\sum_{j=1}^{d_{2}}A_{ij}B_{ij}.$ Note that this inner product induces the Frobenius norm. In matrix regression, we consider observations $(X_{1},y_{1}),\ldots,(X_{n},y_{n})$ where $X_{i}\in\mathbb{R}^{d_{1}\times d_{2}}$ is a matrix of covariates and $y_{i}\in\mathbb{R}$ is the response. Then we want to estimate $\Theta^{\ast}\in\mathbb{R}^{d_{1}\times d_{2}}$ such that

$$
y_{i}=\langle X_{i},\Theta^{\ast}\rangle+\epsilon_{i},
$$

where $\epsilon_{i}$ is some type of noise. This general framework encompasses the following problems:

<details open>
<summary>Example: multivariate regression</summary>

In multivariate regression, we want to solve problems of the form:

$$
Y=Z\Theta^{\ast}+W
$$

where $Z\in\mathbb{R}^{n\times d}$ is the regression matrix, $W$ is a matrix of noise variables and $Y\in\mathbb{R}^{n\times T}$ is a matrix of responses. This is in fact an instance of matrix regression: we can view this problem as $T$ (univariate) linear regression problems $Y^{(j)}=Z\theta^{\ast(j)}+\epsilon^{(j)}$ where $Y^{(j)}, \theta^{\ast(j)}$ and $\epsilon^{(j)}$ are the $j$th column of $Y,$ $\Theta^{\ast}$ and $W$ respectively. In particular, an estimator for $\Theta^{\ast}$ can be obtained by concatenating the estimators for each of the $T$ problems. Letting $E_{jl}$ be an $n\times T$ mask matrix with zeros everywhere except from a one in position $jl,$ the problem can be rewritten as

$$
y_{jl}=\langle Z^{T}E_{jl},\Theta^{\ast}\rangle+W_{jl}.
$$

</details>

<details open>
<summary>Example: matrix completion</summary>

We assume that we observe a subset $\widetilde{y}$ of the entries of a matrix $\Theta^{\ast} \in \mathbb{R}^{d_1 \times d_2},$ and we want to reconstruct it. That is, we have

$$
\widetilde{y}_{i}=\Theta_{a(i),b(i)}^{\ast}+\epsilon_{i}/\sqrt{d_{1}d_{2}}
$$

where $\epsilon$ denotes some observational noise. This is a form of matrix regression. To see this, define the mask matrix $X_{i}\in\mathbb{R}^{d_{1}\times d_{2}}$ which is zero everywhere, except for observation $(a(i),b(i))$ where it takes the value $\sqrt{d_{1}d_{2}}.$ Then, working with the rescaled observation $y_{i}=\sqrt{d_{1}d_{2}}\widetilde{y}_{i},$ we have

$$
y_{i}=\langle X_{i},\Theta^{\ast}\rangle+\epsilon_{i}.
$$

</details>


## Some results about matrices

Let us begin by recalling some results in linear algebra concerning matrices.

<details open>
<summary>Useful Matrix Norms</summary>

Let $A$ be an $m\times n$ matrix with singular values $\sigma_{1}\geq\sigma_{2}\geq\cdots\geq\sigma_{r}$ where $r=\min(m,n).$

* The Frobenius norm: $\Vert A\Vert_{\text{F}}=\sqrt{\operatorname{tr}(A^{T}A)}.$

* Schatten norms: Let $\sigma=(\sigma_{1},\ldots,\sigma_{r})$ be the vector of singular values of $A.$ For any $q\in[1,\infty),$ we define

  $$
  \Vert A\Vert_{q}:=\Vert\sigma\Vert_{q}=\left(\sum_{i=1}^{r}\sigma^{q}\right)^{1/q}.
  $$

  This is called the Schatten $q$-norm of A. In particular, $q=2$ gives the Frobenius norm, $q=1$ gives the nuclear norm, and $q=\infty$ gives the $\ell^{2}$-operator norm
</details>


<details open>
<summary>Useful Matrix Inequalities</summary>

Let $A$ and $B$ be two $m\times n$ matrices with singular values $\sigma_{1}(A)\geq\sigma_{2}(A)\geq\cdots\geq\sigma_{r}(A)$ and $\sigma_{1}(B)\geq\sigma_{2}(B)\geq\cdots\geq\sigma_{r}(B),$ where $r=\min(m,n).$ Then the following inequalities hold:

* Weyl's inequality: $\max_{k}|\sigma_{k}(A)-\sigma_{k}(B)|\leq\Vert A-B\Vert_{\text{op}}.$

* Hoffman-Weilandt inequality: $\sum_{k=1}^{r}|\sigma_{k}(A)-\sigma_{k}(B)|^{2}\leq\Vert A-B\Vert_{\text{F}}^{2}.$

* Holder's inequality: $\langle A,B\rangle\leq\Vert A\Vert_{p}\Vert B\Vert_{q}$ where $p,q\in[1,\infty]$ satisfy $\frac{1}{p}+\frac{1}{q}=1.$ 

</details>

We also have the Eckart-Young theorem, which states that for any given integer $k,$ the closest matrix of rank $k$ to a given matrix $A$ in Frobenius norm is given by its truncated SVD.

<details open>
<summary>Eckart-Young Theorem</summary>

Let $A$ be a rank-$r$ matrix with singular value decomposition $A=\sum_{i=1}^{r}\sigma_{i}u_{i}v_{i}^{T}$ where $\sigma_{1}\geq\sigma_{2}\geq\cdots\geq\sigma_{r}$ are the singular values of $A.$ For any $k<r,$ let $A_{k}$ to be the truncated singular value decomposition of $A$ given by $A_{k}=\sum_{i=1}^{k}\sigma_{i}u_{i}v_{i}^{T}.$ Then $A_{k}$ is the solution to the minimization problem

$$
\min_{\operatorname{rank}(B)\leq k}\Vert A-B\Vert_{\operatorname{F}}
$$

and we have $\Vert A-A_{k}\Vert_{\operatorname{F}}^{2}=\sum_{i=k+1}^{r}\sigma_{i}^{2}.$

</details>

<details>
<summary>Proof</summary>

The identity $\Vert A-A_{k}\Vert_{\operatorname{F}}^{2}=\sum_{i=k+1}^{r}\sigma_{i}^{2}$ is easy to verify. The fact that $\Vert A-B\Vert_{\text{F}}^{2}\geq\sum_{i=k+1}^{r}\sigma_{i}^{2}$ follows from the Hoffman-Weilandt inequality. 
</details>

## Analysis of nuclear norm regularization

Returning to the problem of matrix regression, we are particularly interested in cases where we can assume that the regression matrix $\Theta^{\ast}$ is either low-rank or well approximated by a low-rank matrix. Thus, we should consider the M-estimator with the nuclear norm as a regularizer:

$$
\widehat{\Theta}\in\argmin_{\Theta\in\mathbb{R}^{m\times T}}\left\{ \frac{1}{2n}\Vert Y-\mathcal{X}_{n}(\Theta)\Vert_{2}^{2}+\lambda_{n}\Vert\Theta\Vert_{\text{nuc}}\right\}
$$

where $[\mathcal{X}_{n}(\Theta)]_{i}=\langle X_{i},\Theta\rangle .$

### Decomposability of the nuclear norm 

The first thing we need to do is show that the nuclear norm is decomposable with respect to a suitable pair of subspaces. Let $U\in\mathbb{R}^{d_{1}\times d'}$ and $V\in\mathbb{R}^{d_{2}\times d'}$ be orthonormal matrices containing respectively the left and right singular vectors of $\Theta^{\ast}.$ For a given positive integer $r\leq d'=\min(d_{1},d_{2}),$ define $\mathbb{U}^{r}$ to be the span of the first $r$ columns of $U$ and $\mathbb{V}^{r}$ to be the span of the first $r$ columns of $V.$ We can then define the two subspaces of matrices:

$$
\mathbb{M}(\mathbb{U}^{r},\mathbb{V}^{r})=\{\Theta\in\mathbb{R}^{d_{1}\times d_{2}}:\operatorname{rowspan}(\Theta)\subseteq\mathbb{V}^{r},\operatorname{colspan}(\Theta)\subseteq\mathbb{U}^{r}\},
$$

$$
\overline{\mathbb{M}}^{\perp}(\mathbb{U}^{r},\mathbb{V}^{r})=\left\{ \Theta\in\mathbb{R}^{d_{1}\times d_{2}}:\operatorname{rowspan}(\Theta)\subseteq(\mathbb{V}^{r})^{\perp},\operatorname{colspan}(\Theta)\subseteq(\mathbb{U}^{r})^{\perp}\right\} .
$$

It should be clear that any matrix in $\mathbb{M}$ has rank at most $r.$ With this choice, any pair of matrices $A\in\mathbb{M}$ and $B\in\overline{\mathbb{M}}^{\perp}$ can be represented in the form

$$
A=U\left(\begin{array}{cc}
\Gamma_{11} & 0_{r\times(d'-r)}\\
0_{(d'-r)\times r} & 0_{(d'-r)\times(d'-r)}
\end{array}\right)V^{T}\quad\text{and}\quad B=U\left(\begin{array}{cc}
0_{r\times r} & 0_{r\times(d'-r)}\\
0_{(d'-r)\times r} & \Gamma_{22}
\end{array}\right)V^{T},
$$

where $\Gamma_{11}\in\mathbb{R}^{r\times r}$ and $\Gamma_{22}\in\mathbb{R}^{(d'-r)\times(d'-r)}$ are arbitrary matrices. Since the trace inner product defines orthogonality, any matrix $\overline{A}$ in $\overline{\mathbb{M}}$ must take the form

$$
\overline{A}=U\left(\begin{array}{cc}
\Gamma_{11} & \Gamma_{12}\\
\Gamma_{21} & 0_{(d'-r)\times(d'-r)}
\end{array}\right)V^{T}
$$

where all the $\Gamma$ matrices are arbitrary. In this way, we see explicitly that $\overline{\mathbb{M}}$ is a strict superset of $\mathbb{M}$ whenever $r<d'.$ Note that $\overline{\mathbb{M}}$ is not substantially larger than $\mathbb{M}$ as this representation shows that any matrix in $\overline{\mathbb{M}}$ has rank at most $2r.$ This also gives the decomposability of the nuclear norm, since for $(A,B)\in(\mathbb{M},\overline{\mathbb{M}}^{\perp}),$ we have

$$
\begin{aligned}
\Vert A+B\Vert_{\text{nuc}} &= \left\Vert \left(\begin{array}{cc}
\Gamma_{11} & 0_{r\times(d'-r)}\\
0_{(d'-r)\times r} & 0_{(d'-r)\times(d'-r)}
\end{array}\right)+\left(\begin{array}{cc}
0_{r\times r} & 0_{r\times(d'-r)}\\
0_{(d'-r)\times r} & \Gamma_{22}
\end{array}\right)\right\Vert _{\text{nuc}} \\
	&=\left\Vert \left(\begin{array}{cc}
\Gamma_{11} & 0_{r\times(d'-r)}\\
0_{(d'-r)\times r} & 0_{(d'-r)\times(d'-r)}
\end{array}\right)\right\Vert _{\text{nuc}}+\left\Vert \left(\begin{array}{cc}
0_{r\times r} & 0_{r\times(d'-r)}\\
0_{(d'-r)\times r} & \Gamma_{22}
\end{array}\right)\right\Vert _{\text{nuc}} \\
	&=\Vert A\Vert_{\text{nuc}}+\Vert B\Vert_{\text{nuc}}
\end{aligned}
$$

where we used the fact that the nuclear norm is invariant under an orthogonal transformation. For any choice of regularization parameter $\lambda_{n}\geq2\Vert\nabla\mathcal{L}_{n}(\Theta^{\ast})\Vert_{2},$ it follows that the error matrix $\Delta=\widehat{\Theta}-\Theta^{\ast}$ satisfies $\Vert\widehat{\Theta}_{\overline{\mathbb{M}}^{\perp}}\Vert_{\text{nuc}}\leq3\Vert\widehat{\Theta}_{\overline{\mathbb{M}}}\Vert_{\text{nuc}}+4\Vert\Theta_{\mathbb{M}^{\perp}}^{\ast}\Vert_{\text{nuc}}.$

### Restricted strong convexity

For the given cost function, restricted strong convexity amounts to lower bounding the quadratic form $\frac{\Vert\mathcal{X}_{n}(\Theta)\Vert_{2}^{2}}{2n}.$ It is possible to show that the bound

$$
\frac{\Vert\mathcal{X}_{n}(\Theta)\Vert_{2}^{2}}{2n}\geq\frac{\kappa}{2}\Vert\Delta\Vert_{\text{F}}^{2}-c_{0}\frac{d_{1}+d_{2}}{n}\Vert\Delta\Vert_{\text{nuc}}^{2}\quad\text{for all }\Delta\in\mathbb{R}^{d_{1}\times d_{2}}
$$

holds with high probability, where $\kappa$ and $c_{0}$ are positive constants. We obtain the following. 

<details open>
<summary>Theorem</summary>

Assume the restricted strong convexity condition above holds with parameter $\kappa>0.$ Then on the event $\mathbb{G}(\lambda_{n})=\left\{ \left\Vert \frac{1}{n}\sum_{i=1}^{n}\epsilon_{i}X_{i}\right\Vert _{\operatorname{op}}\leq\frac{\lambda_{n}}{2}\right\} ,$ any optimal solution $\widehat{\Theta}$ to the nuclear norm regularized least squares satisfies the bound

$$
\Vert\widehat{\Theta}-\Theta^{\ast}\Vert_{\operatorname{F}}^{2}\leq\frac{72\lambda_{n}^{2}r}{\kappa^{2}}+\frac{16}{\kappa}\left(\lambda_{n}\sum_{j=r+1}^{d'}\sigma_{j}(\Theta^{\ast})+\frac{16c_{0}(d_{1}+d_{2})}{n}\left(\sum_{j=r+1}^{d'}\sigma_{j}(\Theta^{\ast})\right)^{2}\right)
$$

for any $r\in[d']$ such that $r\leq\frac{\kappa n}{256c_{0}(d_{1}+d_{2})}. $
</details>


<details>
<summary>Proof</summary>

We want to apply the general error bounds for regularized M-estimators. Let $r\in[d'].$ We have seen that the nuclear norm is decomposable over $(\mathbb{M}(\mathbb{U}^{r},\mathbb{V}^{r}),\overline{\mathbb{M}}^{\perp}(\mathbb{U}^{r},\mathbb{V}^{r})).$ For the cost function $\mathcal{L}_{n}(\Theta)=\frac{1}{2n}\Vert Y-\mathcal{X}_{n}(\Theta)\Vert_{2}^{2},$ we have $\nabla\mathcal{L}_{n}(\Theta)=\frac{1}{n}\sum_{i=1}^{n}\epsilon_{i}X_{i}$ and the dual norm of the nuclear norm is the operator norm. Since we assume that the cost function satisfies the restricted strong convexity condition with curvature $\kappa$ and tolerance $\tau_{n}^{2}=c_{0}\frac{d_{1}+d_{2}}{n},$ to apply the general bound we need to ensure that $\tau_{n}^{2}\Psi^{2}(\overline{\mathbb{M}})\leq\frac{\kappa}{128}.$ Any matrix $\Theta\in\overline{\mathbb{M}}(\mathbb{U}^{r},\mathbb{V}^{r})$ has rank at most $2r,$ so 

$$
\Psi(\overline{\mathbb{M}}(\mathbb{U}^{r},\mathbb{V}^{r}))=\sup_{\Theta\in\overline{\mathbb{M}}\backslash\{0\}}\frac{\Vert\Theta\Vert_{\text{nuc}}}{\Vert\Theta\Vert_{\text{F}}}=\sup_{\Theta\in\overline{\mathbb{M}}\backslash\{0\}}\frac{\Vert\sigma(\Theta)\Vert_{1}}{\Vert\sigma(\Theta)\Vert_{2}}=\sqrt{2r}.
$$

Therefore, whenever $r\leq\frac{\kappa n}{256c_{0}(d_{1}+d_{2})},$ we have

$$
\tau_{n}^{2}\Psi^{2}(\overline{\mathbb{M}})=2c_{0}\left(\frac{d_{1}+d_{2}}{n}\right)r\leq\frac{\kappa}{128}.
$$

With these assumptions, we can apply the general error bounds for regularized M-estimators to get $\Vert\widehat{\Theta}-\Theta^{\ast}\Vert_{\operatorname{F}}^{2}\leq\epsilon_{n}^{2}(\overline{\mathbb{M}},\mathbb{M}^{\perp}),$ where 

$$
\begin{aligned}
\epsilon_{n}^{2}(\overline{\mathbb{M}},\mathbb{M}^{\perp}) &= \frac{36\lambda_{n}^{2}\Psi^{2}(\overline{\mathbb{M}})}{\kappa^{2}}+\frac{16}{\kappa}(\lambda_{n}\Phi(\theta_{\mathbb{M}^{\perp}}^{\ast})+16\tau_{n}^{2}\Psi^{2}(\theta_{\mathbb{M}^{\perp}}^{\ast}))\\
	&=\frac{72\lambda_{n}^{2}r}{\kappa^{2}}+\frac{16}{\kappa}\left(\lambda_{n}\sum_{j=r+1}^{d'}\sigma_{j}(\Theta^{\ast})+\frac{16c_{0}(d_{1}+d_{2})}{n}\left(\sum_{j=r+1}^{d'}\sigma_{j}(\Theta^{\ast})\right)^{2}\right).
\end{aligned}
$$
</details>