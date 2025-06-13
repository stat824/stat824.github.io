# PCA for spiked covariance model

In principal component analysis (PCA), the goal is to find one or more directions onto which the data can be projected without losing much of its properties. There are several reasons for doing this, for example data visualization and clustering (clustering is a hard computational problem and it is therefore preferable to carry it out in lower dimensions). To see how this assumption translates into the structure of the covariance matrix $\Sigma,$ assume that $X_{1},\ldots,X_{n}$ are Gaussian random variables of the form $X_{i}=v^{T}Y_{i}v+Z_{i},$ where $v$ is a fixed vector, $Y_{1},\ldots,Y_{n}\overset{\text{i.i.d.}}{\sim}N(0,I_{d}),$ and $Z_{1},\ldots,Z_{n}\overset{\text{i,i.d.}}{\sim}N(0,\sigma^{2}I_{d})$ are independent of the $Y_{i}$'s. The covariance matrix of $X$ generated as such is given by

$$
\Sigma=\mathbb{E}[XX^{T}]=vv^{T}+\sigma^{2}I_{d}.
$$

If $\sigma$ is small enough, we can hope to recover the direction $v.$ This is called the spiked covariance model. By a simple rescaling, it is equivalent to the following. 

<details open>
<summary>Definition</summary>

A covariance matrix $\Sigma\in\mathbb{R}^{d\times d}$ is said to satisfy the spiked covariance model if it is of the form

$$
\Sigma=\theta vv^{T}+I_{d},
$$

where $\theta>0$ and $v\in\mathcal{S}^{d-1}.$ The vector $v$ is called the spike.
</details>



Under the spiked covariance model, $v$ is the eigenvector of the matrix $\Sigma$ that is associated to its largest eigenvalue $1+\theta .$ We will refer to this vector simply as largest eigenvector. To estimate it, a natural candidate is the largest eigenvector $\widehat{v}$ of $\widehat{\Sigma},$ where $\widehat{\Sigma}$ is the empirical covariance matrix. There is a caveat: by symmetry, if $u$ is an eigenvector of a symmetric matrix, then $-u$ is also an eigenvector associated to the same eigenvalue. Therefore, we may only estimate $v$ up to a sign flip. To overcome this limitation, it is often useful to describe proximity between two vectors $u$ and $v$ in terms of the principal angle between their linear span. 


<details open>
<summary>Definition</summary>

For two unit vectors $u$ and $v,$ the principal angle between their linear spans is defined as

$$
\angle(u,v)=\arccos(|u^{T}v|).
$$
</details>

The following result bounds the sine of the principal angle between eigenspaces. 

<details open>
<summary>Davis-Kahan sin(θ) theorem</summary>

Let $A,$ $B$ be two $d\times d$ positive semidefinite matrices. Let $(\lambda_{1},u_{1}),\ldots,(\lambda_{d},u_{d})$ and $(\mu_{1},v_{1}),\ldots,(\mu_{d},v_{d})$ denote the pairs of eigenvalues and unit eigenvectors of $A$ and $B,$ ordered in non-increasing order of the eigenvalues. Then

$$
\sin(\angle(u_{1},v_{1}))\leq\frac{2}{\max(\lambda_{1}-\lambda_{2},\mu_{1}-\mu_{2})}\Vert A-B\Vert_{\operatorname{op}}.
$$

Moreover, 

$$
\min_{\epsilon\in\{\pm1\}}\Vert\epsilon u_{1}-v_{1}\Vert_{2}^{2}\leq2\sin^{2}(\angle(u_{1},v_{1})).
$$
</details>

<details>
<summary>Proof</summary>

Note that $u_{1}^{T}Au_{1}=\lambda_{1}.$ For any $x\in\mathcal{S}^{d-1},$ it holds

$$
\begin{aligned}
x^{T}Ax	&=\sum_{j=1}^{d}\lambda_{j}(u_{j}^{T}x)^{2} \\
	&\leq\lambda_{1}(u_{1}^{T}x)^{2}+\lambda_{2}(1-(u_{1}^{T}x)^{2}) \\
	&=\lambda_{1}\cos^{2}(\angle(u_{1},x))+\lambda_{2}\sin^{2}(\angle(u_{1},x)).
