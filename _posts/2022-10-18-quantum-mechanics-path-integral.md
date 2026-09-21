---
title: "Quantum Mechanics -Path Integral"
date: 2022-10-18 16:45:00 +0800
categories:
  - quantum-mechanics
excerpt: "A derivation of the quantum-mechanical propagator and path-integral formulation from time evolution in position and phase space."
mathjax: true
original_url: "https://www.cnblogs.com/Eureka10shen/articles/16803174.html"
permalink: /blog/quantum-mechanics-path-integral/
---

> This article was migrated from [Eureka10shen on 博客园]({{ page.original_url }}). The original publication date was 2022-10-18.

reference :  
QM - 路径积分 (Path Integral) PT. 1 - 基本构架, https://zhuanlan.zhihu.com/p/275827978  
Lecture Slide - Path Integral, 张其安, Advanced QM Au22, BUAA  

---

## classical mechanics revisited
Lagrangian mechanics -- configuration space  
the dynamics of the system is controled by the _Lagrangian_ $L(q(t),\dot{q}(t),t)$  
the _action_ of the system reads  

$$

S[q(t)] = \int_{t_1}^{t_2} L(q(t),\dot{q}(t),t)\text{d}t

$$

real trajectory under classical mechanics satisfies the _least action principle_  

$$

\delta S[q(t)] = 0

$$

$$

\begin{align*}
\delta S
&= \int_{t_1}^{t_2} \text{d}t \left(\frac{\partial L}{\partial\dot{q}_i}\delta\dot{q}_i + \frac{\partial L}{\partial q_i}\delta q_i\right) \\
&= \int_{t_1}^{t_2} \text{d}t \left[\frac{\text{d}}{\text{d}t}\left(\frac{\partial L}{\partial\dot{q}_i}\delta q_i\right) - \left(\frac{\text{d}}{\text{d}t}\frac{\partial L}{\partial\dot{q}_i}\right)\delta q_i + \frac{\partial L}{\partial q_i}\delta q_i\right] \\
&= \left.\frac{\partial L}{\partial\dot{q}_i}\delta q_i\right|_{t_1}^{t_2} + \int_{t_1}^{t_2} \text{d}t \left(\frac{\partial L}{\partial q_i} - \frac{\text{d}}{\text{d}t}\frac{\partial L}{\partial\dot{q}_i}\right)\delta q_i \\
&= 0 + \int_{t_1}^{t_2} \text{d}t \left(\frac{\partial L}{\partial q_i} - \frac{\text{d}}{\text{d}t}\frac{\partial L}{\partial\dot{q}_i}\right)\delta q_i 
\end{align*}

$$

where in the 3rd to 4th line we used $\delta q_ {i}(t_ {1}) = \delta q_ {i}(t_ {2}) = 0$  
we have the _Euler-Lagrange equation_  

$$

\frac{\text{d}}{\text{d}t}\frac{\partial L}{\partial\dot{q}_i} - \frac{\partial L}{\partial q_i} = 0

$$

---

## time evolution
the fundamental question in QM : how does the state of a particle evolve with time ?  
define the _time evolution operator_ $U(t-t_ {0})$ as  

$$

U(t-t_0)|\psi(t_0)\rangle = |\psi(t)\rangle

$$

under Schordinger picture, we have  

$$

i\hbar\frac{\text{d}|\psi(t)\rangle}{\text{d}t} = H|\psi(t)\rangle

$$

$$

\frac{\text{d}}{\text{d}t}U(t-t_0)|\psi(t_0)\rangle = -i\frac{H}{\hbar}U(t-t_0)|\psi(t_0)\rangle

$$

$$

\frac{\text{d}}{\text{d}t}U(t-t_0) = -i\frac{H}{\hbar}U(t-t_0)

$$

$$

\text{d}\ln U(t-t_0) = -i\frac{H}{\hbar}\text{d}t

$$

$$

