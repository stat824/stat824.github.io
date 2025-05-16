# Empirical Bayes perspective of James-Stein estimator

Let $X_{1},\ldots,X_{n}\overset{\mathrm{i.i.d.}}{\sim}N(\theta,I_{p})$ where $\theta\in\mathbb{R}^{p}$, and consider the loss function $L(\widehat{\theta},\theta)=\Vert\widehat{\theta}-\theta\Vert^{2}$. In dimension $p \geq 3,$ the James-Stein estimator gives an example of an estimator which has strictly smaller risk than $\overline{X}$. It is defined as

$$
\widehat{\theta}_{\text{JS}}=\left(1-\frac{p-2}{n\Vert\overline{X}\Vert^{2}}\right)\overline{X}.
$$
 
This estimator can be derived from the empirical Bayes perspective. In empirical Bayes, the prior distribution depends on a parameter $\tau$ which we estimate from the data rather than as a hyperparameter. In other words, we estimate $\tau$ from the marginal likelihood

$$
m(x|\tau)=\int p(x|\theta)\pi(\theta|\tau)\,d\theta.
$$

Consider the prior $\theta|\tau^{2}\sim N(0,\tau^{2}I_{p})$. Then the Bayes estimator is

$$
\widehat{\theta}=\mathbb{E}(\theta|X_{1},\ldots,X_{n})=\frac{n}{n+\frac{1}{\tau^{2}}}\overline{X}=\left(1-\frac{1}{n}\left(\frac{1}{\frac{1}{n}+\tau^{2}}\right)\right)\overline{X}.
$$

Note that we have $X_{i}=\theta+Z_{i}$ where $Z_{i}\overset{\text{i.i.d.}}{\sim}N(0,I_{p})$, and $\theta=\tau W$ where $W\sim N(0,I_{p})$, so $X_{i}=\tau W+Z_{i}$ for $i=1,\ldots,n$. This gives

$$
\overline{X}=\tau W+\overline{Z}\sim N\left(0,\left(\tau^{2}+\frac{1}{n}\right)I_{p}\right).
$$

Therefore, 

$$
\frac{\Vert\overline{X}\Vert^{2}}{\tau^{2}+\frac{1}{n}}\sim\chi_{p}^{2}\implies\frac{\tau^{2}+\frac{1}{n}}{\Vert\overline{X}\Vert^{2}}\sim\text{inv-}\chi_{p}^{2}.
$$

Then

$$
\mathbb{E}\left(\frac{\tau^{2}+\frac{1}{n}}{\Vert\overline{X}\Vert^{2}}\right)=\frac{1}{p-2}\implies\mathbb{E}\left(\frac{p-2}{\Vert\overline{X}\Vert^{2}}\right)=\frac{1}{\tau^{2}+\frac{1}{n}},
$$

so $\frac{p-2}{\Vert\overline{X}\Vert^{2}}$ is unbiased estimator of $\frac{1}{\tau^{2}+\frac{1}{n}}$. Thus, the empirical Bayes estimator is

$$
\widehat{\theta}_{\text{JS}}=\left(1-\frac{p-2}{n\Vert\overline{X}\Vert^{2}}\right)\overline{X}.
$$

