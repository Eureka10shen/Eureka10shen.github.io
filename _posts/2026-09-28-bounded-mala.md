---
title: "From Minorization to a Strong Law for Metropolis–Hastings"
date: 2026-09-28 17:09:00 +0800
categories:
  - Mathematics
tags:
  - MCMC
  - Sampling
excerpt: "Technical notes on proving convergence of empirical averages for bounded Metropolis–Hastings samplers."
mathjax: true
permalink: /blog/bounded-mh-sampler/
---

*Technical notes on proving convergence of empirical averages for bounded Metropolis–Hastings samplers.*

## References

- [Roberts1996] Roberts, Gareth O., and Richard L. Tweedie. "Exponential convergence of Langevin distributions and their discrete approximations." (1996): 341-363. 
- [Atchadé2006] Atchadé, Yves F. "An adaptive version for the Metropolis adjusted Langevin algorithm with a truncated drift." Methodology and Computing in applied Probability 8.2 (2006): 235-254. 
- [Andrieu2006] Andrieu, Christophe, and Éric Moulines. "On the ergodicity properties of some adaptive MCMC algorithms." (2006): 1462-1505. 

---

I have been studying tamed, or truncated, MALA for use in a quantum Monte Carlo sampling algorithm. Roberts and Tweedie introduced this idea in [Roberts1996] under the name MALTA (Metropolis-Adjusted Langevin Truncated Algorithm). The ergodicity and convergence analysis in [Atchadé2006] then motivated me to work through a simplified proof.

These notes establish a strong law of large numbers for bounded observables of a fixed-parameter Metropolis–Hastings sampler with bounded drift:

$$
\frac1N\sum_{n=0}^{N-1}f(X_n) \xrightarrow{\mathrm{a.s.}}\pi(f), \quad \pi(f)=\int_S f(x)\pi(x)\,dx
$$

This result is one notion of sampling convergence: it states that empirical averages converge almost surely to the corresponding expectation under the target distribution.

## Setting and assumptions

Let $S=[-L,L]$, where $L>0$, and let $\pi$ be a normalized, continuous, strictly positive density on $S$. The proposal uses a fixed step size $h>0$ and a bounded measurable drift $b$, with $\lvert b(x)\rvert\leq D$:

$$
Y_{n+1}=X_n+\frac h2b(X_n)+\sqrt h\,\xi_{n+1}, \quad \xi_{n+1}\sim N(0,1)
$$

Here, $q(y\mid x)$ denotes the unconstrained Gaussian proposal density on the real line. Any proposal outside $S$ is rejected. A proposal inside $S$ is accepted according to the Metropolis–Hastings probability; if it is rejected, then $X_{n+1}=X_{n}$. Let $P$ denote the complete transition kernel, including this rejection mechanism. Detailed balance implies that $\pi P=\pi$. Finally, assume that the observable $f$ is measurable and bounded, with $\lvert f(x)\rvert\leq F$.

## 1. Decomposing the deviation

To motivate the main argument, consider the hypothetical, stronger situation in which a bounded function $u(x)$ satisfies the pathwise identity

$$
f(X_n) - \pi(f) = u(X_n) - u(X_{n+1})
$$

Summing this identity would make the deviation telescope:

$$
\frac{1}{N} \sum_{n=0}^{N-1} [f(X_n) - \pi(f)]
= \frac{u(X_0) - u(X_N)}{N}
$$

The identity above is stronger than what we need. Instead, we seek the corresponding representation in conditional expectation:

$$
f(x)-\pi(f) = u(x)-\mathbb{E}[u(X_{n+1})\mid X_n=x]
$$

Writing $Pu(x)=\mathbb{E}[u(X_{n+1})\mid X_{n}=x]$, we obtain the discrete Poisson equation

$$
u - Pu = f - \pi(f)
$$

The function $u(x)$ can be interpreted as the expected cumulative future deviation, including the current step. Accordingly,