\end{aligned}
$$

Taking $x=v_{1},$ we get

$$
\begin{aligned}
u_{1}^{T}Au_{1}-v_{1}^{T}Av_{1}	&\geq\lambda_{1}-\lambda_{1}\cos^{2}(\angle(u_{1},x))-\lambda_{2}\sin^{2}(\angle(u_{1},x)) \\
	&=(\lambda_{1}-\lambda_{2})\sin^{2}(\angle(u_{1},x)).
\end{aligned}
$$

On the other hand, 

$$
\begin{aligned}
u_{1}^{T}Au_{1}-v_{1}^{T}Av_{1}	&=u_{1}^{T}Bu_{1}-v_{1}^{T}Av_{1}+u_{1}^{T}(A-B)u_{1} \\
	&\leq v_{1}^{T}Bv_{1}-v_{1}^{T}Av_{1}+u_{1}^{T}(A-B)u_{1} \\
	&=\langle A-B,u_{1}u_{1}^{T}-v_{1}v_{1}^{T}\rangle \\
	&\leq\Vert A-B\Vert_{\text{op}}\Vert u_{1}u_{1}^{T}-v_{1}v_{1}^{T}\Vert_{\text{nuc}} \\
	&\leq\sqrt{2}\Vert A-B\Vert_{\text{op}}\Vert u_{1}u_{1}^{T}-v_{1}v_{1}^{T}\Vert_{\text{F}}
\end{aligned}
$$

where in the last inequality we used the fact that $\text{rank}(u_{1}u_{1}^{T}-v_{1}v_{1}^{T})\leq2.$ Then we have

$$
\Vert u_{1}u_{1}^{T}-v_{1}v_{1}^{T}\Vert_{\text{F}}^{2}=2-2(u_{1}^{T}v_{1})^{2}=2\sin^{2}(\angle(u_{1},v_{1})).
$$

So it follows that 

$$
(\lambda_{1}-\lambda_{2})\sin^{2}(\angle(u_{1},v_{1}))\leq2\Vert A-B\Vert_{\text{op}}\sin(\angle(u_{1},v_{1})).
$$

Note that we can replace $\lambda_{1}-\lambda_{2}$ with $\mu_{1}-\mu_{2}$ since the result is completely symmetric in $A$ and $B,$ so this shows the first bound. The second bound follows from $\min_{\epsilon\in\{\pm1\}}\Vert\epsilon u_{1}-v_{1}\Vert_{2}^{2}\leq2-2|u_{1}^{T}v_{1}|\leq2-2(u_{1}^{T}v_{1})^{2}=2\sin^{2}(\angle(u_{1},x)).$

</details>


Using the low-dimensional bound for $\Vert\widehat{\Sigma}-\Sigma\Vert_{\operatorname{op}}$ we showed previously, we get the following corollary of the Davis-Kahan $\sin(\theta)$ theorem.

<details open>
<summary>Corollary</summary>

Let $Y\in\mathbb{R}^{d}$ be a zero-mean random vector such that $\mathbb{E}[YY^{T}]=I_{d},$ and $Y\sim\operatorname{subG}_{d}(1).$ Let $X_{1},\ldots,X_{n}$ be $n$ independent copies of the sub-Gaussian random vector $X=\Sigma^{1/2}Y.$ Then $\mathbb{E}[X]=0,$ $\mathbb{E}[XX^{T}]=\Sigma ,$ and $X\sim\operatorname{subG}_{d}(\Vert\Sigma\Vert_{\operatorname{op}}).$ Assume further that the covariance matrix satisfies the spiked covariance model $\Sigma=\theta vv^{T}+I_{d}.$ Then the largest eigenvector $\widehat{v}$ of the empirical covariance matrix satisfies

$$
\min_{\epsilon\in\{\pm1\}}\Vert\epsilon\widehat{v}-v\Vert_{2}\lesssim\frac{1+\theta}{\theta}\left(\sqrt{\frac{d+\log(1/\delta)}{n}}\lor\frac{d+\log(1/\delta)}{n}\right)
$$

with probability at least $1-\delta . $
</details>


This result justifies the use of the empirical covariance matrix as a replacement for the true covariance matrix when performing PCA, but only in the low-dimensional regime where $d\leq n.$ 