U(t-t_0) = C e^{-i\frac{H}{\hbar}t}

$$

when $t=t_ {0}$, no time evolution occurs, $U=I$, so  

$$

U(t-t_0) = e^{-i\frac{H}{\hbar}(t-t_0)}

$$

under position representation, time evolution reads  

$$

\begin{align*}
\psi(r,t)
&= \langle r|U(t,t_0)|\psi(t_0)\rangle \\
&= \int \langle r|U(t,t_0)|r_0\rangle\langle r_0|\psi(t_0)\rangle \text{d}r_0 \\
&= \int K(r,t;r_0,t_0)\psi(r_0,t_0)\text{d}r_0
\end{align*}

$$

where $K(r,t;r_ {0},t_ {0})$ is the _propagator_  

$$

K(r,t;r_0,t_0) = \langle r|U(t,t_0)|r_0\rangle

$$

split time interval into parts as $t_ {0}\leq t_ {n}\leq t=t_ {N}$, $n\in[N]$, we have  

$$

\begin{align*}
K(r,t;r_0,t_0)
&= \langle r|U(t,t_0)|r_0\rangle \\
&= \langle r|U(t,t_1)U(t_1,t_0)|r_0\rangle \\
&= \int \langle r|U(t,t_1)|r_1\rangle\langle r_1|U(t_1,t_0)|r_0\rangle\text{d}r_1 \\
&= \int \langle r|U(t,t_2)|r_2\rangle\langle r_2|U(t_2,t_1)|r_1\rangle\langle r_1|U(t_1,t_0)|r_0\rangle\text{d}r_1\text{d}r_2 \\
&= \int K(r,t;r_2,t_2)K(r_2,t_2;r_1,t_1)K(r_1,t_1;r_0,t_0) \text{d}r_1\text{d}r_2 \\
\end{align*}

$$

extrapolation to the infinite split, the propagator reads  

$$

K(r,t;r_0,t_0) = \int \left[\prod_{n=1}^N \mathcal{K}(r_n,t_n;r_{n-1},t_{n-1})\right] \text{d}r_1...\text{d}r_{N-1}

$$

where $\mathcal{K}(r_ {n},t_ {n};r_ {n-1},t_ {n-1})$ is called _short time kernel_  

---

## path integral
denote $\Delta t_ {n} = t_ {n}-t_ {n-1}$, $\Delta r_ {n} = r_ {n}-r_ {n-1}$ the quasi-propagator reads  

$$

\mathcal{K}(r_n,t_n;r_{n-1},t_{n-1}) = \langle r_n|U(t_n,t_{n-1})|r_{n-1}\rangle = \langle r_n|e^{-i\frac{H}{\hbar}\Delta t_n}|r_{n-1}\rangle

$$

substitute the Hamiltonian  

$$

e^{-i\frac{H}{\hbar}\Delta t_n} = e^{-\frac{i}{\hbar}\left[\frac{p^2}{2m}+V(R,t_n)\right]\Delta t_n} \overset{\Delta t\rightarrow0}{=} e^{-\frac{i}{\hbar}V(R,t_n)\Delta t_n}e^{-\frac{i}{\hbar}\frac{p^2}{2m}\Delta t_n}

$$

$\spadesuit$ phase space  
in phase space the short time kernel reads  

$$

