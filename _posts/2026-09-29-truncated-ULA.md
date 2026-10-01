---
title: "Ergodicity and Convergence Analysis of Truncated ULA"
date: 2026-09-29 14:49:00 +0800
categories:
  - Mathematics
tags:
  - MCMC
  - Sampling
excerpt: "Technical notes on proving ergodicity and the convergence analysis of truncated ULA."
mathjax: true
permalink: /blog/truncated-ula/
---

*Technical notes on the ergodicity and convergence of truncated ULA.*

## References

- [Brosse2019] Brosse, Nicolas, et al. "The tamed unadjusted Langevin algorithm." Stochastic Processes and their Applications 129.10 (2019): 3638-3663.
- [Hairer2011] Hairer, Martin, and Jonathan C. Mattingly. "Yet another look at Harris’ ergodic theorem for Markov chains." Seminar on Stochastic Analysis, Random Fields and Applications VI: Centro Stefano Franscini, Ascona, May 2008. Basel: Springer Basel, 2011.

---

Following my previous post, I consider tamed, or truncated, MALA for use in an
NNVMC (neural network quantum Monte Carlo) sampling algorithm. Brosse et al.
introduced the Tamed Unadjusted Langevin Algorithm (TULA) in [Brosse2019] to
sample Boltzmann distributions with superlinear potentials.

The TULA iteration for sampling the target distribution $ \pi \propto e^{-U} $
is

$$
X_{k+1} = X_k-\gamma G_\gamma(X_k) + \sqrt2\,\Delta B_k, \quad X_0 = x
$$

where $ G_ {\gamma}(x)=\frac{\nabla U(x)}{1+\gamma\|\nabla U(x)\|} $ denotes the
tamed gradient of the potential $ U $.

To study the convergence of TULA to the target distribution $ \pi $, we compare
it with the ideal continuous-time Langevin process

$$
dY_t = -\nabla U(Y_t)\,dt + \sqrt2\,dB_t, \quad Y_0 = x
$$

The total error can then be decomposed into two terms:

$$
d\!\left(\mathcal L(X_n),\pi\right)
\le
\underbrace{d\!\left(\mathcal L(X_n),\mathcal L(Y_{n\gamma})\right)}
_{\text{from TULA to }Y_t}
+
\underbrace{d\!\left(\mathcal L(Y_{n\gamma}),\pi\right)}
_{Y_t\text{ not mixed in}}
$$

## 1. From TULA to the continuous Langevin process

We first construct a continuous-time interpolation of the discrete TULA
iteration. For $ t \in [k\gamma, (k+1)\gamma] $, define

$$
\bar X_t
=
X_k-(t-k\gamma)G_\gamma(X_k)
+\sqrt2\bigl(B_t-B_{k\gamma}\bigr)
$$

By construction, $ \bar X_ {k\gamma}=X_ {k} $ and
$\bar X_ {(k+1)\gamma}=X_ {k+1} $. On each interval, the interpolation satisfies

$$
d\bar X_t = -G_\gamma(\bar X_{k\gamma})\,dt + \sqrt2\,dB_t 
$$

Relative to the Langevin process, the drift deviation is

$$
r_t = G_\gamma(\bar X_{k\gamma})-\nabla U(\bar X_t) 
= \underbrace{G_\gamma(X_k)-\nabla U(X_k)}_{a_k : \text{Taming error}}
+ \underbrace{\nabla U(X_k)-\nabla U(\bar X_t)}_{b_t : \text{Discretization error}}
$$

Its squared norm satisfies

$$
\|r_t\|^2 = \|a_k+b_t\|^2\le 2\|a_k\|^2+2\|b_t\|^2
$$

### 1.1 Taming error

The taming error satisfies

$$
\|a_k\|^2
= \| G_\gamma(x)-\nabla U(x) \|^2
= - \| \frac{\gamma\|\nabla U(x)\|}{1+\gamma\|\nabla U(x)\|}\nabla U(x)\|^2 
\le \gamma^2\|\nabla U(x)\|^4 
$$

Assume that the fourth moment of the potential gradient is uniformly bounded:
$ \sup_{k\gamma\le T}\mathbb E\|\nabla U(X_ {k})\|^4\le M $. It follows that
$ \mathbb E\|a_ {k}\|^2 \le M\gamma^2 $, and hence

$$
\mathbb E\int_{k\gamma}^{(k+1)\gamma}\|a_k\|^2\,dt \le M\gamma^3
$$

