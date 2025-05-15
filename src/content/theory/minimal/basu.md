# Basu's theorem

Basu's thereom tells us that a complete and sufficient statistic is independent of every ancillary statistic.

<details open>
<summary>Basu's Theorem</summary>

Let $T$ be complete and sufficient. If $A$ is ancillary, then $T \mathrel{\bot\mkern-10mu\bot} A$. 
</details>

<details>
<summary>Proof</summary>

Let $B$ be a measurable set. We want to show that $\mathbb{P} _ {\theta}(A\in B|T=t) = \mathbb{P} _ {\theta}(A\in B)$ for all $t$. Set $c=\mathbb{P} _ \theta (A\in B)$. This does not depend on $\theta$ since $A$ is ancillary. Also, set $g(t)=\mathbb{P} _ \theta (A\in B|T=t)$, which also does not depend on $\theta$ since $T$ is sufficient. Then 

$$
\mathbb{E}_{\theta}(g(T)-c)=\mathbb{E}_{\theta}\mathbb{P}_{\theta}(A\in B|T)-\mathbb{P}_{\theta}(A\in B)=0\quad\text{for all }\theta\in\Theta,
$$

so by completeness we have $g(T)=c$ almost surely. 
</details>

This gives a very short proof of the following classical result. 

<details open>
<summary>Example</summary>

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}N(\theta,1)$. Then $\overline{X} \mathrel{\bot\mkern-10mu\bot} \sum_{i=1}^{n}(X_{i}-\overline{X})^{2}$ by Basu's theorem. 
</details>