$$
u(x)
= [f(x)-\pi(f)] + Pu(x)
$$

where $Pu(x)$ represents the expected remaining cumulative deviation after one transition.

Define the one-step martingale difference by $D_{n+1} = u(X_{n+1}) - Pu(X_{n})$. The empirical deviation then decomposes as

$$
\frac{1}{N} \sum_{n=0}^{N-1} [f(X_n) - \pi(f)]
= \frac{u(X_0) - u(X_{N})}{N} + \frac{1}{N} \sum_{n=0}^{N-1} D_{n+1}
$$

If $u(x)$ is bounded, the telescoping term converges immediately to zero. The proof therefore reduces to two questions:

- How can we construct a bounded solution $u(x)$?
- How can we prove that the martingale term converges to zero?

## 2. Constructing a bounded solution $u(x)$

Denote the expected deviation at each step by $P^k f(x) = \mathbb{E}[f(X_{k})\mid X_{0}=x]$, and define

$$
u(x) = \sum_{k=0}^{\infty} \left[ P^k f(x) - \pi(f) \right]
$$

Pointwise convergence of $P^kf(x)$ to $\pi(f)$ is not enough to guarantee convergence of this series. We need a summable bound on the deviations that holds uniformly over $x$. Specifically, we will establish

$$
\lvert P^kf(x)-\pi(f)\rvert
\leq 2F(1-\varepsilon)^k
$$

This estimate guarantees that the series defining $u(x)$ converges absolutely and uniformly.

### 2.1 A uniform minorization condition

Because $\pi$ is continuous and strictly positive on the compact state space, there exist constants satisfying $0 < m \leq \pi(x) \leq M < \infty$.

For any two states in the state space, boundedness of the drift gives

$$
\left\lvert y - x - \frac{h}{2}b(x) \right\rvert
\leq \left\lvert y - x \right\rvert + \left\lvert \frac{h}{2}b(x) \right\rvert \leq 2L + \frac{h}{2}D
$$

The Gaussian proposal density therefore has the uniform lower bound

$$
q(y\mid x)
\geq \frac1{\sqrt{2\pi h}} \exp\!\left[-\frac{(2L+hD/2)^2}{2h}\right] =:q_{\min}>0
$$

After applying the Metropolis–Hastings acceptance rule, the accepted-move density satisfies

$$
q(y\mid x)\alpha(x,y)
=\min\left\{ q(y\mid x), \frac{\pi(y)}{\pi(x)}q(x\mid y) \right\} \geq q_{\min}\frac mM=:c>0
$$

Consequently, for every initial state $x$ and every measurable set $A\subseteq S$, we have $P(x,A) \geq c\lvert A\rvert$.

Let $\nu(A) = \lvert A\rvert / 2L$ denote the uniform distribution on $[-L, L]$. Then $P(x,A)\geq 2Lc\,\nu(A) =: \varepsilon \nu(A)$. Taking $A=S$ shows that $0<\varepsilon\leq1$. If $\varepsilon=1$, every transition regenerates from $\nu$ and the conclusion is immediate. We may therefore consider the nontrivial case $0<\varepsilon<1$. This is a uniform minorization condition.

It allows us to decompose the full Metropolis–Hastings transition kernel as

$$
P(x,\cdot)
=\varepsilon\nu(\cdot)+(1-\varepsilon)Q(x,\cdot)
$$

where $Q(x,\cdot)= \frac{P(x,\cdot)-\varepsilon\nu(\cdot)}{1-\varepsilon}$.

Here, $Q$ is a residual transition kernel; it is not the original proposal kernel $q$.

### 2.2 Coupling and geometric convergence

