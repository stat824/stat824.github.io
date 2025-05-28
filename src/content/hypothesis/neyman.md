# Neyman-Pearson lemma

In a two-point test, we want to decide between the null hypothesis $H_{0}:X\sim P$ and the alternative hypothesis $H_{1}:X\sim Q$. The testing function is a function $\phi$ which maps the data $X$ to $\{0,1\}$. We define the Type-I error to be $P\phi:=\mathbb{E} _ {X\sim P}\phi(X)$ and the Type-II error to be $Q(1-\phi) := \mathbb{E} _ {X\sim Q}(1-\phi(X))$. The testing error is then $P\phi+Q(1-\phi)$, and the optimal testing error is $\inf_{\phi}(P\phi+Q(1-\phi))$. The Neyman-Pearson lemma tells us what the optimal testing error is and which test achieves it.  


<details open>
<summary>Definition</summary>

The total variation distance between two probability measures $P$ and $Q$ is

$$
\mathsf{TV}(P,Q)=\sup_{B}\left|P(B)-Q(B)\right|
$$

where the supremum is taken over all measurable sets $B$. 

</details>

<details open>
<summary>Lemma</summary>

If $P$ and $Q$ are absolutely continuous with respect to the Lebesgue measure, we have

$$
\begin{aligned}
\mathsf{TV}(P,Q) & =P(\{p(x)>q(x)\})-Q(\{p(x)>q(x)\}) \\ &=\frac{1}{2}\int|p-q| \\ &=1-\int\min(p,q).
\end{aligned}
$$

</details>


<details>
<summary>Proof</summary>

Let $A=\{p(x)>q(x)\}$. Then $\mathsf{TV}(P,Q)\geq P(A)-Q(A)$ by definition. For all measurable sets $B$, we have

$$
\begin{aligned}
|P(B)-Q(B)| &= \left|\int_{B}(p-q)\right| \\
	&=\left|\int_{B\cap A}(p-q)+\int_{B\cap A^{c}}(p-q)\right| \\
	&=\left|\int_{B\cap A}(p-q)-\int_{B\cap A^{c}}(q-p)\right| \\
	&\leq\max\left(\int_{B\cap A}(p-q),\int_{B\cap A^{c}}(q-p)\right) \\
	&\leq\max\left(\int_{A}(p-q),\int_{A^{c}}(q-p)\right) \\
	&=\max\left(P(A)-Q(A),Q(A^{c})-P(A^{c})\right) \\
	&=P(A)-Q(A).
\end{aligned}
$$

This proves the first equality. For the second, we note that

$$
P(A)-Q(A)=\int_{\{p>q\}}(p-q)=\int_{\{p>q\}}|p-q|,
$$

$$
Q(A^{c})-P(A^{c})=\int_{\{p\leq q\}}(q-p)=\int_{\{p\leq q\}}|p-q|,
$$

so from $P(A)-Q(A)=Q(A^{c})-P(A^{c})$ it follows that 

$$
2(P(A)-Q(A))=\int_{\{p>q\}}|p-q|+\int_{\{p\leq q\}}|p-q|=\int|p-q|
$$

which implies the second equality. For the third equality, we note that

$$
\begin{aligned}
2-2\int\min(p,q) &=\left(\int p-\int\min(p,q)\right)+\left(\int q-\int\min(p,q)\right) \\
	&=\left(\int p-\int_{A}q-\int_{A^{c}}p\right)+\left(\int q-\int_{A}q-\int_{A^{c}}p\right) \\
	&=\left(\int_{A}p-\int_{A}q\right)+\left(\int_{A^{c}}q-\int_{A^{c}}p\right) \\
	&=\int_{A}|p-q|+\int_{A^{c}}|p-q| \\
	&=\int|p-q|.
\end{aligned}
$$
</details>

<details open>
<summary>Neyman-Pearson Lemma</summary>

The optimal testing error is given by

$$
\inf_{\phi}(P\phi+Q(1-\phi))=1-\mathsf{TV}(P,Q)=\int\min(p,q)
$$

which is achieved by the likelihood ratio test $\phi(X)=1(P(X) < Q(X))$. 

</details>

<details>
<summary>Proof</summary>

For all $\phi$, we have 

$$
P\phi+Q(1-\phi) = \int p\phi+q(1-\phi)\geq\int\min(p,q),
$$

which shows that the optimal testing error is bounded below by $1-\mathsf{TV}(P,Q)=\int\min(p,q)$. For the upper bound, we have

$$
\inf_{\phi} (P\phi+Q(1-\phi)) \leq P(\{ p < q \}) + Q(\{ p \geq q \})=1-\mathsf{TV}(P,Q).
$$

</details>
