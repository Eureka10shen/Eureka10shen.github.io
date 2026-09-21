---
title: "Quantum Monte Carlo"
date: 2022-12-18 02:48:00 +0800
categories:
  - quantum-mechanics
excerpt: "Notes on variational and diffusion Monte Carlo, imaginary-time projection, Green functions, drift-diffusion, and branching."
mathjax: true
original_url: "https://www.cnblogs.com/Eureka10shen/articles/16989931.html"
permalink: /blog/quantum-monte-carlo/
---

> This article was migrated from [Eureka10shen on 博客园]({{ page.original_url }}). The original publication date was 2022-12-18.
---

references :  
Diffusion Monte Carlo : A powerful tool for studying quantum many-body systems, Tao Pang, Am.J.Phys. 82(10)   
Quantum Monte Carlo simulations of solids, W.M.C. Foulkes, et al., Rev.Mod.Phys., 73(33)  
Introduction to the Variational and Diffusion Monte Carlo Methods, Julien Toulouse, et al., Advances in Quantum Chemistry, 73(285)  

---

## Overview

real-space quantum Monte Carlo methods

---

## Variational Monte Carlo (VMC)

the idea of the VMC method is simply to calculate the multidimensional integrals appearing in quantum mechanics using a Monte Carlo numerical integration technique  
the variational energy reads  

$$

E_v = \frac{\langle\Psi|\hat{H}|\Psi\rangle}{\langle\Psi|\Psi\rangle} = \frac{\int\text{d}\mathbf{r}\Psi(\mathbf{r})^2E_L(\mathbf{r})}{\int\text{d}\mathbf{r}\Psi(\mathbf{r})^2} = \int\text{d}\mathbf{r}\rho(\mathbf{r})E_L(\mathbf{r})

$$

where $E_ {L}(\mathbf{r}) = \hat{H}\Psi(\mathbf{r})/\Psi(\mathbf{r})$ is the __local energy__  
and $\rho(\mathbf{r}) = \Psi(\mathbf{r})^2/\int\text{d}\mathbf{r}\Psi(\mathbf{r})^2$ is the __normalized probability density__  
the variational energy becomes  

$$

E_v = \mathbb{E}_{\mathbf{r}\sim\rho(\mathbf{r})} [E_L(\mathbf{r})]

$$

which can be estimated by sampling  

$$

E_v \approx \bar{E}_L = \frac{1}{N}\sum_{i=1}^N E_L(\mathbf{r}_i) \quad (\mathbf{r}_i \sim \rho(\mathbf{r}))

$$

---

## Diffusion Monte Carlo (DMC)

### Basic Ideas

the limitation of VMC is that unless we know the exact form of the ground state wavefunction, the simulation will never approach the ground state  
DMC helps to simulate a many-body wavefunction with limited knowledge  
consider the trial wavefunction $\Phi(\mathbf{r})$  
if it is the eigenstate of $\hat{H}$ with $E'$ the eigenvalue other than the groud state  

$$

\begin{aligned}
\langle\Psi_0(\mathbf{r})|\hat{H}|\Phi(\mathbf{r})\rangle 
&= \langle\Psi_0(\mathbf{r})|E'|\Phi(\mathbf{r})\rangle = 0 \\
&= \langle\Psi_0(\mathbf{r})|E_0|\Phi(\mathbf{r})\rangle = 0 \\
\end{aligned}

$$

since eigenstates with different eigenvalues of Hermitian operator are orthogonal  
if it is not the eigenstate of $\hat{H}$  

$$

\langle\Psi_0(\mathbf{r})|\hat{H}|\Phi(\mathbf{r})\rangle = \langle\Psi_0(\mathbf{r})|E_0|\Phi(\mathbf{r})\rangle = E_0\langle\Psi_0(\mathbf{r})|\Phi(\mathbf{r})\rangle

$$

we have  

$$

E_0 = \frac{\langle\Psi_0(\mathbf{r})|\hat{H}|\Phi(\mathbf{r})\rangle}{\langle\Psi_0(\mathbf{r})|\Phi(\mathbf{r})\rangle} = \frac{\int\text{d}\mathbf{r}\Psi_0(\mathbf{r})\Phi(\mathbf{r})E_L(\mathbf{r})}{\int\text{d}\mathbf{r}\Psi_0(\mathbf{r})\Phi(\mathbf{r})} = \int\text{d}\mathbf{r}\rho(\mathbf{r})E_L(\mathbf{r})