> Consider two chains. The first starts from an arbitrary state, $X_{0} = x$. The second starts in stationarity, $Y_{0} \sim \pi$, so that $\forall n, \, Y_{n} \sim \pi$.
>
> At each transition, draw a fresh Bernoulli variable with success probability $\varepsilon$, independently of the past, and use the same outcome for both chains. On success, draw a common value $Z\sim\nu$ and set
>
> $$
> X_{n+1}
> =Y_{n+1}=Z
> $$
>
> On failure, update the chains using their respective residual kernels. After the chains meet, couple all subsequent residual updates synchronously so that they remain together.
>
> This construction preserves the transition kernel $P$ for each chain. Since $Y_{0}\sim\pi$ and $\pi P=\pi$, we have $Y_{n}\sim\pi$ for every $n$. Therefore,
>
> $$
> \Pr(X_n\neq Y_n)
> \leq(1-\varepsilon)^n
> $$

The coupling yields the required geometric convergence of $P^k f(x)$:

$$
\lvert P^k f(x)-\pi(f)\rvert
=\left\lvert\mathbb E[f(X_k)-f(Y_k)]\right\rvert
\leq 2F \Pr(X_k\neq Y_k)
\leq 2F (1-\varepsilon)^k
$$

It follows that $u(x)$ is bounded:

$$
\lvert u(x)\rvert \leq
\sum_{k=0}^{\infty} 2F (1-\varepsilon)^k =\frac{2F}{\varepsilon}
$$

At the same time, $u(x)$ satisfies the Poisson equation by cancellation:

$$
u - Pu
= (\bar{f} + P\bar{f} + P^2\bar{f} + \cdots) - (P\bar{f} + P^2\bar{f} + \cdots) = \bar{f} = f - \pi(f)
$$

## 3. Convergence of the martingale term

It remains to prove that the second term in the decomposition converges to zero. This is an instance of the martingale strong law of large numbers (MSLLN, 鞅大数定律). Let $\mathcal F_{n}=\sigma(X_{0},\ldots,X_{n})$ and define $M_{N}:=\sum_{j=1}^{N}D_j$.

Suppose that $\lvert u\rvert\leq B$. Then $\lvert Pu\rvert\leq B$, and hence $\lvert D_{n+1}\rvert\leq2B$.

By construction, $\mathbb E[D_{n+1}\mid\mathcal F_{n}]=0$.

For $i<j$, the random variable $D_{i}$ is $\mathcal F_{j-1}$-measurable, so the martingale differences are orthogonal:

$$
\mathbb E[D_iD_j]
= \mathbb E\!\left[D_i\mathbb E[D_j\mid\mathcal F_{j-1}]\right]=0
$$

Therefore,

$$
\mathbb E[M_N^2]
= \sum_{j=1}^{N}\mathbb E[D_j^2] \leq4B^2N
$$

Chebyshev’s inequality now gives

$$
\Pr\!
\left(\left\lvert\frac{M_N}{N}\right\rvert>\eta\right) \leq\frac{4B^2}{\eta^2N}
$$

Thus $M_{N}/N\to0$ both in mean square and in probability. To strengthen this conclusion to almost sure convergence, consider the square subsequence.

Along the subsequence $N=j^2$, for every fixed $\eta>0$,

$$
\sum_{j=1}^{\infty}
\Pr\!\left(\left\lvert\frac{M_{j^2}}{j^2}\right\rvert>\eta\right) \leq \frac{4B^2}{\eta^2} \sum_{j=1}^{\infty}\frac1{j^2} <\infty
$$

By the first Borel–Cantelli lemma, these exceedances occur only finitely often almost surely. Applying the argument to $\eta=1/r$, $r=1,2,\ldots$, yields

$$
\frac{M_{j^2}}{j^2}
\xrightarrow{\mathrm{a.s.}}0
$$

We then fill the gaps between consecutive square indices. For $j^2\leq N<(j+1)^2$, bounded increments give

$$
\lvert M_N-M_{j^2}\rvert
\leq2B(2j+1)
$$

Hence,

$$
\left\lvert\frac{M_N}{N}\right\rvert
\leq \frac{\lvert M_{j^2}\rvert}{j^2} +\frac{2B(2j+1)}{j^2} \xrightarrow{\mathrm{a.s.}}0
$$

