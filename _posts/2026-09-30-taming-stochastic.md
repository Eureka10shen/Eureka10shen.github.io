---
title: "Taming in Stochastic Processes"
date: 2026-09-30 13:39:00 +0800
categories:
  - Mathematics
tags:
  - MCMC
  - Sampling
  - Stochastic Process
  - SDE
  - Optimization
excerpt: "Technical notes on taming methods for stochastic sampling, SDE solvers, and stochastic optimization."
mathjax: true
permalink: /blog/taming-stochastic-process/
---

*Technical notes on taming methods for stochastic sampling, SDE solvers, and stochastic optimization.*

## References

- [Roberts1996] Roberts, Gareth O., and Richard L. Tweedie. "Exponential convergence of Langevin distributions and their discrete approximations." (1996): 341-363.
- [Atchadé2006] Atchadé, Yves F. "An adaptive version for the Metropolis adjusted Langevin algorithm with a truncated drift." Methodology and Computing in Applied Probability 8.2 (2006): 235-254.
- [Brosse2019] Brosse, Nicolas, et al. "The tamed unadjusted Langevin algorithm." Stochastic Processes and their Applications 129.10 (2019): 3638-3663.
- [Hutzenthaler2012] Hutzenthaler, Martin, Arnulf Jentzen, and Peter E. Kloeden. "Strong convergence of an explicit numerical method for SDEs with nonglobally Lipschitz continuous coefficients." (2012): 1611-1641.
- [Sabanis2013] Sabanis, Sotirios. "A note on tamed Euler approximations." (2013): 1-10.
- [Wang2013] Wang, Xiaojie, and Siqing Gan. "The tamed Milstein method for commutative stochastic differential equations with non-globally Lipschitz continuous coefficients." Journal of Difference Equations and Applications 19.3 (2013): 466-490.
- [Lovas2023] Lovas, Attila, et al. "Taming neural networks with TUSLA: Nonconvex learning via adaptive stochastic gradient Langevin algorithms." SIAM Journal on Mathematics of Data Science 5.2 (2023): 323-345.
- [Lim2024] Lim, Dong-Young, and Sotirios Sabanis. "Polygonal Unadjusted Langevin Algorithms: Creating stable and efficient adaptive algorithms for neural networks." Journal of Machine Learning Research 25.53 (2024): 1-52.
- [Lim2025] Lim, Dong-Young, et al. "Langevin dynamics based algorithm e-THεO POULA for stochastic optimization problems with discontinuous stochastic gradient." Mathematics of Operations Research 50.3 (2025): 2333-2374.

---

Following my previous post on truncated ULA, I investigated taming as a broader
stabilization principle for stochastic algorithms. The same idea appears in
three related settings:

1. Langevin sampling;
2. numerical solvers for stochastic differential equations (SDEs); and
3. stochastic optimization.

In each setting, an explicit update may become unstable when its drift or
stochastic gradient grows faster than linearly. Taming modifies that term so
that a single step cannot become excessively large, while retaining the
original direction and recovering the untamed update as the step size tends to
zero.

Much of the development across these three directions is due to Sotirios
Sabanis and collaborators; several of the references above belong to this line
of work.

## 1. Taming in Langevin sampling

For a target distribution $ \pi\propto e^{-U} $, the Tamed Unadjusted Langevin
Algorithm (TULA) replaces the raw potential gradient with

$$
G_\gamma(x)
=
\frac{\nabla U(x)}
{1+\gamma\|\nabla U(x)\|}
$$

and uses the update

$$
X_{k+1}
=
X_k-\gamma G_\gamma(X_k)+\sqrt{2}\,\Delta B_k,
\qquad X_0=x
$$

The denominator controls a superlinearly growing gradient and prevents the
drift contribution from producing an excessively large proposal. The
unadjusted version gives TULA [Brosse2019]. Related truncated proposals can
also be followed by a Metropolis--Hastings accept--reject step, as in MALTA and
adaptive truncated MALA [Roberts1996; Atchadé2006].

The distinction is therefore algorithmic: TULA directly accepts the tamed
Euler proposal, whereas a Metropolis-adjusted method corrects the proposal to
preserve the target distribution exactly.

## 2. Tamed numerical schemes for SDEs

Consider the SDE

$$
dX_t
=
\mu(X_t)\,dt+\sigma(X_t)\,dW_t
$$

with step size $h$. The explicit Euler--Maruyama scheme is

$$
X_{n+1}
=
X_n+h\mu(X_n)
+\sigma(X_n)\bigl(W_{(n+1)h}-W_{nh}\bigr)
$$

When the drift grows superlinearly, the moments of this explicit scheme can
diverge even if the underlying SDE is well behaved. An implicit Euler scheme
can restore stability by evaluating the drift at the next state:

$$
X_{n+1}
=
X_n+h\mu(X_{n+1})
+\sigma(X_n)\bigl(W_{(n+1)h}-W_{nh}\bigr)
$$

However, each implicit step requires solving an equation for $X_ {n+1}$.
Hutzenthaler et al. [Hutzenthaler2012] instead proposed the explicit tamed
Euler scheme

$$
X_{n+1}
=
X_n
+\frac{h\mu(X_n)}
{1+h\|\mu(X_n)\|}
+\sigma(X_n)\bigl(W_{(n+1)h}-W_{nh}\bigr)
$$

The taming factor bounds the norm of the drift increment:

