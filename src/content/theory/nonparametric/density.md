# The problem of density estimation

Let $(\varphi _ {j}) _ {j=1}^{\infty}$ be the orthonormal basis for $L^{2}([0,1])$ given by $\{ 1, \sqrt{2}\sin(2\pi j\cdot), \sqrt{2}\cos(2\pi j\cdot) : j=1,2,\ldots \}.$ Given $\alpha>0$, we define the Sobolev ball

$$
S_{\alpha}(R)=\left\{ f\in L^{2}([0,1]),\,f=\sum_{j}\theta_{j}\varphi_{j},\,f\geq0,\:\int f=1,\,\sum_{j}j^{2\alpha}\theta_{j}^{2}\leq R^{2}\right\} .
$$

The parameter $\alpha$ is called the smoothness parameter because for a function $f\in C^{\alpha}([0,1])$ with Fourier series expansion $f(x)=a_{0}+\sum_{j=1}^{\infty}\left(a_{j}\sin(2\pi jx)+b_{j}\cos(2\pi jx)\right)$, we have

$$
\Vert f^{(\alpha)}\Vert^{2}=a_{0}^{2}+\frac{1}{2}\sum_{j=1}^{\infty}(2\pi j)^{2\alpha}(a_{j}^{2}+b_{j}^{2}).
$$

Let $f_{1},\ldots,f_{n}\overset{\text{i.i.d.}}{\sim}f\in \Theta = S_{\alpha}(R)$. Then estimating $f$ is equivalent to estimating the coefficients $\theta_{j}$. Since $\theta_{j}=\int f\varphi_{j}$, by the central limit theorem, we have

$$
\frac{1}{n}\sum_{i=1}^{n}\int f_{i}\varphi_{j}\overset{d}{\approx}N\left(\theta_{j},\frac{\text{Var}(\int f\varphi_{j})}{n}\right).
$$

However, instead of considering density estimation directly, we can consider an asymptotically equivalent model known as the Gaussian sequence model. Most nonparametric models such as the white noise model and nonparametric regression are asymptotically equivalent to the Gaussian sequence model. 