### 1.2 Discretization error

Next, assume that the potential gradient is Lipschitz continuous:
$ \|\nabla U(x)-\nabla U(y)\|\le L\|x-y\| $. Then

$$
\mathbb E\|b_t\|^2 \le L^2\mathbb E\|\bar X_t-X_k\|^2
$$

Writing $ s=t-k\gamma\in[0,\gamma] $, we obtain

$$
\bar X_t-X_k = -sG_\gamma(X_k)+\sqrt2(B_t-B_{k\gamma})
$$

In a $d$-dimensional state space, the corresponding second moment is

$$
\mathbb E\|\bar X_t-X_k\|^2 = s^2\mathbb E\|G_\gamma(X_k)\|^2 + 2ds
$$

Therefore, $ \mathbb E\|b_ {t}\|^2 \le Cs $, which gives

$$
\mathbb E\int_{k\gamma}^{(k+1)\gamma}\|b_t\|^2\,dt
\le C\int_0^\gamma s\,ds
=\frac C2\gamma^2
$$

### 1.3 Total approximation error

Combining the taming and discretization errors yields

$$
\mathbb E\int_{k\gamma}^{(k+1)\gamma}\|r_t\|^2\,dt
\le 2M\gamma^3+C\gamma^2
\le C'\gamma^2
$$

Over a total time horizon $ T = N\gamma$, summing over all time steps gives

$$
\mathbb E\int_0^T\|r_t\|^2\,dt
=\sum_{k=0}^{N-1}\mathbb E\int_{k\gamma}^{(k+1)\gamma}\|r_t\|^2\,dt 
\le NC'\gamma^2
=C'T\gamma
$$

Girsanov's theorem then gives the following relative-entropy bound:

$$
\mathrm{KL}(\mathsf Q\|\mathsf P)
=\frac14\mathbb E_{\mathsf Q} \int_0^T\|r_t\|^2\,dt 
\le \frac{CT}{4}\gamma
$$

By the data-processing inequality for relative entropy,

$$
\mathrm{KL}\!\left(\mathcal L(\bar X_T)\|
\mathcal L(Y_T)\right)
\le \mathrm{KL}(\mathsf Q\|\mathsf P) 
\le \frac{CT}{4}\gamma
$$

Finally, applying Pinsker's inequality,
$ d_ {\mathrm{TV}}(\mu,\nu) \le \sqrt{\mathrm{KL}(\mu\|\nu) / 2} $, yields

$$
d_{\mathrm{TV}}\!\left(\mathcal L(X_N),\mathcal L(Y_T)\right)
\le \sqrt{\frac{CT}{8}}\,\sqrt\gamma
\to 0
$$

## 2. From the Langevin process to the target distribution

We now turn to the ideal continuous-time Langevin process

$$
dY_t=-\nabla U(Y_t)\,dt+\sqrt{2}\,dB_t,
\qquad Y_0=x,
$$

with target density $\pi(x)\propto e^{-U(x)}$.

The goal is to show that the distribution of $Y_ {T}$ approaches $\pi$ as $T$
increases. This does not mean that $Y_ {T}$ settles at a fixed position:
convergence concerns the distribution rather than individual sample paths, and
the process continues to move even as its distribution approaches equilibrium.

### 2.1 Invariance of $\pi$

First, observe that

$$
\nabla\pi=-\pi\nabla U,
$$

and therefore the probability flow at density $\pi$ vanishes:

$$
J_\pi=-\pi\nabla U-\nabla\pi=0.
$$

Under the required regularity and non-explosion conditions, the vanishing flow
implies invariance: if $Y_ {0}\sim\pi$, then $Y_ {t}\sim\pi$ for every $t\ge0$.

Invariance alone, however, does not show that a process starting from a fixed
point converges to $\pi$. We must also establish that the process forgets its
initial condition.

This requires answering two questions:

- Does the process have a sufficiently strong tendency to return after moving
  far from the origin?
- Within a bounded region, do transition distributions from different starting
  points share a common probability component?

### 2.2 Control of excursions with a Lyapunov function

Following [Brosse2019], we address the first question by choosing

$$
V(x)=\exp\!\left(a\sqrt{1+\|x\|^2}\right),
\quad a>0
$$

Because this function grows with the distance from the origin, a large value
indicates that the process is far from the central region.

Applying the infinitesimal generator of the Langevin process to $V$ gives

$$
\mathcal AV=-\nabla U\cdot\nabla V+\Delta V
$$

