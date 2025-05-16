# Maximum over a convex polytope

A convex polytope is a compact set $P\subset\mathbb{R}^{d}$ such that there exists a finite set of points $\mathcal{V}(P)$ with $P=\operatorname{conv}(\mathcal{V}(P)).$ The elements of $\mathcal{V}(P)$ are called the vertices or extreme points of $P.$ For example, the unit ball of $\mathbb{R}^{d}$ in the $\ell_{1}$-norm is a convex polytope with $2d$-vertices. Let $X\in\mathbb{R}^{d}$ be a random vector and consider the (infinite) family of random variables $\mathcal{F}=\{\theta^{T}X:\theta\in P\}$ where $P$ is a polytope with $N$ vertices. The family $\mathcal{F}$ is infinite, but the maximum over $\mathcal{F}$ can be reduced to a finite maximum using the following lemma: 

<details open>
<summary>Lemma</summary>

Let $c\in\mathbb{R}^{d}.$ Then for any convex polytope $P\subset\mathbb{R}^{d}$, 

$$
\max_{x\in P}c^{T}x=\max_{x\in\mathcal{V}(P)}c^{T}x.
$$
</details>

<details>
<summary>Proof</summary>

Let $v_{1},\ldots,v_{n}$ denote the vertices of $P.$ For any $x\in P$, we have $x=\sum_{i=1}^{n}\lambda_{i}v_{i}=\lambda^{T}x$ for some $\lambda=(\lambda_{1},\ldots,\lambda_{n})^T$ satisfying $\lambda_{1},\ldots,\lambda_{n}\geq0$ and $\sum_{i=1}^{n}\lambda_{i}=1.$ Hence, 

$$
c^{T}x=\sum_{i=1}^{N}\lambda_{i}c^{T}v_{i}\leq\sum_{i=1}^{N}\lambda_{i}\left(\max_{1\leq i\leq N}c^{T}v_{i}\right)=\max_{1\leq i\leq N}c^{T}v_{i}.
$$

Thus, 

$$
\max_{1\leq i\leq N}c^{T}v_{i}\leq\max_{x\in P}c^{T}x\leq\max_{1\leq i\leq N}c^{T}v_{i}
$$

which means that the two quantities are equal.
</details>


This gives us the following result.

<details open>
<summary>Theorem</summary>

Let $P$ be a convex polytope with $N$ vertices. If $X\in\mathbb{R}^{d}$ is a random vector such that $v^{T}X\sim\operatorname{subG}(\sigma^{2})$ for all $v\in\mathcal{V}(P),$ then 

$$
\mathbb{E}\left[\max_{\theta\in P}\theta^{T}X\right]\leq\sigma\sqrt{2\log N}\quad\text{and}\quad\mathbb{E}\left[\max_{\theta\in P}|\theta^{T}X|\right]\leq\sigma\sqrt{2\log(2N)}.
$$

Moreover, for any $t>0,$ 

$$
\mathbb{P}\left[\max_{\theta\in P}\theta^{T}X>t\right]\leq Ne^{-\frac{t^{2}}{2\sigma^{2}}}\quad\text{and}\quad\mathbb{P}\left[\max_{\theta\in P}|\theta^{T}X|>t\right]\leq2Ne^{-\frac{t^{2}}{2\sigma^{2}}}.
$$
</details>


