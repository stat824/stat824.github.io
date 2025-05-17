# The problem of binary classification

Suppose we observe the tuples $(X_{1},Y_{1}),\ldots,(X_{n},Y_{n}),$ assumed to be the i.i.d realizations of a random variable $(X,Y).$ Here, $X$ is a random variable with values in a measurable space $\mathcal{X},$ and $Y\in\{0,1\}$ is a label. The problem in classification is to find the prediction of $Y$ given observed values of $X.$ The joint law of the tuple $(X,Y)$ is determined by the law of the predictor $X,$ denoted as $P_{X},$ and by the conditional probability

$$
\eta(x)=\mathbb{P}[Y=1|X=x]=\mathbb{E}[Y|X=x].
$$

A classifier is a measurable function $h:\mathcal{X}\to\{0,1\}.$ If you observe $X,$ $h(X)$ is what is used to predict $Y.$ To construct a classifier in practice, we use the data sample $\mathcal{D}=\{(X_{1},Y_{1}),\ldots,(X_{n},Y_{n})\}.$ The performance of the classifier $h$ is measured by the risk

$$
R(h)=\mathbb{P}[Y\neq h(X)].
$$

## Bayes classifier

The classifier that achieves $R^{\ast}=\min_{h}R(h)$ is called the Bayes classifier. It can be explicitly found to be

$$
h^{\ast}(x)=\begin{cases}
1 & \text{if }\eta(x)>1/2,\\
0 & \text{if }\eta(x)\leq1/2.
\end{cases}
$$

<details open>
<summary>Theorem</summary>

For any classifier $h,$

$$
\begin{aligned}
R(h)-R(h^{\ast})=\mathbb{E}\left[|2\eta(X)-1|1(h(X)\neq h^{\ast}(X))\right]=\int_{\{x:h(x)\neq h^{\ast}(x)\}}|2\eta(x)-1|\,P_{X}(dx).
\end{aligned}
$$

Consequently, the classifier $h^{\ast}$ is the Bayes classifier. Moreover, the Bayes risk satisfies

$$
R^{\ast}=\mathbb{E}[\min\{\eta(X),1-\eta(X)\}]\leq\frac{1}{2}.
$$
</details>

<details>
<summary>Proof</summary>

We have

$$
\begin{aligned}
R(h)	&=\mathbb{P}[Y\neq h(X)] \\
	&=\mathbb{E}[\mathbb{P}[Y\neq h(X)|X]] \\
	&=\mathbb{E}[\mathbb{P}[Y=1|X]1(h(X)=0)+\mathbb{P}[Y=0|X]1(h(X)=1)] \\
	&=\mathbb{E}[\eta(X)1(h(X)=0)+(1-\eta(X))1(h(X)=1)] \\
	&=\mathbb{E}[\eta(X)+(1-2\eta(X))1(h(X)=1)].
\end{aligned}
$$

Clearly this is minimized when the classifier is chosen to be $h^{\ast}.$ We have

$$
R(h)-R(h^{\ast})=\mathbb{E}[(1-2\eta(X))(1(h(X)=1)-1(h^{\ast}(X)=1))],
$$

where 

$$
\begin{aligned}
(1-2\eta(X))(1_{\{h(X)=1\}}-1_{\{h^{\ast}(X)=1\}}) &=\begin{cases}
1-2\eta(X) & \text{if }h(X)=1\text{ and }h^{\ast}(X)=0\\
2\eta(X)-1 & \text{if }h(X)=0\text{ and }h^{\ast}(X)=1\\
0 & \text{otherwise}
\end{cases} \\
	&=|2\eta(X)-1|1(h(X)\neq h^{\ast}(X)),
\end{aligned}
$$

so we have the first part of the theorem. For the second part, we note that $\eta(X)\leq1/2$ implies $\eta(X)\leq1-\eta(X)$ and similarly $\eta(X)>1/2$ implies $1-\eta(X)\leq\eta(X),$ so

$$
\begin{aligned}
R(h^{\ast})	&=\mathbb{E}[\eta(X)1(\eta(X)\leq1/2)+(1-\eta(X))1(\eta(X)>1/2)] \\
	&=\mathbb{E}[(1(\eta(X)\leq1/2)+1(\eta(X)>1/2))\min(\eta(X),1-\eta(X))] \\
	&=\mathbb{E}[\min(\eta(X),1-\eta(X))].
\end{aligned}
$$