This quantity describes the instantaneous expected rate of change of
$V(Y_ {t})$.

Under assumptions H1–H2, Proposition 1 of [Brosse2019] establishes a bound of
the form

$$
\mathcal AV(x)\le-\lambda V(x)+b,
\quad \lambda>0,\quad b<\infty
$$

The role of H2 is to ensure that, far from the origin, the inward drift is
strong enough to dominate the outward contribution of the noise.

Let $ m(t)=\mathbb E_ {x}[V(Y_ {t})] $. The generator bound then gives

$$
m'(t)\le-\lambda m(t)+b
$$

Solving this differential inequality yields

$$
\mathbb E_x[V(Y_t)]
\le e^{-\lambda t}V(x)
+\frac b\lambda(1-e^{-\lambda t})
$$

Thus, the contribution of the initial condition decays, while the expected
value of $V(Y_ {t})$ remains controlled. This estimate does not imply that every
trajectory moves inward at every step; occasional outward excursions remain
possible.

### 2.3 A common probability component

To address the second question, define the transition kernel

$$
P_\tau(x,A)=\Pr(Y_\tau\in A\mid Y_0=x)
$$

On a compact region $K$, we seek a probability measure $\nu$ and a constant
$\varepsilon>0$ such that

$$
P_\tau(x,A)\ge\varepsilon\nu(A),
\quad x\in K
$$

for every measurable set $A$. This inequality is the **minorization
condition**.

It states that all transition distributions starting in $K$ contain the same
probability component $\varepsilon\nu$.

This condition can be understood through the transition density
$p_ {\tau}(x,y)$. For the nondegenerate diffusion considered here, standard
diffusion results provide the required local positivity and regularity. If
$p_ {\tau}$ is continuous and strictly positive on $K\times D$, where $D$ is a
fixed closed ball, then

$$
m_\tau=\min_{x\in K,\;y\in D}p_\tau(x,y)>0
$$

Taking $\nu$ to be the uniform distribution on $D$ then gives

$$
P_\tau(x,A)
\ge m_\tau\,\operatorname{Vol}(A\cap D)
=\varepsilon\nu(A)
$$

where $\varepsilon=m_ {\tau}\operatorname{Vol}(D)$.

The restriction $x\in K$ is essential because a uniform positive lower bound
generally cannot hold over every starting point in an unbounded state space.

### 2.4 Combining return and overlap with Harris’ theorem

Consider the process sampled every $\tau$ units of time. The Lyapunov estimate
becomes

$$
P_\tau V\le qV+B,
\qquad
q=e^{-\lambda\tau}<1,\quad
B=\frac b\lambda(1-q)
$$

We then choose a sufficiently large level set

$$
K=\{x:V(x)\le R\},
\quad R>\frac{2B}{1-q}
$$

and establish the minorization condition on this set.

The drift and minorization estimates are the two conditions required by a
convenient version of Harris’ theorem [Hairer2011]. Together, they imply
geometric convergence of the sampled chain and, consequently, exponential
convergence in continuous time:

$$
d_{\mathrm{TV}}\!\left(P_T(x,\cdot),\pi\right)
\le CV(x)e^{-cT}
$$

The two conditions play complementary roles. The drift condition controls
excursions, whereas minorization supplies a common probability component after
the process returns. Neither condition alone is sufficient. Because $\pi$ is
already known to be invariant, it is the unique equilibrium identified by the
theorem.

## Conclusion

Combining this mixing estimate with the finite-time TULA approximation bound
from Section 1 gives

$$
d_{\mathrm{TV}}\!\left(\mathcal L(X_N),\pi\right)
\le
\underbrace{C_{T,x}\sqrt{\gamma}}_{\text{Discretization and taming error}}
+
\underbrace{CV(x)e^{-cT}}_{\text{Mixing error}},
\qquad N\gamma=T
$$

The first term measures how accurately TULA follows the ideal process over a
finite time horizon. The second measures how close the ideal process is to
equilibrium.

To reduce the total error below a chosen tolerance, we can first choose $T$
large enough to control the mixing error and then choose $\gamma=T/N$ small
enough to control the approximation error.

This order matters because $C_ {T,x}$ may grow with $T$. Therefore, the bound
does not by itself imply that running TULA longer with a fixed step size removes
all error. At a fixed step size, TULA generally has its own invariant
distribution $\pi_ {\gamma}$, which differs from $\pi$. The paper develops
sharper long-time bounds beyond this basic finite-time comparison.