\begin{align*}
\mathcal{K}(r_n,t_n;r_{n-1},t_{n-1})
&= \langle r_n|e^{-\frac{i}{\hbar}V(R,t_n)\Delta t_n}e^{-\frac{i}{\hbar}\frac{p^2}{2m}\Delta t_n}|r_{n-1}\rangle \\
&= e^{-\frac{i}{\hbar}V(r_n,t_n)\Delta t_n}\langle r_n|e^{-\frac{i}{\hbar}\frac{p^2}{2m}\Delta t_n}|r_{n-1}\rangle \\
&= \int e^{-\frac{i}{\hbar}V(r_n,t_n)\Delta t_n}\langle r_n|p_n\rangle\langle p_n|e^{-\frac{i}{\hbar}\frac{p^2}{2m}\Delta t_n}|r_{n-1}\rangle \text{d}p_n \\
&= \int e^{-\frac{i}{\hbar}V(r_n,t_n)\Delta t_n}\langle r_n|p_n\rangle e^{-\frac{i}{\hbar}\frac{p_n^2}{2m}\Delta t_n}\langle p_n|r_{n-1}\rangle \text{d}p_n \\
&= \frac{1}{(2\pi\hbar)^3} \int e^{-\frac{i}{\hbar}V(r_n,t_n)\Delta t_n}e^{\frac{i}{\hbar}p_n\Delta r_n}e^{-\frac{i}{\hbar}\frac{p_n^2}{2m}\Delta t_n}\text{d}p_n \\
&= \frac{1}{(2\pi\hbar)^3} \int e^{\frac{i}{\hbar}\left[p_n\frac{\Delta r_n}{\Delta t_n} - H(r_n,p_n,t_n)\right]\Delta t_n}\text{d}p_n \\
&= \frac{1}{(2\pi\hbar)^3} \int e^{\frac{i}{\hbar}\left[p_n\dot{r}_n - H(r_n,p_n,t_n)\right]\Delta t_n}\text{d}p_n \\
&= \frac{1}{(2\pi\hbar)^3} \int e^{\frac{i}{\hbar}L(r_n,p_n,t_n)\Delta t_n}\text{d}p_n \\
\end{align*}

$$

the propagator reads  

$$

\begin{align*}
K(r,t;r_0,t_0)
&= \int \left[\prod_{n=1}^N \mathcal{K}(r_n,t_n;r_{n-1},t_{n-1})\right] \text{d}r_1...\text{d}r_{N-1} \\
&= \int \prod_{n=1}^N \left[\frac{1}{(2\pi\hbar)^3} \int e^{\frac{i}{\hbar}L(r_n,p_n,t_n)\Delta t_n}\text{d}p_n\right] \text{d}r_1...\text{d}r_{N-1} \\
&= \frac{1}{(2\pi\hbar)^{3N}} \int \left[\int e^{\frac{i}{\hbar}\sum\limits_{n=1}^N L(r_n,p_n,t_n)\Delta t_n}\text{d}p_1...\text{d}p_N\right] \text{d}r_1...\text{d}r_{N-1} \\
&= \frac{1}{(2\pi\hbar)^{3N}} \int e^{\frac{i}{\hbar} \int_{t_0}^t L(r,p,\tau)\text{d}\tau} \text{d}r_1...\text{d}r_{N-1}\text{d}p_1...\text{d}p_N \\
&= \frac{1}{(2\pi\hbar)^{3N}} \int e^{\frac{i}{\hbar}S(r,p,t)} \mathcal{D}r\mathcal{D}p
\end{align*}

$$

where $\mathcal{D}$ denotes the full integration space  

$\clubsuit$ configuration space  
in configuration space the short time kernel reads  

$$

\begin{align*}
\mathcal{K}(r_n,t_n;r_{n-1},t_{n-1})
&= \frac{1}{(2\pi\hbar)^3} \int e^{-\frac{i}{\hbar}V(r_n,t_n)\Delta t_n}e^{\frac{i}{\hbar}p_n\Delta r_n}e^{-\frac{i}{\hbar}\frac{p_n^2}{2m}\Delta t_n}\text{d}p_n \\
&= \frac{1}{(2\pi\hbar)^3} e^{-\frac{i}{\hbar}V(r_n,t_n)\Delta t_n} \int e^{\frac{i}{\hbar}p_n\Delta r_n}e^{-\frac{i}{\hbar}\frac{p_n^2}{2m}\Delta t_n}\text{d}p_n \\
&= \left(\frac{m}{2\pi i\hbar\Delta t_n}\right)^{\frac{3}{2}} e^{-\frac{i}{\hbar}V(r_n,t_n)\Delta t_n} e^{i\frac{m(\Delta r_n)^2}{2\hbar\Delta t_n}} \\
&= \left(\frac{m}{2\pi i\hbar\Delta t_n}\right)^{\frac{3}{2}} e^{\frac{i}{\hbar}\left[\frac{m}{2}\frac{(\Delta r_n)^2}{(\Delta t_n)^2}-V(r_n,t_n)\right]\Delta t_n} \\
&= \left(\frac{m}{2\pi i\hbar\Delta t_n}\right)^{\frac{3}{2}} e^{\frac{i}{\hbar}\left[\frac{m}{2}\dot{r}_n^2-V(r_n,t_n)\right]\Delta t_n}
\end{align*}

