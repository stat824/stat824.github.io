# Pitman estimator

The Pitman estimator is the explicit formula for the MREE in the special case where the loss function is $\rho(t)=t^{2}$ and the pilot estimator is $\delta_{0}(X)=X_{n}.$ Recall that we have $\delta(X) = X _ {n} - \mathbb{E} _ {0}(X_{n}|Y).$ Let 

$$
Z=\left(\begin{array}{c}
Y\\
X_{n}
\end{array}\right)=\left(\begin{array}{c}
X_{1}-X_{n}\\
\vdots\\
X_{n-1}-X_{n}\\
X_{n}
\end{array}\right).
$$

Then $X_{1}=Z_{1}+Z_{n},\ldots,X_{n-1}=Z_{n-1}+Z_{n}, X_{n}=Z_{n},$ so 

$$
\frac{\partial X}{\partial Z}=\left(\begin{array}{cc}
I_{n-1} & 1_{n-1} \\
0 & 1
\end{array}\right),
$$

and we have

$$
\begin{aligned}
P_{Z,0}(z_{1},\ldots,z_{n}) &=P_{X,0}(x_{1},\ldots,x_{n})\left|\frac{\partial X}{\partial Z}\right| \\
	&=P_{X,0}(x_{1},\ldots,x_{n}) \\
	&=\prod_{i=1}^{n}f(x_{i}) \\
	&=f(y_{1}+x_{n})\cdots f(y_{n-1}+x_{n})f(x_{n}).
\end{aligned}
$$

Then

$$
\mathbb{E}_{0}(X_{n}|Y)=\frac{\int tf(Y_{1}+t)\cdots f(Y_{n-1}+t)f(t)\,dt}{\int f(Y_{1}+t)\cdots f(Y_{n-1}+t)f(t)\,dt}.
$$

Using $\delta(X) = X _ {n} - \mathbb{E} _ {0}(X_{n}|Y)$, we have

$$
\begin{aligned}
\delta(X) &=\frac{\int(X_{n}-t)f(Y_{1}+t)\cdots f(Y_{n-1}+t)f(t)\,dt}{\int f(Y_{1}+t)\cdots f(Y_{n-1}+t)f(t)\,dt} \\
	&=\frac{\int uf(X_{1}-u)\cdots f(X_{n}-u)\,du}{\int f(X_{1}-u)\cdots f(X_{n}-u)\,du}.
\end{aligned}
$$

<details open>
<summary>Definition</summary>

The formula

$$
\delta(X)=\frac{\int u\prod_{i=1}^{n}f(X_{i}-u)\,du}{\int\prod_{i=1}^{n}f(X_{i}-u)\,du}
$$

is called the Pitman estimator. 
</details>

<details open>
<summary>Example</summary>

Let $X_{1},\ldots,X_{n}\overset{\text{i.i.d.}}{\sim}\text{Unif}(\theta-\frac{b}{2},\theta+\frac{b}{2})$. Then the density is $P_{\theta}(x)=b^{-1}1_{\{\theta-\frac{b}{2}<x<\theta+\frac{b}{2}\}}$. Then

$$
\begin{aligned}
\prod_{i=1}^{n} f(X_{i} - u) &= \prod_{i=1}^{n} b^{-1} 1_{\{u-\frac{b}{2} < X_{i} < u+\frac{b}{2}\}} \\
	&=b^{-n}1_{\{u-\frac{b}{2} < X_{(1)}\}}1_{\{X_{(n)} < u+\frac{b}{2}\}} \\
	&=b^{-n}1_{\{X_{(n)} - \frac{b}{2} < u < X_{(1)} + \frac{b}{2}\}}.
\end{aligned}
$$

Therefore, the MREE is

$$
\delta(X) = \frac{\int_{X_{(n)}-\frac{b}{2}}^{X_{(1)}+\frac{b}{2}}u\,du}{\int_{X_{(n)}-\frac{b}{2}}^{X_{(1)}+\frac{b}{2}}\,du}=\frac{1}{2}\frac{(X_{(1)}+\frac{b}{2})^{2}-(X_{(n)}-\frac{b}{2})^{2}}{(X_{(1)}+\frac{b}{2})-(X_{(n)}-\frac{b}{2})}=\frac{X_{(1)}+X_{(n)}}{2}.
$$
</details>