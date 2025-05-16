# Pairwise incoherence and restricted isometry

If we can show that $X$ satisfies the restricted nullspace property with respect to the support of the sparsest solution $\theta^{\ast}$ to $Y=X\theta ,$ then solving the basis pursuit linear program recovers the sparsest solution $\theta^{\ast}.$ One way to show that the restricted nullspace property holds is by bounding the pairwise incoherence parameter of the design matrix, given by

$$
\delta_{PW}(X)=\max_{j,k=1,\ldots,d}\left|\frac{\langle X_{j},X_{k}\rangle}{n}-1_{\{j=k\}}\right|.
$$

<details open>
<summary>Theorem</summary>

If $\delta_{PW}(X)\leq\frac{1}{3s},$ then the restricted nullspace property holds for all subsets $S \subset [d]$ with $|S| \leq s.$
</details>

See homework for proof of the above. A more sophisticated version of the this result can be stated in terms of a related quantity. 

<details open>
<summary>Definition</summary>

For $s\in\{1,2,\ldots,d\},$ we say that $X\in\mathbb{R}^{n\times d}$ satisfies the restricted isometry property (RIP) of order $s$ with constant $\delta_{s}(X)>0$ if

$$
\left\Vert \frac{X_{S}^{T}X_{S}}{n}-I_{S}\right\Vert _{2}\leq\delta_{s}(X)
$$

for all subsets $S$ of size at most $s.$ 
</details>

Let us try to understand the RIP property a little more.

* For $s=1,$ the property becomes $\left|\frac{X_{i}^{T}X_{i}}{n}-1\right|\leq\delta_{1}\implies\frac{\Vert X_{i}\Vert^{2}}{n}\in[1-\delta_{1},1+\delta_{1}],$ so the columns of $X / \sqrt{n}$ are all almost unit vectors. 

* For $s=2,$ if we assume that the columns of $X/\sqrt{n}$ are unit vectors, then

  $$
  \frac{X_{[j,k]}^{T}X_{[j,k]}}{n}-I_{[j,k]}=\left(\begin{array}{cc}
  \frac{\Vert X_{j}\Vert^{2}}{n}-1 & \frac{\langle X_{j},X_{k}\rangle}{n}\\
  \frac{\langle X_{j},X_{k}\rangle}{n} & \frac{\Vert X_{k}\Vert^{2}}{n}-1
  \end{array}\right)=\left(\begin{array}{cc}
  0 & \frac{\langle X_{j},X_{k}\rangle}{n}\\
  \frac{\langle X_{j},X_{k}\rangle}{n} & 0
  \end{array}\right).
  $$  

  The operator norm of this matrix is $\left|\frac{\langle X_{j},X_{k}\rangle}{n}\right|.$ Hence, we can set

  $$
  \delta_{2}=\max_{j\neq k}\left|\frac{\langle X_{j},X_{k}\rangle}{n}\right|
  $$

  which is the pairwise incoherence parameter. 



More generally, we can show that for any matrix $X\in\mathbb{R}^{n\times d}$ and sparsity level $s\in\{1,\ldots,d\},$ 

$$
\delta_{PW}(X)\leq\delta_{s}(X)\leq s\delta_{PW}(X)
$$

and neither bound can be improved. 

<details open>
<summary>Proposition</summary>

If $\delta_{2s}(X)<1/3,$ then the restricted nullspace property holds for any subset $S \subset [d]$ with $|S|\leq s.$
</details>

<details>
<summary>Proof</summary>

Assume that $\delta_{2s}(X)<1/3.$ Let $\theta\in\operatorname{null}(X)\backslash\{0\}.$ To show that $\theta\not\in\mathbb{C}(S)$ for any subset $S\subset[d]$ with $|S|\leq s,$ it suffices to show that $\Vert\theta_{S^{c}}\Vert>\Vert\theta_{S}\Vert$ when $S$ is chosen to be the index set corresponding to the $s$ largest entries of $\theta.$ For any subset $A\subset[d],$ let $\theta_{A}\in\mathbb{R}^{|A|}$ be the sub-vector of elements indexed by $A.$ Also, define $\widetilde{\theta}_{A}\in\mathbb{R}^{d}$ by 

$$
(\widetilde{\theta}_{A})_{j}=\begin{cases}
\theta_{j} & \text{if }j\in A,\\
0 & \text{otherwise}.
\end{cases}
$$

Let us write $S^{c}=\bigcup_{j\geq1}S_{j}$ where $S_{1}$ is the subset of indices given by the $s$ largest values of $S^{c},$ $S_{2}$ is the subset of indices given by the $s$ largest values of $S^{c}\backslash S_{1},$ and so on. We can write

$$
\theta=\sum_{j=0}^{k}\widetilde{\theta}_{S_{j}}
$$

where we set $S_{0}=S.$ By the RIP property, we have

$$
\Vert\theta_{S}\Vert_{2}^{2}-\frac{1}{n}\left\Vert X_{S}\theta_{S}\right\Vert _{2}^{2}\leq\left|\left\langle \left(\frac{X_{S}^{T}X_{S}}{n}-I_{S}\right)\theta_{S},\theta_{S}\right\rangle \right|\leq\delta_{2s}\Vert\theta_{S}\Vert_{2}^{2}.
$$

Since $\Vert\theta _ {S}\Vert_{2}^{2}=\Vert\widetilde{\theta} _ {S}\Vert_{2}^{2}$ and $\Vert X _ {S}\theta_{S}\Vert _ {2}^{2}=\Vert X\widetilde{\theta} _ {S}\Vert_{2}^{2},$ it follows that

