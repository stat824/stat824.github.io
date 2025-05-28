# VC class dictionaries

Let $\mathcal{H}$ be a collection of classifiers. In empirical risk minimization, we have seen that the stochastic error satisfies

$$
R(\widehat{h}_{n}^{\operatorname{erm}})-\inf_{h\in\mathcal{H}}R(h)\leq2\sup_{h\in\mathcal{H}}|R_{n}(h)-R(h)|,
$$

so the key to obtaining oracle inequalities is to control the quantity $\sup_{h\in\mathcal{H}}|R_{n}(h)-R(h)|.$ This quantity can be written in terms of an empirical measure. Indeed, if we take $\mathcal{Y}=\mathcal{X}\times\{0,1\},$ then for any classifier $h\in\mathcal{H},$ let us define $A_{h}$ to be the measurable set in $\mathcal{Y}$ defined by

$$
A_{h}=\{(x,y):h(x)\neq y\}.
$$

This gives a bijection between $\mathcal{H}$ and a class of measurable sets in $\mathcal{Y}=\mathcal{X}\times\{0,1\},$ which we denote as $\overline{\mathcal{A}}.$ With this notation we have introduced, we can write

$$
\sup_{h\in\mathcal{H}}|R_{n}(h)-R(h)|=\sup_{A\in\overline{\mathcal{A}}}|\mu_{n}(A)-\mu(A)|.
$$

The theory we have developed allows us to give bounds on this quantity in terms of the VC dimension of $\overline{\mathcal{A}}.$ However, $\overline{\mathcal{A}}$ is not a very natural class to consider. Since a classifier $h$ can only take values in $\{0,1\},$ it is more natural to consider the VC dimension of the family $\mathcal{A}=\{\{h=1\}:h\in\mathcal{H}\}$ which is a class of subsets of $\mathcal{X}.$ It turns out that we can make this replacement without issue since the VC dimensions of these two families are actually the same. 

<details open>
<summary>Lemma</summary>

It holds that $\mathcal{S}_{\mathcal{A}}(n)=\mathcal{S}_{\overline{\mathcal{A}}}(n)$ for all $n\geq1.$ Consequently, we have $\operatorname{VC}(\mathcal{A})=\operatorname{VC}(\overline{\mathcal{A}}). $
</details>

<details>
<summary>Proof</summary>

Let $x_{1},\ldots,x_{n}\in\mathcal{X}$ and $y_{1},\ldots,y_{n}\in\{0,1\}.$ Consider

$$
\overline{\mathcal{A}}((x_{1},y_{1}),\ldots,(x_{n},y_{n}))=\{(1(h(x_{1})\neq y_{1}),\ldots,1(h(x_{n})\neq y_{n})):h\in\mathcal{H}\},
$$

$$
\mathcal{A}(x_{1},\ldots,x_{n})=\{(1(h(x_{1})=1),\ldots,1(h(x_{n})=1)):h\in\mathcal{H}\}.
$$

Applying the XOR operator $\oplus$ component wise, we have

$$
\left(\begin{array}{c}
1(h(x_{1})\neq y_{1})\\
\vdots\\
1(h(x_{n})\neq y_{n})
\end{array}\right)=\left(\begin{array}{c}
1(h(x_{1})=1)\\
\vdots\\
1(h(x_{n})=1)
\end{array}\right)\oplus\left(\begin{array}{c}
y_{1}\\
\vdots\\
y_{n}
\end{array}\right).
$$

For any fixed $v\in\{0,1\},$ $u\mapsto u\oplus v$ is a bijection, so we must have $\operatorname{card}(\overline{\mathcal{A}}((x_{1},y_{1}),\ldots,(x_{n},y_{n})))=\operatorname{card}(\mathcal{A}(x_{1},\ldots,x_{n})). $
</details>

<details open>
<summary>Definition</summary>

Let $\mathcal{H}$ be a collection of classifiers. We define the VC-dimension $\operatorname{VC}(\mathcal{H})$ of $\mathcal{H}$ to be the VC dimension of $\mathcal{A}=\{\{h=1\}:h\in\mathcal{H}\}.$ If $\operatorname{VC}(\mathcal{H})<\infty ,$ we say that $\mathcal{H}$ is a VC class. 
</details>


With this definition, we have the following oracle inequalities.

<details open>
<summary>Theorem</summary>

Let $\mathcal{H}$ be a VC class. Then we have

$$
\mathbb{E}[R(\widehat{h}_{n}^{\operatorname{erm}})]\leq\min_{h\in\mathcal{H}}R(h)+4\frac{\sqrt{2\operatorname{VC}(\mathcal{H})\log(n+1)+\log(2)}}{n}.
$$

Also, for any $\delta\in(0,1),$ with probability at least $1-\delta$ it holds that

$$
R(\widehat{h}_{n}^{\operatorname{erm}})\leq\min_{h\in\mathcal{H}}R(h)+4\sqrt{\frac{2\operatorname{VC}(\mathcal{H})\log(n+1)+\log(2)}{n}}+2\sqrt{\frac{\log(1/\delta)}{2n}}.
$$

Moreover, the classification error of $\widehat{h}_{n}^{\operatorname{erm}}$ is bounded with probability at least $1-\delta$  as

$$
|R(\widehat{h}_{n}^{\operatorname{erm}})-R_{n}(\widehat{h}_{n}^{\operatorname{erm}})|\leq2\sqrt{\frac{2\operatorname{VC}(\mathcal{H})\log(n+1)+\log(2)}{n}}+\sqrt{\frac{\log(1/\delta)}{2n}}.
$$
</details>



The final inequality provides a confidence interval for $R(\widehat{h}_{n}^{\operatorname{erm}})$.