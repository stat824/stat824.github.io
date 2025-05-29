# The convexification principle

The biggest problem with empirical risk minimization is that the optimization problem is often not easy to solve. Note that if $\mathcal{H}$ is a set of classifiers, it is necessarily non-convex (a linear combination of two classifiers is not necessarily a classifier). Even if we consider a convex set $\mathcal{H}$ (which is thus not a set of classifiers), the problem

$$
\min_{h\in\mathcal{H}}R_{n}(h)
$$

is still not a convex optimization because $R_{n}(\cdot)$ is not convex. Consequently, we cannot guarantee that this problem is solvable in polynomial time. The question is thus the following: can we find a minimization problem that gives approximately the same solution, or one that has roughly the same statistical properties? 

## $\phi$ risk

In all subsequent discussions, it will be more practical to consider the label $Y$ to take values in $\{-1,1\}.$ The classification error thus writes

$$
R(h)=\mathbb{P}[Y\neq h(X)]=\mathbb{P}[-Yh(X)\geq0]=\mathbb{E}[\phi_{0}(-Yh(X))],
$$

where $\phi_{0}(x)=1(x\geq0).$ As was already observed, there are two sources of non-convexity. To eliminate the first, we can replace $\mathcal{H}$ with a convex set $\mathcal{F}$ of functions on $\mathcal{X}$ with real values. To eliminate the second source of non-convexity, we replace the function of loss $\phi_{0}(\cdot)=1(\cdot\geq0)$ by a convex function $\phi(\cdot)$ that is such that $1(x\geq0)\leq\phi(x).$ Such a function is called a convex surrogate of $\phi_{0}.$ We thus obtain the $\phi$ risk

$$
R_{\phi}(f)=\mathbb{E}[\phi(-Yf(X))]
$$

and the empirical $\phi$ risk

$$
R_{n,\phi}(f)=\frac{1}{n}\sum_{i=1}^{n}\phi(-Y_{i}f(X_{i})).
$$

The functions $R_{\phi}$ and $R_{n,\phi}$ are convex because $\phi$ is convex. This leads to the following procedure for classification:

1. For a convex set $\mathcal{F}$ of functions with real values, find

   $$
   \widehat{f}_{n,\phi}=\argmin_{f\in\mathcal{F}}R_{n,\phi}(f).
   $$

2. Define a classifier by

   $$
   \widehat{h}_{n,\phi}=\operatorname{sign}(\widehat{f}_{n,\phi}).
   $$


The two parameters of this procedure, $\mathcal{F}$ and $\phi,$ need to be specified.

### Choice of $\phi$

Usually, we assume that $\phi(0)=1$ and $\lim_{x\to-\infty}\phi(x)=0.$ The last condition allows to ensure that $\phi$ does not deviate from $\phi_{0}$ too much for large negative values. Some popular choices for $\phi$:

* $\phi(x)=(1+x)_{+}$ is the hinge loss.

* $\phi(x)=e^{x}$ is the exponential loss.

* $\phi(x)=\log_{2}(1+e^{x})$ is the logit loss.

For these choices, the risk $R_{\phi}$ does not heavily penalize large values of $Yf(X)$ for a good classification. By contrast, it penalizes greatly negative values of $Yf(X).$ What is the best choice of $\phi$? The answer to this question is not really known. 

### Choice of $\mathcal{F}$

The simplest and most widespread custom is to take $\mathcal{F}$ to be the set of all linear combinations of a finite set of classifiers $\{h_{1},\ldots,h_{M}\}$ which we call base classifiers and sometimes weak learners. That is,

$$
\mathcal{F}=\left\{ f=\sum_{j=1}^{M}\theta_{j}h_{j}:\sum_{j=1}^{M}\theta_{j}=1,\,\theta_{j}\geq0\right\} .
$$

A slight modification of this definition suggests taking the coefficients in a ball of radius $\lambda>0$ in the $\ell_{1}$ space:

$$
\mathcal{F}=\left\{ f=\sum_{j=1}^{M}\theta_{j}h_{j}:\sum_{j=1}^{M}|\theta_{j}|\leq\lambda\right\} .
$$

More generally, a choice that is often put forward in theory (but with little relevance in practice) consists of considering the convex hull of some set $\mathcal{H}$ of classifiers or the associated $\ell_{1}$ balls:

$$
\mathcal{F}=\left\{ f=\sum_{j=1}^{M}\theta_{j}h_{j}:M\in\mathbb{N},\,\sum_{j=1}^{M}\theta_{j}=1,\,\theta_{j}\geq0,\,h_{j}\in\mathcal{H}\right\} ,
$$

or

$$
\mathcal{F}=\left\{ f=\sum_{j=1}^{M}\theta_{j}h_{j}:M\in\mathbb{N},\,\sum_{j=1}^{M}|\theta_{j}|\leq\lambda,\,h_{j}\in\mathcal{H}\right\} .
$$

Procedures of convexification with one of these 4 choices of $\mathcal{F}$ are called bagging and boosting. Later on, we will also cover another approach called support vector machines.