$$

which denote thes expectation value of __local energy__ $E_ {L}(\mathbf{r}) = \hat{H}\Phi(\mathbf{r})/\Phi(\mathbf{r})$ under the __mixed distribution__  

$$

\rho(\mathbf{r}) = \frac{\Psi_0(\mathbf{r})\Phi(\mathbf{r})}{\int\text{d}\mathbf{r}\Psi_0(\mathbf{r})\Phi(\mathbf{r})}

$$

but how to access to the exact ground state $\Psi_ {0}(\mathbf{r})$ ?  
the idea is to __make use the connection__ between the trial wavefuntion $\Phi(\mathbf{r})$ and $\Psi_ {0}(\mathbf{r})$  

### Ground State Projection

rewrite the time-dependent Schrodinger equation  

$$

i\hbar\frac{\partial\Psi(\mathbf{r},t)}{\partial t} = \hat{H}\Psi(\mathbf{r},t)

$$

in the imaginary-time form  

$$

\frac{\partial\Psi(\mathbf{r},\tau)}{\partial\tau} = -(\hat{H}-E_R)\Psi(\mathbf{r},\tau)

$$

where $\tau = -it/\hbar$ and $E_ {R}$ is the reference energy  
the solution reads  

$$

\Psi(\mathbf{r},\tau) = e^{-(\hat{H}-E_R)\tau}\Psi(\mathbf{r},0)

$$

in position representation, the solution can be written as  

$$

\Psi(\mathbf{r},\tau) = \int G(\mathbf{r}|\mathbf{r}';\tau)\Psi(\mathbf{r}',0)\text{d}\mathbf{r}'

$$

where  

$$