</details>


## Parametric modeling: linear discriminant analysis

Suppose that the density of $(X|Y=k)$ is given by $p_{k}$ for $k\in\{0,1\}.$ Then if $\pi=\mathbb{P}[Y=1],$ Bayes' theorem gives

$$
\eta(x)=\frac{\pi p_{1}(x)}{\pi p_{1}(x)+(1-\pi)p_{0}(x)},
$$

and using this we find that the Bayes classifier can be written as

$$
h^{\ast}(x)=\begin{cases}
1 & \text{if }\frac{p_{1}(x)}{p_{0}(x)}>\frac{1-\pi}{\pi},\\
0 & \text{otherwise}.
\end{cases}
$$

A popular model when $\mathcal{X}=\mathbb{R}^{d}$ is to assume that the conditional distributions $(X|Y=k)$ are Gaussian with mean $\mu_{k}$ and covariance $\Sigma_{k}.$ When we have $\Sigma_{1}=\Sigma_{0}=\Sigma ,$ the Bayes classifier is given by

$$
h^{\ast}(x)=\frac{1}{2}\left[\operatorname{sign}\left(\left\langle \Sigma^{-1}(\mu_{1}-\mu_{0}),x-\frac{\mu_{1}+\mu_{0}}{2}\right\rangle +\log\left(\frac{\pi}{1-\pi}\right)\right)+1\right].
$$

In practice, we can classify the data with

$$
\widehat{h}_{\text{LDA}}(x)=\frac{1}{2}\left[\operatorname{sign}\left(\left\langle \widehat{\Sigma}^{-1}(\widehat{\mu}_{1}-\widehat{\mu}_{0}),x-\frac{\widehat{\mu}_{1}+\widehat{\mu}_{0}}{2}\right\rangle +\log\left(\frac{\widehat{\pi}_{1}}{1-\widehat{\pi}_{1}}\right)\right)+1\right],
$$

where $\widehat{\pi}_{1}$ is the empirical proportion of the label 1, $\widehat{\mu}_{k}$ is the empirical mean of the observations with label $k,$ and $\widehat{\Sigma}$ is the empirical covariance of the data. This is known as the linear discriminant analysis (LDA) estimator. The parametric modeling is powerful when the model is correct, but in many cases, we do not know the distribution of the points $X$ given the labels $Y,$ and an incorrectly specified model can lead to poor results. 

## Semiparametric modeling: logistic regression

By definition of $h^{\ast},$ we can write the Bayes classifier as $h^{\ast}(x)=2\operatorname{sign}\left(\eta(x)-1/2\right)-1.$ A classical approach is to assume a parametric model for the conditional probability $\eta(x)=\mathbb{P}[Y=1|X=x].$ The most popular model in $\mathbb{R}^{d}$ is probably the logistic model, where

$$
\eta(x)=\frac{\exp(\alpha+\langle\beta,x\rangle)}{1+\exp(\alpha+\langle\beta,x\rangle)}
$$

for some parameters $\alpha\in\mathbb{R}$ and $\beta\in\mathbb{R}^{d}.$ In this case, $\eta(x)>1/2$ if and only if $\exp(\alpha+\langle\beta,x\rangle)>1,$ so the Bayes classifier has the simple form

$$
h^{\ast}(x)=\frac{1}{2}\left[\operatorname{sign}(\alpha+\langle\beta,x\rangle)+1\right].
$$

The parameters $(\alpha,\beta)$ can be estimated by maximizing the conditional likelihood

$$
(\widehat{\alpha},\widehat{\beta})\in\argmin_{(\alpha,\beta)\in\mathbb{R}^{d+1}}\left\{ \prod_{i:Y_{i}=1}\frac{\exp(\alpha+\langle\beta,X_{i}\rangle)}{1+\exp(\alpha+\langle\beta,X_{i}\rangle)}\prod_{i:Y_{i}=0}\frac{1}{1+\exp(\alpha+\langle\beta,X_{i}\rangle)}\right\} ,
$$

giving the classifier

$$
\widehat{h}_{\text{logistic}}(x)=\frac{1}{2}\left[\operatorname{sign}(\widehat{\alpha}+\langle\widehat{\beta},x\rangle)+1\right].
$$

Note that even though both the LDA and logistic classifiers are linear classifiers (the decision boundary is a hyperplane in $\mathbb{R}^{d}$), the two procedures do not lead to the same classifier in general.