$$

the propagator reads  

$$

\begin{align*}
K(r,t;r_0,t_0)
&= \int \left[\prod_{n=1}^N \mathcal{K}(r_n,t_n;r_{n-1},t_{n-1})\right] \text{d}r_1...\text{d}r_{N-1} \\
&= \int \left[\prod_{n=1}^N \left(\frac{m}{2\pi i\hbar\Delta t_n}\right)^{\frac{3}{2}} e^{\frac{i}{\hbar}\left[\frac{m}{2}\dot{r}_n^2-V(r_n,t_n)\right]\Delta t_n}\right] \text{d}r_1...\text{d}r_{N-1} \\
&= \prod_{n=1}^N \left(\frac{m}{2\pi i\hbar\Delta t_n}\right)^{\frac{3}{2}} \int e^{\frac{i}{\hbar} \sum\limits_{n=1}^N \left[\frac{m}{2}\dot{r}_n^2-V(r_n,t_n)\right]\Delta t_n} \text{d}r_1...\text{d}r_{N-1} \\
&= \prod_{n=1}^N \left(\frac{m}{2\pi i\hbar\Delta t_n}\right)^{\frac{3}{2}} \int e^{\frac{i}{\hbar} \int_{t_0}^t \left[\frac{m}{2}\dot{r}^2-V(r,\tau)\right]\text{d}\tau} \text{d}r_1...\text{d}r_{N-1} \\
&= \prod_{n=1}^N \left(\frac{m}{2\pi i\hbar\Delta t_n}\right)^{\frac{3}{2}} \int e^{\frac{i}{\hbar} S(r,\dot{r},t)}\mathcal{D}r
\end{align*}

$$

---

## physical intuition
state of a particle $\psi(r,t)$ is determined by <font color = OrangeRed>all possible previous state</font> $\psi(r_ {0},t_ {0})$  

$$

\psi(r,t) = \int K(r,t;r_0,t_0)\psi(r_0,t_0) \text{d}r_0

$$

where $K(r,t;r_ {0},t_ {0})$ is the _propagator_  

$$

K(r,t;r_0,t_0) = \sum_{\text{all path}}\text{const}\cdot\exp\left(\frac{i}{\hbar}S[x(t)]\right)

$$

where $S[x(t)]$ is the _action_  

$$

S[x(t)] = \int_{(r,t)}^{(r_0,t_0)} L(x(t),\dot{x}(t),t)\text{d}t

$$

which means that <font color = OrangeRed>all paths</font> between $(r,t)$ and $(r_ {0},t_ {0})$ are possible with possibility  

$$

P \sim \text{const}\cdot\exp\left(\frac{i}{\hbar}S[x(t)]\right)

$$

---

## equivalence to Schrodinger equation
consider the pertubative propagation from $\psi(r+\delta r,t)$ to $\psi(r,t+\delta t)$  

$$

\psi(r,t+\delta t) = \int K(r,t+\delta t;r+\delta r,t)\psi(r+\delta r,t)\text{d}r

$$

substitute the propagator we have  

$$