Combining this result with the bound

$$
\left\lvert\frac{u(X_0)-u(X_N)}N\right\rvert
\leq\frac{2B}{N}
$$

the Poisson decomposition gives the desired strong law:

$$
\boxed{ \frac1N\sum_{n=0}^{N-1}f(X_n) \xrightarrow{\mathrm{a.s.}}\pi(f) }
$$

---

## 4. An alternative direct proof

Inspired by the conditional-expectation approach in [Atchadé2006], we can also give a direct proof for the same fixed-kernel, bounded setting. This argument does not invoke a general mixingale theorem.

Let $g=f-\pi(f)$ and choose $A:=2F$, so that $\lvert g\rvert\le A$. The coupling argument above gives

$$
\lvert P^kg(x)\rvert\le 2F(1-\varepsilon)^k=C\rho^k, \quad C=2F,\quad \rho=1-\varepsilon\in(0,1)
$$

uniformly over $x$.

Let $\mathcal F_{i}=\sigma(X_{0},\ldots,X_{i})$. By the Markov property, for $j>i$,

$$
\mathbb E[g(X_j)\mid\mathcal F_i] =P^{j-i}g(X_i)
$$

and therefore

$$
\left\lvert\mathbb E[g(X_j)\mid\mathcal F_i]\right\rvert \le C\rho^{j-i}
$$

Because $g(X_{i})$ is $\mathcal F_{i}$-measurable,

$$
\left\lvert\mathbb E[g(X_i)g(X_j)]\right\rvert
=\left\lvert\mathbb E\!\left[ g(X_i)\mathbb E[g(X_j)\mid\mathcal F_i] \right]\right\rvert
\le AC\rho^{j-i}
$$

Importantly, this bound does not require the chain to start in stationarity.

Define $S_{N}=\sum_{n=0}^{N-1}g(X_{n})$. Expanding the square and applying the covariance bound gives

$$
\mathbb E[S_N^2] \le NA^2+2AC\sum_{0\le i<j<N}\rho^{j-i} \le N\left(A^2+\frac{2AC\rho}{1-\rho}\right) =:KN
$$

Therefore,

$$
\mathbb E\!\left[\left(\frac{S_N}{N}\right)^2\right] \le\frac KN \to 0
$$

Thus $S_{N}/N\to0$ in mean square and, consequently, in probability. To obtain almost sure convergence, apply Chebyshev’s inequality along the square subsequence. For every $\eta>0$,

$$
\sum_{j=1}^{\infty} \Pr\!\left(\frac{\lvert S_{j^2}\rvert}{j^2}>\eta\right) \le \frac K{\eta^2}\sum_{j=1}^{\infty}\frac1{j^2} <\infty
$$

Applying the Borel–Cantelli lemma for $\eta=1/m$, $m=1,2,\ldots$, yields

$$
\frac{S_{j^2}}{j^2} \xrightarrow{\mathrm{a.s.}} 0
$$

Finally, for $j^2\le N<(j+1)^2$, boundedness of $g$ gives

$$
\frac{\lvert S_N\rvert}{N} \le \frac{\lvert S_{j^2}\rvert}{j^2} +\frac{A(2j+1)}{j^2} \xrightarrow{\mathrm{a.s.}} 0
$$

Hence, the alternative argument reaches the same conclusion:

$$
\boxed{ \frac1N\sum_{n=0}^{N-1}f(X_n) \xrightarrow{\mathrm{a.s.}} \pi(f) }
$$

## Conclusion

On a compact state space, positivity of the target density and boundedness of the drift yield a uniform minorization condition for the Metropolis–Hastings kernel. Coupling then gives geometric convergence, which provides a bounded solution to the Poisson equation. The resulting martingale decomposition proves the strong law for every bounded observable. Alternatively, the same coupling estimate directly controls the covariance sum and leads to the same almost sure convergence result.