$$
\Vert\widetilde{\theta}_{S}\Vert_{2}^{2}-\frac{1}{n}\Vert X\widetilde{\theta}_{S}\Vert_{2}^{2}\leq\delta_{2s}\Vert\widetilde{\theta}_{S}\Vert_{2}^{2},
$$

which gives 

$$
\Vert\widetilde{\theta}_{S}\Vert_{2}^{2}\leq\frac{1}{1-\delta_{2s}}\left\Vert \frac{1}{\sqrt{n}}X\widetilde{\theta}_{S}\right\Vert _{2}^{2}.
$$

Since $\theta\in\operatorname{null}(X),$ we have $X\widetilde{\theta} _ {S}=-\sum_{j=1}^{k}X\widetilde{\theta} _ {S_{j}},$ so 

$$
\begin{aligned}
\Vert\widetilde{\theta}_{S}\Vert_{2}^{2} &\leq \frac{1}{1-\delta_{2s}}\left\langle \frac{1}{\sqrt{n}}X\widetilde{\theta}_{S},\frac{1}{\sqrt{n}}\sum_{j=1}^{k}-X\widetilde{\theta}_{S_{j}}\right\rangle \\
	&\leq\frac{1}{1-\delta_{2s}}\left|\left\langle \frac{1}{\sqrt{n}}X\widetilde{\theta}_{S},\frac{1}{\sqrt{n}}\sum_{j=1}^{k}X\widetilde{\theta}_{S_{j}}\right\rangle \right| \\
	&=\frac{1}{1-\delta_{2s}}\left|\frac{1}{n}\sum_{j=1}^{k}\widetilde{\theta}_{S}^{T}X^{T}X\widetilde{\theta}_{S_{j}}\right| \\
	&=\frac{1}{1-\delta_{2s}}\left|\frac{1}{n}\sum_{j=1}^{k}\widetilde{\theta}_{S}^{T}\left(X^{T}X-nI_{d}\right)\widetilde{\theta}_{S_{j}}\right|.
\end{aligned}
$$

Since $\left\Vert \frac{1}{n}X _ {S _ {0}\cup S_{j}}^{T}X _ {S _ {0}\cup S _ {j}}-I _ {2s}\right\Vert _ {2}\leq\delta _ {2s}$ by the RIP property, it follows that 

$$
\left|\frac{1}{n}\sum_{j=1}^{k}\widetilde{\theta}_{S}^{T}\left(X^{T}X-nI_{d}\right)\widetilde{\theta}_{S_{j}}\right|\leq\delta_{2s}\Vert\widetilde{\theta}_{S}\Vert\sum_{k=1}^{k}\Vert\widetilde{\theta}_{S_{j}}\Vert,
$$

giving 

$$
\Vert\widetilde{\theta}_{S}\Vert_{2}\leq\frac{\delta_{2s}}{1-\delta_{2s}}\sum_{j=1}^{k}\Vert\widetilde{\theta}_{S_{j}}\Vert.
$$

By construction of $S_{j},$ we have $\Vert\widetilde{\theta} _ {S _ {j}}\Vert _ {\infty}\leq\frac{1}{s}\Vert\widetilde{\theta} _ {S _ {j-1}}\Vert _ {1},$ so 

$$
\Vert\widetilde{\theta}_{S_{j}}\Vert_{2}^{2}=\sum_{j\in S_{j}}\theta_{j}^{2}\leq\Vert\widetilde{\theta}_{S_{j}}\Vert_{\infty}\Vert\widetilde{\theta}_{S_{j}}\Vert_{1}\leq\Vert\widetilde{\theta}_{S_{j}}\Vert_{\infty}\Vert\widetilde{\theta}_{S_{j-1}}\Vert_{1}\leq\frac{1}{s}\Vert\widetilde{\theta}_{S_{j-1}}\Vert_{1}^{2},
$$

giving $\Vert\widetilde{\theta} _ {S_{j}}\Vert _ {2} \leq \frac{1}{\sqrt{s}}\Vert \widetilde{\theta} _ {S _ {j-1}}\Vert _ {1}.$ Thus, 

$$
\Vert\widetilde{\theta}_{S}\Vert_{1}\leq\sqrt{s}\Vert\widetilde{\theta}_{S}\Vert_{2}\leq\frac{\delta_{2s}}{1-\delta_{2s}}\left(\Vert\widetilde{\theta}_{S}\Vert_{1}+\sum_{j=1}^{k-1}\Vert\widetilde{\theta}_{S_{j}}\Vert_{1}\right)\leq\frac{\delta_{2s}}{1-\delta_{2s}}\left(\Vert\widetilde{\theta}_{S}\Vert_{1}+\Vert\widetilde{\theta}_{S^{c}}\Vert_{1}\right).
$$


Finally, if $\delta_{2s}<1/3,$ then $\delta_{2s}/(1-\delta_{2s})<1/2,$ so 

$$
\Vert\widetilde{\theta}_{S}\Vert_{1}<\frac{1}{2}\left(\Vert\widetilde{\theta}_{S}\Vert_{1}+\Vert\widetilde{\theta}_{S^{c}}\Vert_{1}\right)\implies\Vert\widetilde{\theta}_{S}\Vert_{1}<\Vert\widetilde{\theta}_{S^{c}}\Vert_{1}.
$$

This shows that $\theta\not\in\mathbb{C}(S).$
</details>