\psi(r,t+\delta t) = \int \left(\frac{m}{2\pi i\hbar\delta t}\right)^{\frac{3}{2}} e^{\frac{i}{\hbar}\left[\frac{m}{2}\frac{(\delta r)^2}{(\delta t)^2}-V(r,t)\right]\delta t} \psi(r+\delta r,t)\text{d}r

$$

with Taylor expansion, we have  

$$

e^{-\frac{i}{\hbar}V(r,t)\delta t} = \left[1-\frac{i}{\hbar}V(r,t)\delta t\right]\left[1+\mathcal{O}((\delta t)^2)\right]

$$

$$

\psi(r+\delta r,t) = \psi(r,t) + \delta r\psi'(r,t) + \frac{(\delta r)^2}{2}\psi''(r,t) + \mathcal{O}((\delta r)^3)

$$

$$

\begin{align*}
e^{-\frac{i}{\hbar}V(r,t)\delta t} \psi(r+\delta r,t) 
&=  \psi(r,t) + \delta r\psi'(r,t) + \frac{(\delta r)^2}{2}\psi''(r,t) \\
&- \frac{i}{\hbar}V(r,t)\delta t\psi(r,t) - \frac{i}{\hbar}V(r,t)\delta t\delta r\psi'(r,t) + \mathcal{O}[(\delta r)^3] + \mathcal{O}[(\delta t)^2]
\end{align*}

$$

with Gaussian integral formula, we have  

$$

\int \exp\left(\frac{im}{2\hbar t}r^2\right)\text{d}r = \left(\frac{2\pi i\hbar t}{m}\right)^\frac{3}{2}

$$

$$

\int r\exp\left(\frac{im}{2\hbar t}r^2\right)\text{d}r = 0

$$

$$

\int r^2\exp\left(\frac{im}{2\hbar t}r^2\right)\text{d}r = \frac{i\hbar t}{m}\left(\frac{2\pi i\hbar t}{m}\right)^\frac{3}{2}

$$

the final state reads  

$$

\begin{align*}
\psi(r,t+\delta t)
&= \left(\frac{m}{2\pi i\hbar\delta t}\right)^{\frac{3}{2}} \left\{\int e^{\frac{im}{2\hbar}\frac{(\delta r)^2}{\delta t}}\left(1-\frac{i}{\hbar}V(r,t)\delta t\right)\psi(r,t)\text{d}r + \int e^{\frac{im}{2\hbar}\frac{(\delta r)^2}{\delta t}}\frac{(\delta r)^2}{2}\psi''(r,t)\text{d}r\right\} \\
&= \left(\frac{m}{2\pi i\hbar\delta t}\right)^{\frac{3}{2}} \left\{\left(\frac{2\pi i\hbar\delta t}{m}\right)^\frac{3}{2}\left(1-\frac{i}{\hbar}V(r,t)\delta t\right)\psi(r,t) + \frac{i\hbar\delta t}{2m}\left(\frac{2\pi i\hbar\delta t}{m}\right)^\frac{3}{2}\psi''(r,t)\right\} \\
&= \left(1-\frac{i}{\hbar}V(r,t)\delta t\right)\psi(r,t) + \frac{i\hbar\delta t}{2m}\psi''(r,t)
\end{align*}

$$

then we can derive the Schrodinger equation  

$$

\begin{align*}
i\hbar\frac{\partial}{\partial t}\psi(r,t)
&= i\hbar\lim_{\delta t\rightarrow 0}\frac{\psi(r,t+\delta t)-\psi(r,t)}{\delta t} \\
&= i\hbar\lim_{\delta t\rightarrow 0}\frac{1}{\delta t}\left(-\frac{i}{\hbar}V(r,t)\delta t\psi(r,t) + \frac{i\hbar\delta t}{2m}\psi''(r,t)\right) \\
&= V(r,t)\psi(r,t) - \frac{\hbar^2}{2m}\psi''(r,t) \\
&= \left(-\frac{\hbar^2}{2m}\frac{\partial^2}{\partial r^2} + V(r,t)\right) \psi(r,t)
\end{align*}