$$
\left\|
\frac{h\mu(X_n)}
{1+h\|\mu(X_n)\|}
\right\|
\le 1
$$

### 2.1 Assumptions and strong convergence

The original analysis assumes:

1. a globally one-sided Lipschitz drift,
   $ \langle x-y,\mu(x)-\mu(y)\rangle\le c\|x-y\|^2 $;
2. a drift derivative with at most polynomial growth,
   $ \|\mu'(x)\|\le c(1+\|x\|^c) $; and
3. globally Lipschitz diffusion,
   $ \|\sigma(x)-\sigma(y)\|\le c\|x-y\| $.

Under these conditions, the tamed Euler approximation has the standard strong
convergence order $1/2$. With $h=T/N$, a representative root-mean-square bound
is

$$
\left(\mathbb E\|X_T-X_N\|^2\right)^{1/2}
\le C h^{1/2}
$$

In one dimension, if the drift is continuously differentiable, the one-sided
Lipschitz condition corresponds to the upper derivative bound
$ \mu'(x)\le L $. By contrast, global Lipschitz continuity imposes the
two-sided bound $ \lvert\mu'(x)\rvert\le L $ and is therefore stronger.

Sabanis [Sabanis2013] extended the tamed Euler analysis to locally one-sided
Lipschitz drifts under additional growth conditions. Wang and Gan [Wang2013]
extended the taming principle to a Milstein scheme and obtained strong order
one for commutative-noise SDEs under their stated assumptions.

## 3. Taming in stochastic optimization

The third application is stochastic optimization for machine learning. The
starting point is stochastic gradient Langevin dynamics (SGLD):

$$
\theta_{n+1}
=
\theta_n
-\lambda H(\theta_n,X_{n+1})
+\sqrt{2\lambda\beta^{-1}}\,\xi_{n+1},
\qquad
\xi_{n+1}\sim\mathcal N(0,I_d)
$$

Here, $\lambda$ is the learning rate, $\beta$ is the inverse temperature, and
$H(\theta,x)$ is a stochastic gradient. The following methods differ primarily
in how they replace $H$ with a stable approximation $H_ {\lambda}$.

### 3.1 Global taming in TUSLA

Suppose the stochastic gradient contains a data-dependent term
$G(\theta,x)$ and a high-order regularization term
$\eta\theta\|\theta\|^{2r}$:

$$
H(\theta,x)
=
G(\theta,x)+\eta\theta\|\theta\|^{2r}
$$

TUSLA [Lovas2023] applies one global parameter-dependent taming factor to the
entire stochastic gradient:

$$
H_\lambda(\theta,x)
=
\frac{G(\theta,x)+\eta\theta\|\theta\|^{2r}}
{1+\sqrt{\lambda}\,\|\theta\|^{2r}}
$$

This construction controls superlinear growth, but the same global scaling is
applied to every coordinate.

### 3.2 Componentwise taming and boosting in THεO POULA

THεO POULA [Lim2024] instead combines componentwise gradient taming with a
boosting factor, while taming the regularization term globally:

$$
H_{\lambda,c}^{(i)}(\theta,x)
=
\underbrace{
\frac{G^{(i)}(\theta,x)}
{1+\sqrt{\lambda}\,\lvert G^{(i)}(\theta,x)\rvert}
}_{\text{taming}}
\underbrace{
\left(
1+\frac{\sqrt{\lambda}}
{\varepsilon+\lvert G^{(i)}(\theta,x)\rvert}
\right)
}_{\text{boosting}}
+
\frac{
\eta\theta^{(i)}\|\theta\|^{2r}
}{
1+\sqrt{\lambda}\,\|\theta\|^{2r}
}
$$

The taming factor limits large coordinate updates. The boosting factor
increases the effective step size when a gradient component is small, thereby
addressing vanishing gradients.

### 3.3 Separate treatment of discontinuous and stable terms

The extended method e-THεO POULA [Lim2025] decomposes the stochastic gradient
as $H=G+F$, where $G$ may be discontinuous and $F$ is the continuous stable
term. It then defines $H_ {\lambda}=G_ {\lambda}+F_ {\lambda}$ componentwise:

$$
G_\lambda^{(i)}(\theta,x)
=
\frac{G^{(i)}(\theta,x)}
{1+\sqrt{\lambda}\,\lvert G^{(i)}(\theta,x)\rvert}
\left(
1+\frac{\sqrt{\lambda}}
{\varepsilon+\lvert G^{(i)}(\theta,x)\rvert}
\right)
$$

and

$$
F_\lambda^{(i)}(\theta,x)
=
\frac{F^{(i)}(\theta,x)}
{1+\sqrt{\lambda}\,\|\theta\|^{2r}}
$$

This separation permits different regularity assumptions for the potentially
discontinuous term $G$ and the stable term $F$.

## Conclusion

Across sampling, SDE integration, and stochastic optimization, taming serves
the same basic purpose: it limits unstable explicit increments without
requiring a fully implicit update. The precise denominator depends on the
problem. TULA tames the potential gradient, tamed Euler controls the drift
norm, and the optimization methods use parameter-dependent or componentwise
scaling to manage superlinear and possibly discontinuous stochastic gradients.

This perspective also distinguishes taming from many modern deep-learning
optimizers. Taming is designed primarily to guarantee stability under
superlinear growth, whereas momentum, preconditioning, and curvature-aware
methods primarily exploit the geometry or parameter structure of the learning
problem.