G(\mathbf{r}|\mathbf{r}';\tau) = \langle\mathbf{r}|e^{-(\hat{H}-E_R)\tau}|\mathbf{r}'\rangle

$$

is a Green function called the imaginary-time propagator from $\mathbf{r}$ to $\mathbf{r}'$  
with the spectral expansion we have  

$$

e^{-\hat{H}\tau} = \sum_i|\Psi_i\rangle e^{-E_i\tau}\langle\Psi_i|

$$

where $\{\Psi_ {i}\}$ and $\{E_ {i}\}$ denote the complete sets of eigenfunctions and eigenvalues  
one can express the Green function as  

$$

G(\mathbf{r}|\mathbf{r}';\tau) = \sum_i \Psi_i(\mathbf{r}) e^{-(E_i-E_R)\tau}\Psi_i(\mathbf{r}')

$$

the solution at infinite imaginary-time reads  

$$

\begin{aligned}
\lim_{\tau\rightarrow\infty} \Psi(\mathbf{r},\tau)
&= \lim_{\tau\rightarrow\infty} \int G(\mathbf{r}|\mathbf{r}';\tau)\Psi(\mathbf{r}',0)\text{d}\mathbf{r}' \\
&= \lim_{\tau\rightarrow\infty} \sum_i \Psi_i(\mathbf{r}) e^{-(E_i-E_R)\tau}\int\Psi_i(\mathbf{r}')\Psi(\mathbf{r}',0)\text{d}\mathbf{r}' \\
&= \lim_{\tau\rightarrow\infty} \Psi_0(\mathbf{r}) e^{-(E_0-E_R)\tau} \langle\Psi_0(\mathbf{r}')|\Psi(\mathbf{r}',0)\rangle
\end{aligned}

$$

since all excited states of energies $E_ {i}>E_ {0}$ decay exponentially faster  
regard the initial state $\Psi(\mathbf{r}',0)$ as the trial wavefunction $\Phi(\mathbf{r})$, we have made the connection between the time evolution of trial wavefunction and the ground state of the system  
which is often called the __ground state projection__ method  

### Diffusion Process

the ground state is only contained in the mixed distribution term  

$$

\rho(\mathbf{r}) = \frac{\Psi_0(\mathbf{r})\Phi(\mathbf{r})}{\int\text{d}\mathbf{r}\Psi_0(\mathbf{r})\Phi(\mathbf{r})}

$$

define the evolution function  

$$

f(\mathbf{r},\tau) = \Psi(\mathbf{r},\tau) \Phi(\mathbf{r})

$$

we have  

$$

\lim_{\tau\rightarrow\infty}f(\mathbf{r},\tau) \propto \Psi_0(\mathbf{r}) \Phi(\mathbf{r})

$$

the focus is to get the evolution function at the limit of infinite time  
from the imaginary-time form of Schrodinger equation  

$$

\frac{\partial\Psi(\mathbf{r},\tau)}{\partial\tau} = -(\hat{H}-E_R)\Psi(\mathbf{r},\tau)

$$

we have  

$$

\frac{\partial f(\mathbf{r},\tau)}{\partial\tau} = \frac{\hbar^2}{2m}\nabla^2f(\mathbf{r},\tau) - \nabla[\mathbf{v}_D(\mathbf{r})f(\mathbf{r},\tau)] - [E_L(\mathbf{r})-E_R]f(\mathbf{r},\tau)

$$

where  

$$

\mathbf{v}_D(\mathbf{r}) = \frac{\hbar^2}{m}\nabla\ln|\Phi(\mathbf{r})|

$$

$$

E_L(\mathbf{r}) = \frac{\hat{H}\Phi(\mathbf{r})}{\Phi(\mathbf{r})}

$$

the first term denotes a pure diffusion  
the second term is a drift term with $\mathbf{v}_ {D}(\mathbf{r})$ the drift velocity of the mixed distribution  
the third term is a source/sink term  
Proof :  

$$

\begin{aligned}
\frac{\partial f(\mathbf{r},\tau)}{\partial\tau} 
&= \frac{\hbar^2}{2m}\nabla^2f(\mathbf{r},\tau) - \nabla[\mathbf{v}_D(\mathbf{r})f(\mathbf{r},\tau)] - [E_L(\mathbf{r})-E_R]f(\mathbf{r},\tau) \\
&= \frac{\hbar^2}{2m}\left[\Phi(\mathbf{r})\nabla^2\Psi(\mathbf{r},\tau) + 2\nabla\Phi(\mathbf{r})\nabla\Psi(\mathbf{r},\tau) + \Psi(\mathbf{r},\tau)\nabla^2\Phi(\mathbf{r})\right] \\
&\quad - \frac{\hbar^2}{m}\left[\Psi(\mathbf{r},\tau)\nabla^2\Phi(\mathbf{r}) + \nabla\Phi(\mathbf{r})\nabla\Psi(\mathbf{r},\tau)\right] - \left[\hat{H}\Phi(\mathbf{r})\right]\Psi(\mathbf{r},\tau) + E_Rf(\mathbf{r},\tau) \\
&= \frac{\hbar^2}{2m}\left[\Phi(\mathbf{r})\nabla^2\Psi(\mathbf{r},\tau) - \Psi(\mathbf{r},\tau)\nabla^2\Phi(\mathbf{r})\right] + \frac{\hbar^2}{2m}\Psi(\mathbf{r},\tau)\nabla^2\Phi(\mathbf{r}) \\
&\quad - V(\mathbf{r})\Psi(\mathbf{r},\tau)\Phi(\mathbf{r}) + E_Rf(\mathbf{r},\tau) \\
&= \frac{\hbar^2}{2m}\Phi(\mathbf{r})\nabla^2\Psi(\mathbf{r},\tau) - V(\mathbf{r})\Psi(\mathbf{r},\tau)\Phi(\mathbf{r}) + E_Rf(\mathbf{r},\tau) \\
&= \left[-(\hat{H}-E_R)\Psi(\mathbf{r},\tau)\right]\Phi(\mathbf{r}) \\
&= \frac{\partial\Psi(\mathbf{r},\tau)}{\partial\tau}\Phi(\mathbf{r})
\end{aligned}

$$

### Time Evolution

the short-time evolution of $f(\mathbf{r},\tau)$ reads  

$$

f(\mathbf{r},\tau+\Delta\tau) = \int\tilde{G}(\mathbf{r}|\mathbf{r}';\Delta\tau)f(\mathbf{r}',\tau)\text{d}\mathbf{r}'

$$

from the definition of the evolution function  

$$

\begin{aligned}
f(\mathbf{r},\tau+\Delta\tau) 
&= \Psi(\mathbf{r},\tau+\Delta\tau) \Phi(\mathbf{r}) \\
&= \int G(\mathbf{r}|\mathbf{r}';\Delta\tau)\Psi(\mathbf{r}',\tau)\text{d}\mathbf{r}'\Phi(\mathbf{r}) \\
&= \int \Phi(\mathbf{r})G(\mathbf{r}|\mathbf{r}';\Delta\tau)\frac{1}{\Phi(\mathbf{r}')}\Psi(\mathbf{r}',\tau)\Phi(\mathbf{r}')\text{d}\mathbf{r}' \\
&= \int \Phi(\mathbf{r})G(\mathbf{r}|\mathbf{r}';\Delta\tau)\frac{1}{\Phi(\mathbf{r}')}f(\mathbf{r}',\tau)\text{d}\mathbf{r}'
\end{aligned}

$$

we have  

$$

\tilde{G}(\mathbf{r}|\mathbf{r}';\Delta\tau) = \Phi(\mathbf{r})G(\mathbf{r}|\mathbf{r}';\Delta\tau)\frac{1}{\Phi(\mathbf{r}')}

$$

for the Green function of wavefunction, apply the Trotter-Suzuki formula  

$$

e^{-(\hat{T}+\hat{V})\tau} = e^{-\hat{V}\tau/2}e^{-\hat{T}\tau}e^{-\hat{V}\tau/2} + O(\tau^3)

$$

the Green function reads  

$$

G(\mathbf{r}|\mathbf{r}';\tau) \approx \left(\frac{m}{2\pi\tau\hbar^2}\right)^{\frac{3N}{2}} \exp\left[-\frac{(\mathbf{r}-\mathbf{r}')^2}{2\tau}\right] \exp\left[-\left(\frac{V(\mathbf{r})+V(\mathbf{r}')}{2}-E_R\right)\tau\right]

$$

the Green function of evolution function reads  

$$

\tilde{G}(\mathbf{r}|\mathbf{r}';\Delta\tau) = P(\mathbf{r}|\mathbf{r}')W(\mathbf{r}|\mathbf{r}')

$$

where  

$$

P(\mathbf{r}|\mathbf{r}') = \left(\frac{m}{2\pi\tau\hbar^2}\right)^{\frac{3N}{2}} \exp\left\{-\frac{[\mathbf{r}-\mathbf{r}'-\Delta\tau\mathbf{v}_D(\mathbf{r}')]^2}{2\Delta\tau}\right\}

$$

$$

W(\mathbf{r}|\mathbf{r}') = \exp\left[-\left(\frac{E_L(\mathbf{r})+E_L(\mathbf{r}')}{2}-E_R\right)\tau\right]

$$

the propagator can be sampled by a __branching or birth-death process__  
use at each iteration $k$ a population of $M_ {k}$ walkers  

$$

\mathbf{r}_{k,\alpha} \sim P(\mathbf{r}_{k,\alpha}|\mathbf{r}_{k-1,\alpha}) \quad (\alpha=1,2,...,M_k)

$$

$$

w_{k,\alpha} = W(\mathbf{r}_{k,\alpha}|\mathbf{r}_{k-1,\alpha}) w_{k-1,\alpha} \quad (w_{k,\alpha}=1, \alpha=1,2,...,M_k)

$$

$$

f(\mathbf{r}) \propto \mathbb{E}\left[\sum_{\alpha=1}^{M_k}w_{k,\alpha}\delta(\mathbf{r}-\mathbf{r}_{k,\alpha})\right] \approx \frac{1}{M}\sum_{k=1}^{M}\sum_{\alpha=1}^{M_k}w_{k,\alpha}\delta(\mathbf{r}-\mathbf{r}_{k,\alpha})

$$

the ground state energy reads  

$$

E_0 \approx \bar{E}_L = \frac{\sum\limits_{k=1}^{M}\sum\limits_{\alpha=1}^{M_k}w_{k,\alpha}E_L(\mathbf{r}_{k,\alpha})}{\sum\limits_{k=1}^{M}\sum\limits_{\alpha=1}^{M_k}w_{k,\alpha}}

$$

---