$$

---

## one-dimensional harmonic oscillator
for the one-dimensional harmonis oscillator system, the Lagrangian reads  

$$

L = \frac{1}{2}m\dot{x}^2 - \frac{1}{2}m\omega^2x^2

$$

substitute into the short time kernel  

$$

\begin{align*}
\mathcal{K}(x_n,t_n;x_{n-1},t_{n-1})
&= \left(\frac{m}{2\pi i\hbar\delta t}\right)^{\frac{1}{2}} \exp\left\{\frac{im}{2\hbar}\left[\left(\frac{x_n-x_{n-1}}{\delta t}\right)^2 - \omega^2\frac{x_n^2+x_{n-1}^2}{2}\right]\delta t\right\} \\
&= \left(\frac{m}{2\pi i\hbar\delta t}\right)^{\frac{1}{2}} \exp\left\{\frac{i}{\hbar}\left[a_0\left(x_n^2+x_{n-1}^2\right) - 2b_0x_nx_{n-1}\right]\right\} \\
& \left(a_0 = \frac{m}{2\delta t} - \frac{\delta tm\omega^2}{4}, b_0 = \frac{m}{2\delta t}\right)
\end{align*}

$$

the path integral reads  

$$

\begin{align*}
K(x,t;x_0,t_0)
&= \lim_{N\rightarrow\infty} \int \prod_{n=1}^N \mathcal{K}(x_n,t_n;x_{n-1},t_{n-1}) \prod_{n=1}^{N-1} \text{d}x_n \\
&= \lim_{N\rightarrow\infty} \left(\frac{m}{2\pi i\hbar\delta t}\right)^{\frac{N}{2}} \int \exp\left\{\sum_{n=1}^{N}\frac{i}{\hbar}\left[a_0\left(x_n^2+x_{n-1}^2\right) - 2b_0x_nx_{n-1}\right]\right\} \prod_{n=1}^{N-1} \text{d}x_n \\
\end{align*}

$$

for the one-stage short time integral  

$$

\begin{align*}
& \int e^{\frac{i}{\hbar}}e^{\left[a_0\left(x_2^2+x_1^2\right) - 2b_0x_2x_1 + a_0\left(x_1^2+x_0^2\right) - 2b_0x_1x_0\right]} \text{d}x_1 \\
=& \int e^{\frac{i}{\hbar}} \exp\left[2a_0\left(x_1-\frac{b_0}{2a_0}(x_0+x_2)\right)^2 - \frac{b_0^2}{2a_0}(x_0+x_2)^2 + a_0\left(x_0^2+x_2^2\right)\right] \text{d}x_1 \\
=& \int e^{\frac{i}{\hbar}} \exp\left[2a_0\left(x_1-\frac{b_0}{2a_0}(x_0+x_2)\right)^2 + a_1\left(x_0^2+x_2^2\right) - 2b_1x_0x_2\right] \text{d}x_1 \\
=& \sqrt{\frac{i\pi\hbar}{2a_0}} \exp\left\{\frac{i}{\hbar} \left[a_1\left(x_0^2+x_2^2\right) - 2b_1x_0x_2\right]\right\} \\
& \left(a_1 = a_0 - \frac{b_0^2}{2a_0}, b_1 = \frac{b_0^2}{2a_0}\right)
\end{align*}

$$

for the two-stage short time integral  

$$

\begin{align*}
& \int e^{\frac{i}{\hbar}} e^{\left[a_0\left(x_3^2+x_2^2\right) - 2b_0x_3x_2 + a_0\left(x_2^2+x_1^2\right) - 2b_0x_2x_1 + a_0\left(x_1^2+x_0^2\right) - 2b_0x_1x_0\right]} \text{d}x_1\text{d}x_2 \\
=& \sqrt{\frac{i\pi\hbar}{2a_0}} \int e^{\frac{i}{\hbar}} e^{\left[a_0\left(x_3^2+x_2^2\right) - 2b_0x_3x_2 + a_1\left(x_0^2+x_2^2\right) - 2b_1x_0x_2\right]} \text{d}x_2 \\
=& \sqrt{\frac{i\pi\hbar}{2a_0}} \int e^{\frac{i}{\hbar}} \exp\left[(a_0+a_1)\left(x_2-\frac{1}{a_0+a_1}(b_0x_3+b_1x_0)\right)^2 - \frac{(b_0x_3+b_1x_0)^2}{a_0+a_1} + a_0x_3^2 + a_1x_0^2\right] \text{d}x_2 \\
=& \sqrt{\frac{i\pi\hbar}{2a_0}} \int e^{\frac{i}{\hbar}} \exp\left[(a_0+a_1)\left(x_2-\frac{1}{a_0+a_1}(b_0x_3+b_1x_0)\right)^2 + a_2\left(x_3^2 + x_0^2\right) - 2b_2x_0x_3\right] \text{d}x_2 \\
=& \sqrt{\frac{i\pi\hbar}{2a_0}} \sqrt{\frac{i\pi\hbar}{a_0+a_1}} \exp\left\{\frac{i}{\hbar} \left[a_2\left(x_0^2+x_3^2\right) - 2b_2x_0x_3\right]\right\} \\
& \left(a_2 = a_0 - \frac{b_0^2}{a_0+a_1} = a_1 - \frac{b_1^2}{a_0+a_1}, b_2 = \frac{b_0b_1}{a_0+a_1}\right)
\end{align*}

$$

with _mathematical induction_ we can derive  

$$

K(x,t;x_0,t_0) = \lim_{N\rightarrow\infty} \left(\frac{m}{2\pi i\hbar\delta t}\right)^{\frac{N}{2}} \sqrt{\prod_{n=0}^{N-2}\frac{i\pi\hbar}{a_0+a_n}} \exp\left\{\frac{i}{\hbar} \left[a_{N-1}\left(x_0^2+x_N^2\right) - 2b_{N-1}x_0x_N\right]\right\} \\
\left(a_0 = \frac{m}{2\delta t} - \frac{\delta tm\omega^2}{4}, b_0 = \frac{m}{2\delta t}, 
a_n = a_0 - \frac{b_0^2}{a_0+a_{n-1}}, b_n = \frac{b_0b_{n-1}}{a_0+a_{n-1}}\right)

$$

consider the infinite time splite, we can make the approximation that  

$$

a_0 = \frac{m}{2\delta t} \left(1 - \frac{(\delta t)^2\omega^2}{2}\right) = b_0 \left(1 - 2\sin^2\frac{\delta t\omega}{2}\right) = b_0\cos(\delta t\omega)

$$

substituite into the notations  

$$

\begin{align*}
& a_1 = a_0 - \frac{b_0^2}{2a_0} = b_0\frac{\sin(\delta t\omega)\cos(2\delta t\omega)}{\sin(2\delta t\omega)}, & a_0+a_1 = b_0\frac{\sin(3\delta t\omega)}{\sin(2\delta t\omega)} \\
& a_2 = a_0 - \frac{b_0^2}{a_0+a_1} = b_0\frac{\sin(\delta t\omega)\cos(3\delta t\omega)}{\sin(3\delta t\omega)}, & a_0+a_2 = b_0\frac{\sin(4\delta t\omega)}{\sin(3\delta t\omega)} \\
& ... \\
& a_0+a_{n-1} = b_0\frac{\sin((n+1)\delta t\omega)}{\sin(n\delta t\omega)} \\
\end{align*}

$$

where we can derive  

$$

a_{n-1} = b_0\frac{\sin(\delta t\omega)\cos(n\delta t\omega)}{\sin(n\delta t\omega)}, b_{n-1} = b_0\frac{\sin(\delta t\omega)}{\sin(n\delta t\omega)}

$$

substitute into the path integral expression  

$$

\prod_{n=0}^{N-2}\frac{1}{a_0+a_n} = \frac{1}{b_0^{N-1}} \left(\prod_{n=0}^{N-2}\frac{\sin((n+1)\delta t\omega)}{\sin((n+2)\delta t\omega)}\right) = \left(\frac{2\delta t}{m}\right)^{N-1} \frac{\sin(\delta t\omega)}{\sin(N\delta t\omega)}

$$

then the path integral reads  

$$

\begin{align*}
K(x,t;x_0,t_0)
&= \lim_{N\rightarrow\infty} \left(\frac{m}{2\pi i\hbar\delta t}\right)^{\frac{N}{2}} \sqrt{\prod_{n=0}^{N-2}\frac{i\pi\hbar}{a_0+a_n}} \exp\left\{\frac{i}{\hbar} \left[a_{N-1}\left(x_0^2+x_N^2\right) - 2b_{N-1}x_0x_N\right]\right\} \\
&= \lim_{N\rightarrow\infty} \left(\frac{m}{2\pi i\hbar\delta t}\right)^{\frac{N}{2}} \left(\frac{2i\pi\hbar\delta t}{m}\right)^\frac{N-1}{2} \left[\frac{\sin(\delta t\omega)}{\sin(\Delta t\omega)}\right]^\frac{1}{2} e^{\frac{i}{\hbar}\frac{m\omega}{2\sin(\Delta t\omega)} \left[\cos(\Delta t\omega)\left(x_0^2+x^2\right) - 2x_0x\right]} \\
&= \left(\frac{m\omega}{2\pi i\hbar\sin(\omega\Delta t)}\right)^{\frac{1}{2}} \exp\left\{\frac{i}{\hbar}\frac{m\omega}{2\sin(\omega\Delta t)} \left[\cos(\omega\Delta t)\left(x_0^2+x^2\right) - 2x_0x\right]\right\}
\end{align*}

$$

with periodic boundary condition $x=x_ {0}$, we have the trace of propagator  

$$

\begin{align*}
K(\Delta t)
&= \int K(x_0,t;x_0,t_0) \text{d}x_0 \\
&= \left(\frac{m\omega}{2\pi i\hbar\sin(\omega\Delta t)}\right)^{\frac{1}{2}} \int \exp\left[\frac{i}{\hbar}\frac{m\omega}{\sin(\omega\Delta t)} (\cos(\omega\Delta t)-1)x_0^2\right] \text{d}x_0 \\
&= \left(\frac{m\omega}{2\pi i\hbar\sin(\omega\Delta t)}\right)^{\frac{1}{2}} \left(\frac{i\pi\hbar\sin(\omega\Delta t)}{m\omega(\cos(\omega\Delta t)-1)}\right)^\frac{1}{2} \\
&= \left(\frac{1}{2(\cos(\omega\Delta t)-1)}\right)^\frac{1}{2} 
= \left(\sqrt{-4\sin^2\frac{\omega\Delta t}{2}}\right)^{-1} 
= \left(2i\sin\frac{\omega\Delta t}{2}\right)^{-1} \\
&= \frac{1}{e^{i\omega\Delta t/2} - e^{-i\omega\Delta t/2}} 
= e^{-\frac{i\omega\Delta t}{2}} \frac{1}{1-e^{-i\omega\Delta t}} \\
&= \sum_{n=0}^\infty \exp\left[-i\left(n+\frac{1}{2}\right)\omega\Delta t\right]
\end{align*}

$$

which equals to the sum of all eigenvalues of time evolution operator  

$$

K(\Delta t) = \sum_{n=0}^\infty \exp\left(-i\frac{E_n\Delta t}{\hbar}\right)

$$

finally, we can get the energy level of the one dimensional harmonic oscillator  

$$

E_n = \left(n+\frac{1}{2}\right)\hbar\omega

$$

which coincides with other methods' results  

---
