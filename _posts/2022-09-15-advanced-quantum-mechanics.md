---
title: "Advanced Quantum Mechanics"
date: 2022-09-15 22:51:00 +0800
categories:
  - quantum-mechanics
excerpt: "A structured review of mathematical foundations, Hilbert spaces, operators, quantum states, identical particles, and second quantization."
mathjax: true
original_url: "https://www.cnblogs.com/Eureka10shen/articles/16698221.html"
permalink: /blog/advanced-quantum-mechanics/
---

> This article was migrated from [Eureka10shen on 博客园]({{ page.original_url }}). The original publication date was 2022-09-15.

---
reference books :  
高等量子力学，第二版，喀兴林，高等教育出版社，ISBN: 9787040099256  
量子力学，第四版，卷II，曾谨言，科学出版社，ISBN: 9787030190215

---

# C1 -- Mathematical Fundamentals and Physical Principles

## 1.1 Basic principles of quantum mechanics

(1) state of a microsystem <--> vector in a __Hilbert space__  
 

$$

|\Psi\rangle = \sum_{i=1}^N c_i|\psi_i\rangle

$$

$$

|\Psi\rangle := [c_1, c_2, ..., c_N]^\top,\qquad
\langle\Psi| := [c_1, c_2, ..., c_N]

$$

(2) physical quantity of a microsystem <--> __Hermite operatror__ in Hilbert space  
 

$$

\hat{O}|\psi_i\rangle = \lambda_i|\psi_i\rangle

$$

$$

\langle\hat{O}\rangle = \langle\Psi|\hat{O}|\Psi\rangle
= \langle\sum_{i=1}^Nc_i\psi_i|\hat{O}|\sum_{j=1}^Nc_j\psi_j\rangle
= \sum_{ij}c_ic_j\langle\psi_i|\hat{O}|\psi_j\rangle
= \sum_{ij}c_ic_j\lambda_i\delta_{ij}
= \sum_i|c_i|^2\lambda_i

$$

(3) commutation between location operator and momentum operator  
 

$$

[\mathbf{x_i}, \mathbf{x_j}] = [\mathbf{p_i}, \mathbf{p_j}] = 0

$$

$$

[\mathbf{x_i}, \mathbf{p_j}] = i\hbar\delta_{ij}

$$

(4) evolution of the state of a microsystem --> Schrödinger equation  
 

$$

i\hbar\frac{\partial|\Psi(t)\rangle}{\partial t}
= \hat{H}|\Psi(t)\rangle

$$

(5) symmetry of identical particles --> symmetrical (Boson), antisymmetrical (Fermi)
 

$$

|\Psi(..., \mathbf{q_i}, ..., \mathbf{q_j}, ...)\rangle
= \pm|\Psi(..., \mathbf{q_j}, ..., \mathbf{q_i}, ...)\rangle

$$

## 1.2 Hilbert space
__vector space__ : a set $\mathcal{H} = \{\psi. \phi, ...\}$ where all elements satisfy the rules  
(1) additon --> $\forall \psi, \phi \in \mathcal{H}$, $\chi = \psi + \phi \in \mathcal{H}$  
(2) multiplication --> $\forall a\in\mathbb{C}$ and $\psi\in\mathcal{H}$, $\chi = a\psi\in\mathcal{H}$  
(3) inner product --> $\forall \psi,\phi\in\mathcal{H}$, $(\psi, \phi) = C \in \mathbb{C}$

__basis vector__ : an orthogonal complete set of the vector space  
projection onto basis vector $\vert \psi_{i}\rangle$ --> $\vert \psi_{i}\rangle\langle\psi_{i}\vert $
--> $\sum_{i}\vert \psi_{i}\rangle\langle\psi_{i}\vert  = 1$
 

$$

\langle\Phi|\Psi\rangle
= \left(\sum_i\langle\Phi|\psi_i\rangle\langle\psi_i|\right)|\Psi\rangle
= \sum_i\langle\Phi|\psi_i\rangle\langle\psi_i|\Psi\rangle

$$

__complete space__ : for all __Cauchy sequence__ $\{S_{n}\}$ in the vector space, $\{S_{n}\}$ converges to a vector in the space  
Cauchy sequence $\{S_{n}\}$ --> $\forall\varepsilon>0, \exists N, s.t. \forall m,n>N\Rightarrow\vert S_{n}-S_{m}\vert <\varepsilon$

__Hilbert space__ : infinite-dimensional complete vector space  
conjugate space : ket --> $\vert \psi\rangle \in \mathcal{H}$, bra --> $\langle\psi\vert  \in \mathcal{H}^{\ast}$ --> $\langle\psi\vert  = \vert \psi\rangle^{\ast}$  

## 1.3 Operator
__operator__ : transformation between vectors in Hilbert space  

$$

\forall |\psi\rangle \in \mathcal{H}, \hat{O}|\psi\rangle = |\phi\rangle \in \mathcal{H}

$$

$$

\hat{O} \{|\psi\rangle+|\phi\rangle\} = \hat{O}|\psi\rangle + \hat{O}|\phi\rangle

$$

conjugate of an operator -->
$\langle\psi\vert\hat{A}^\dagger\vert\phi\rangle
= (\langle\psi\vert\hat{A}^\dagger)\vert\phi\rangle
= (\hat{A}\vert\psi\rangle)^{\ast}(\langle\phi\vert)^{\ast}
= \langle\phi\vert\hat{A}\vert\psi\rangle^{\ast}$  
Harmite operator --> $\hat{A}^\dagger = \hat{A}$  
unitrary operator --> $\hat{U}^{-1} = \hat{U}^\dagger$

__eigenvalue__

$$

\hat{A}|\psi_i\rangle = a_i|\psi_i\rangle,\qquad
\hat{A}\langle\psi_i| = a_i'\langle\psi_i|

$$

linear operator --> left and right eigenvalue spectrums are identical  
Hermite operator --> eigenvalues are real, eigenvectors of different eigenvalues are orthogonal

__projective operator__ --> $\hat{P_{S}}\vert \psi\rangle = \vert \psi_{S}\rangle \in \mathcal{S} \subset \mathcal{H}, \forall \vert \psi\rangle \in\mathcal{H}$  
(1) idempotent --> $\hat{P_{S}}^2 = \hat{P_{S}}$  
_Proof_ : 

$$

\hat{P_S}^2|\psi\rangle = \hat{P_S}|\psi_S\rangle = |\psi_S\rangle

$$

(2) eigenvalues of $\hat{P_{S}}$ are 0 and 1, eigenvectors span the whole Hilbert space $\mathcal{H} = \mathcal{S} + \mathcal{S'}$  
_Proof_ : 

$$

\hat{P_S}|\psi_S\rangle = |\psi_S\rangle
\Rightarrow (\hat{P_S}-1)|\psi_S\rangle = 0,\qquad
\forall|\psi_S\rangle\in\mathcal{S}

$$

$$

\hat{P_S}|\psi_{S'}\rangle = 0
\Rightarrow (\hat{P_S}-0)|\psi_{S'}\rangle = 0,\qquad
\forall|\psi_{S'}\rangle\in\mathcal{S'}

$$

$$

|\psi\rangle = |\psi_S\rangle + |\psi_{S'}\rangle,\qquad
\forall|\psi\rangle\in\mathcal{H}

$$

(3) $\hat{P} = \vert \psi_{i}\rangle\langle\psi_{i}\vert $ is a projective operator  
_Proof_ : 

$$

\forall |\Psi\rangle \in\mathcal{H},\qquad
\hat{P}|\Psi\rangle = |\psi_i\rangle\langle\psi_i|\Psi\rangle = c_i|\psi_i\rangle

$$

## 1.4 Representation theory

In the ψ-basis, a state vector can be written as

$$

|\Psi\rangle
= \sum_i |\psi_i\rangle\langle\psi_i|\Psi\rangle
= \begin{bmatrix}|\psi_1\rangle & \cdots & |\psi_N\rangle\end{bmatrix}
\begin{bmatrix}c_1 \\ \vdots \\ c_N\end{bmatrix}.

$$

The corresponding bra is

$$

\langle\Psi|
= \sum_i \langle\Psi|\psi_i\rangle\langle\psi_i|
= \begin{bmatrix}c_1^{\ast} & \cdots & c_N^{\ast}\end{bmatrix}.

$$

The inner product and the action of an operator are represented by

$$

\begin{aligned}
\langle\Psi|\Phi\rangle
&= \sum_i \langle\Psi|\psi_i\rangle
   \langle\psi_i|\Phi\rangle, \\
\hat{A}|\Psi\rangle
&= \sum_{ij}|\psi_i\rangle
   \langle\psi_i|\hat{A}|\psi_j\rangle
   \langle\psi_j|\Psi\rangle.
\end{aligned}

$$

For two orthonormal bases, define the change-of-basis matrix by

$$

U_{\phi\to\psi}
= \begin{bmatrix}
\langle\psi_1|\phi_1\rangle & \cdots & \langle\psi_1|\phi_N\rangle \\
\vdots & \ddots & \vdots \\
\langle\psi_N|\phi_1\rangle & \cdots & \langle\psi_N|\phi_N\rangle
\end{bmatrix}.

$$

The coefficient vectors satisfy

$$

\begin{bmatrix}c_1 \\ \vdots \\ c_N\end{bmatrix}
= U_{\phi\to\psi}
\begin{bmatrix}b_1 \\ \vdots \\ b_N\end{bmatrix},
\qquad
\begin{bmatrix}b_1 \\ \vdots \\ b_N\end{bmatrix}
= U_{\phi\to\psi}^{-1}
\begin{bmatrix}c_1 \\ \vdots \\ c_N\end{bmatrix}.

$$

For orthonormal bases, the transformation is unitary:

$$

U_{\phi\to\psi}^{\dagger}
= U_{\psi\to\phi}
= U_{\phi\to\psi}^{-1}.

$$

---

# C2 - Density Matrix and Complex System

## 2.1 Density operator
Considering a complete set of commuting conserved observables $F$, whose simultaneous eigenstates form a complete basis, we use the $F$-representation.

_completeness_:

$$

\sum_i |\psi_i\rangle\langle\psi_i| = 1

$$

The quantum state in the $F$-representation is

$$

|\Psi\rangle = \sum_i|\psi_i\rangle\langle\psi_i|\Psi\rangle
= \sum_i c_i|\psi_i\rangle

$$

The density operator $\hat{\rho}$ in the $F$-representation is

$$

\hat{\rho}_{\{|\psi_i\rangle\}} = \langle\psi_i|\hat{\rho}|\psi_j\rangle 
= \langle\psi_i|\Psi\rangle \langle\Psi|\psi_j\rangle
= \begin{bmatrix}c_1 \\ c_2 \\ \vdots \\ c_N\end{bmatrix}
\begin{bmatrix}c_1 & c_2 & \dots & c_N\end{bmatrix}

$$

## 2.2 Mixed state
$\diamondsuit$ for a __pure state__, we have the density operator  

$$

\hat{\rho} = |\Psi\rangle\langle\Psi|

$$

average of observable $B$  

$$

\langle\hat{B}\rangle = \langle\Psi|\hat{B}|\Psi\rangle
= \sum_i \langle\Psi|\hat{B}|\psi_i\rangle\langle\psi_i|\Psi\rangle
= \sum_i \langle\psi_i|\Psi\rangle\langle\Psi|\hat{B}|\psi_i\rangle
= \sum_i \langle\psi_i|\hat{\rho}\hat{B}|\psi_i\rangle = \text{Tr}[\hat{\rho}\hat{B}]

$$

for the trace of density operator  

$$

\text{Tr}[\hat{\rho}] = \sum_i \langle\psi_i|\hat{\rho}|\psi_i\rangle
= \sum_i \langle\psi_i|\Psi\rangle\langle\Psi|\psi_i\rangle
= \sum_i \langle\Psi|\psi_i\rangle\langle\psi_i|\Psi\rangle
= \langle\Psi|\Psi\rangle = 1

$$

idempotent

$$

\hat{\rho}^2 = (|\Psi\rangle\langle\Psi|)(|\Psi\rangle\langle\Psi|) 
= |\Psi\rangle\langle\Psi| = \hat{\rho}

$$

e.g. :  

$$

|\Psi\rangle = \frac{1}{\sqrt{2}}|\uparrow\rangle + \frac{1}{\sqrt{2}}|\downarrow\rangle

$$

$$

\hat{\rho} = |\Psi\rangle\langle\Psi| 
= \frac{1}{2}\left(|\uparrow\rangle\langle\uparrow| + |\uparrow\rangle\langle\downarrow| 
+ |\downarrow\rangle\langle\uparrow| + |\downarrow\rangle\langle\downarrow|\right)
:= \frac{1}{2} \begin{bmatrix}1 & 1 \\ 1 & 1\end{bmatrix}

$$

$\heartsuit$ for a __mixed state__, we have the density operator  

$$

\hat{\rho} = \sum_j p_j|\Psi_j\rangle\langle\Psi_j|,\qquad
\sum_jp_j = 1

$$

not idempotent  

$$

\begin{align*}
\hat{\rho}^2 &= \left(\sum_j p_j|\Psi_j\rangle\langle\Psi_j|\right)
\left(\sum_k p_k|\Psi_k\rangle\langle\Psi_k|\right) \\
&= \sum_{jk} p_jp_k|\Psi_j\rangle\langle\Psi_j|\Psi_k\rangle\langle\Psi_k| \\
&= \sum_j p_j^2|\Psi_j\rangle\langle\Psi_j| \neq \hat{\rho}
\end{align*}

$$

e.g. :  

$$

\hat{\rho} = \frac{1}{2}(|\uparrow\rangle\langle\uparrow| + |\downarrow\rangle\langle\downarrow|)
:= \frac{1}{2} \begin{bmatrix}1 & 0 \\ 0 & 1\end{bmatrix}

$$

## 2.3 Entangled state
__direct product state__ $\Rightarrow$ $\vert \Psi_{AB}\rangle = \vert \Psi_{A}\rangle \otimes \vert \Psi_{B}\rangle$  
__entangled state__ $\Rightarrow$ $\forall \vert \Psi_{A}\rangle, \vert \Psi_{B}\rangle\in\mathbb{R} \rightarrow \vert \Psi_{AB}\rangle \neq \vert \Psi_{A}\rangle \otimes \vert \Psi_{B}\rangle$  
e.g.:

_Bell states_

$$

|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)

$$

$$

|\Phi^-\rangle = \frac{1}{\sqrt{2}}(|00\rangle - |11\rangle)

$$

$$

|\Psi^+\rangle = \frac{1}{\sqrt{2}}(|01\rangle + |10\rangle)

$$

$$

|\Psi^-\rangle = \frac{1}{\sqrt{2}}(|01\rangle - |10\rangle)

$$

_GHZ state_

$$

|GHZ\rangle = \frac{1}{\sqrt{2}}(|000\rangle + |111\rangle)

$$

_W state_

$$

|W\rangle = \frac{1}{\sqrt{3}}(|100\rangle + |010\rangle + |001\rangle)

$$

---

# C3 - Second Quantization

## 3.1 - Identical particles
__** permutation symmetry **__  
permutation symmetry $\Rightarrow$ $[\hat{H}, \hat{P}_ {ij}] = 0$, where $\hat{P}_ {ij}$ is the permutation operator  
eigenvalue of permutation operator :  

$$

\hat{P}_{ij}^{-1} = \hat{P}_{ij}
\Rightarrow \hat{P}_{ij}^2 = 1
\Rightarrow \lambda = \pm 1

$$

$$

\begin{cases}
\lambda = +1 &\rightarrow \hat{P}_{ij}\psi^S = \psi^S 
&\Rightarrow \text{Bosons }(s=0,\hbar,2\hbar,...) \\
\lambda = -1 &\rightarrow \hat{P}_{ij}\psi^A = -\psi^A 
&\Rightarrow \text{Fermions }(s=\frac{\hbar}{2}, \frac{3\hbar}{2},...)
\end{cases}

$$

__** wavefunction **__  
for Fermions, the wavefunction follows the Pauli exclusion principle  

$$

\Psi_{k_1,\ldots,k_N}(q_1,\ldots,q_N)
= \frac{1}{\sqrt{N!}}
\begin{bmatrix}
\phi_{k_1}(q_1) & \phi_{k_1}(q_2) & \dots & \phi_{k_1}(q_N) \\
\phi_{k_2}(q_1) & \phi_{k_2}(q_2) & \dots & \phi_{k_2}(q_N) \\
\vdots & \vdots & \ddots & \vdots\\
\phi_{k_N}(q_1) & \phi_{k_N}(q_2) & \dots & \phi_{k_N}(q_N) \\
\end{bmatrix}

$$

for Bosons, particles are allowed to be in the same state  

$$

\Psi_{k_1,\ldots,k_N}(q_1,\ldots,q_N)
= \sqrt{\frac{\prod_i n_i!}{N!}}\sum_p\hat{P}
[\phi_{k_1}(q_1)\cdots\phi_{k_1}(q_{n_1})
\phi_{k_2}(q_{n_1+1})\cdots\phi_{k_2}(q_{n_1+n_2})
\cdots+\phi_{k_N}(q_N)]

$$

where $n_{i}$ particles are in $\phi_{k_{i}}$ state, and $\hat{P}$ permutates particles in different states

## 3.2 - Particle number representation
identity of particles $\Rightarrow$ we only need to distinguish between particles in different states  
for Bosons, the wavefunction can be reformulated as  

$$

|\Psi\rangle := |n_1n_2\ldots n_N\rangle

$$

where $n_{i}$ denotes the particle number in the $i$th state  
for Fermions, the wavefunction can be reformulated as  

$$

|\Psi\rangle := |k_1k_2\ldots k_N\rangle

$$

where $k_{i} = 0/1$ denotes the occupation of the $i$th state  

__** harmonoic oscillator (Bosons) **__  
Hamiltian of a one-dimensional harmonic oscillator  

$$

\hat{H} = \frac{1}{2m}\hat{p}_x^2 + \frac{1}{2}m\omega^2\hat{x}^2

$$

define creation and annihilation operator  

$$

\hat{a}^\dagger = \frac{1}{\sqrt{2}} \left(\sqrt{\frac{m\omega}{\hbar}}\hat{x} - i\frac{\hat{p}_x}{\sqrt{m\omega\hbar}}\right), 
\hat{a} = \frac{1}{\sqrt{2}} \left(\sqrt{\frac{m\omega}{\hbar}}\hat{x} + i\frac{\hat{p}_x}{\sqrt{m\omega\hbar}}\right)

$$

we have  

$$

[\hat{a}, \hat{a}^\dagger] = -\frac{i}{2\hbar} [\hat{x},\hat{p}_x] -\frac{i}{2\hbar} [\hat{x},\hat{p}_x] = 1

$$

$$

\hat{x} = \sqrt{\frac{\hbar}{2m\omega}(\hat{a}^\dagger+\hat{a})}, 
\hat{p}_x = \sqrt{\frac{m\omega\hbar}{2}i(\hat{a}^\dagger-\hat{a})}

$$

Hamiltian can be reformulated as  

$$

\hat{H} = (\hat{a}^\dagger\hat{a} + \hat{a}\hat{a}^\dagger) \frac{\hbar\omega}{2} 
= (\hat{a}^\dagger\hat{a} + \frac{1}{2})\hbar\omega

$$

If $\lvert n\rangle$ is an eigenstate of the Hamiltonian with eigenvalue $E_{n}$, then we have

$$

\hat{H}\hat{a}^\dagger|n\rangle 
= \left(\hat{a}^\dagger\hat{a}\hat{a}^\dagger + \frac{1}{2}\hat{a}^\dagger\right) \hbar\omega|n\rangle 
= \hat{a}^\dagger \left(\hat{a}^\dagger\hat{a} + \frac{1}{2} + 1\right) \hbar\omega|n\rangle
= (E_n + \hbar\omega) \hat{a}^\dagger |n\rangle

$$

$$

\hat{H}\hat{a}|n\rangle 
= \left(\hat{a}^\dagger\hat{a}\hat{a} + \frac{1}{2}\hat{a}\right) \hbar\omega|n\rangle 
= \hat{a} \left(\hat{a}^\dagger\hat{a} + \frac{1}{2} - 1\right) \hbar\omega|n\rangle
= (E_n - \hbar\omega) \hat{a} |n\rangle

$$

which shows that $\hat{a}^\dagger\lvert n\rangle$ and $\hat{a}\lvert n\rangle$ are also eigenstates of the Hamiltonian.
For the ground state $\lvert 0\rangle$, we have

$$

\hat{H}\hat{a}|0\rangle = (E_0 - \hbar\omega) \hat{a}|0\rangle

$$

Because the eigenvalue cannot be lowered further, we impose $\hat{a}\lvert 0\rangle = 0$, which means

$$

\hbar\omega\hat{a}^\dagger\hat{a}|0\rangle = \left(\hat{H}-\frac{1}{2}\hbar\omega\right)|0\rangle = 0
\Rightarrow \hat{H}|0\rangle = \frac{1}{2}\hbar\omega|0\rangle

$$

eigenvalue of the ground state $\lvert 0\rangle$ is $E_{0} = (1/2)\hbar\omega$  
then we can get all the eigenvalues and eigenstates of $\hat{H}$  

$$

E_n = \frac{1}{2}\hbar\omega + n\hbar\omega

$$

$$

|n\rangle = \frac{1}{\sqrt{n!}} (\hat{a}^\dagger)^n |0\rangle

$$

__** particle number operator **__  
creation and annihilation operator work as  

$$

\hat{a}^\dagger |n\rangle = \sqrt{n+1} |n+1\rangle

$$

$$

\hat{a} |n\rangle = \sqrt{n} |n-1\rangle

$$

$$

\langle n| \hat{a} = \sqrt{n+1} \langle n+1|

$$

$$

\langle n| \hat{a}^\dagger = \sqrt{n} \langle n-1|

$$

define $\hat{n} = \hat{a}^\dagger \hat{a}$, we have the commutation relations  

$$

[\hat{a}^\dagger, \hat{a}^\dagger] = 0, [\hat{a}, \hat{a}] = 0, [\hat{a}, \hat{a}^\dagger] = 1

$$

$$

[\hat{a}, \hat{n}] = \hat{a}\hat{a}^\dagger\hat{a} - \hat{a}^\dagger\hat{a}\hat{a}
= (\hat{a}\hat{a}^\dagger - \hat{a}^\dagger\hat{a})\hat{a} = [\hat{a}, \hat{a}^\dagger]\hat{a} 
= \hat{a}

$$

$$

[\hat{a}^\dagger, \hat{n}] = \hat{a}^\dagger\hat{a}^\dagger\hat{a} - \hat{a}^\dagger\hat{a}\hat{a}^\dagger = \hat{a}^\dagger(\hat{a}^\dagger\hat{a} - \hat{a}\hat{a}^\dagger) 
= \hat{a}^\dagger[\hat{a}^\dagger, \hat{a}] = -\hat{a}^\dagger

$$

__** $N$-dimensional harmonic oscillator (Bosons) **__  
commutation relations  

$$

[\hat{a}_i^\dagger, \hat{a}_j^\dagger] = 0, [\hat{a}_i, \hat{a}_j] = 0, 
[\hat{a}_i, \hat{a}_j^\dagger] = \delta_{ij}

$$

eigenstates and eigenvalues  

$$

|n_1n_2...n_N\rangle = \frac{1}{\sqrt{\prod_in_i!}} 
\left(\hat{a}_1^\dagger\right)^{n_1} \left(\hat{a}_2^\dagger\right)^{n_2} ...
\left(\hat{a}_N^\dagger\right)^{n_N} |0\rangle

$$

$$

E_{n_1n_2n_N} = \sum_{i=1}^N \left(n_i + \frac{1}{2}\right) \hbar\omega

$$

where $n_{i}$ is the particle number in the $i$th state  
creation and annihilation operators for Bosons behave  

$$

\hat{a}^\dagger_i|n_1n_2...n_i...\rangle = \sqrt{n_i+1}|n_1n_2...(n_i+1)...\rangle

$$

$$

\hat{a}_i|n_1n_2...n_i...\rangle = \sqrt{n_i}|n_1n_2...(n_i-1)...\rangle

$$

$$

\langle...n_i...n_2n_1|\hat{a}_i = \sqrt{n_i+1}\langle...(n_i+1)...n_2n_1|

$$

$$

\langle...n_i...n_2n_1|\hat{a}^\dagger_i = \sqrt{n_i}\langle...(n_i-1)...n_2n_1|

$$

$$

\hat{n}_i|n_1n_2...n_i...\rangle = \hat{a}^\dagger_i\hat{a}_i|n_1n_2...n_i...\rangle
= n_i|n_1n_2...n_i...\rangle

$$

__** Fermions **__  
for Fermions, basis of particle number representation is  

$$

|n_1n_2...n_N\rangle, n_\alpha=0,1

$$

where $n_{\alpha}$ is the occupation number of the $\alpha$th state  
creation and annihilation operators for Fermions behave  

$$

\hat{a}^\dagger_\alpha|n_1n_2...n_\alpha...\rangle = (-1)^{\sum_{\beta=1}^{\alpha-1}n_\beta} |n_1n_2...1_\alpha...\rangle \delta_{n_\alpha0}

$$

$$

\hat{a}_\alpha|n_1n_2...n_\alpha...\rangle = (-1)^{\sum_{\beta=1}^{\alpha-1}n_\beta}|n_1n_2...0_\alpha...\rangle\delta_{n_\alpha1}

$$

$$

\langle...n_\alpha...n_2n_1|\hat{a}_\alpha = (-1)^{\sum_{\beta=1}^{\alpha-1}n_\beta}\langle...1_\alpha...n_2n_1|\delta_{n_\alpha0}

$$

$$

\langle...n_\alpha...n_2n_1|\hat{a}^\dagger_\alpha = (-1)^{\sum_{\beta=1}^{\alpha-1}n_\beta}\langle...0_\alpha...n_2n_1|\delta_{n_\alpha1}

$$

$$

\hat{n}_\alpha|n_1n_2...n_\alpha...\rangle = \hat{a}^\dagger_\alpha\hat{a}_\alpha|n_1n_2...n_\alpha...\rangle = \delta_{n_\alpha1}|n_1n_2...1_\alpha...\rangle

$$

commutation relations  

$$

[\hat{a}_\alpha^\dagger, \hat{a}_\beta^\dagger]_+ = 0, [\hat{a}_\alpha, \hat{a}_\beta]_+ = 0, 
[\hat{a}_\alpha, \hat{a}_\beta^\dagger]_+ = \delta_{\alpha\beta}

$$

## 3.3 - Single and double particle operator of Bosons
__** single-particle operator **__  
in the particle number representation, single particle operator becomes  

$$

\hat{F} = \sum_{ij}f_{ij}\hat{a}_i^\dagger\hat{a}_j, f_{ij} = \langle\psi_i|\hat{f}|\psi_j\rangle

$$

for diagonal element  

$$

\begin{align*}
\bar{\hat{F}} &= \langle...n_l...n_k...|\hat{F}|...n_k...n_l...\rangle \\
&= \sum_{ij}f_{ij} \langle...n_l...n_k...|\hat{a}_i^\dagger\hat{a}_j|...n_k...n_l...\rangle \\
&= \sum_{i}f_{ii} \langle...n_l...n_k...|\hat{a}_i^\dagger\hat{a}_i|...n_k...n_l...\rangle \\
&= \sum_{i}f_{ii} \langle...n_l...n_k...|\hat{n}_i|...n_k...n_l...\rangle \\
&= \sum_{i}f_{ii}n_i
\end{align*}

$$

for single-excitation element  

$$

\begin{align*}
& \langle...(n_l-1)...(n_k+1)...|\hat{F}|...n_k...n_l...\rangle \\
=& \sum_{ij}f_{ij} \langle...(n_l-1)...(n_k+1)...|\hat{a}_i^\dagger\hat{a}_j|...n_k...n_l...\rangle \\
=& \sum_{i}f_{ii} \sqrt{n_k+1}\delta_{ik} \langle...(n_l-1)...n_k...|...n_k...(n_l-1)...\rangle \sqrt{n_l}\delta_{jl} \\
=& f_{kl} \sqrt{(n_k+1)n_l}
\end{align*}

$$

__** double-particle operator **__  
in the particle number representation, double particle operator becomes  

$$

\hat{G} = \frac{1}{2}\sum_{i'j'ij}g_{i'j'ji}\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}\hat{a}_j\hat{a}_i,
g_{i'j'ji} = \langle\psi_{i'}(1)\psi_{j'}(2)|\hat{g}(1,2)|\psi_j(2)\psi_i(1)\rangle

$$

from the symmetry $\hat{g}(a,b) = \hat{g}(b,a)$, we have  

$$

g_{i'j'ji} = \langle\psi_{i'}(1)\psi_{j'}(2)|\hat{g}(1,2)|\psi_j(2)\psi_i(1)\rangle 
= \langle\psi_{i'}(2)\psi_{j'}(1)|\hat{g}(2,1)|\psi_j(1)\psi_i(2)\rangle = g_{j'i'ij}

$$

 
for diagonal element  

$$

\begin{align*}
\langle...n_j...n_i...|\hat{G}|...n_i...n_j...\rangle =& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...n_j...n_i...|\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}\hat{a}_j\hat{a}_i|...n_i...n_j...\rangle \\
+& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...n_i...|\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}\hat{a}_j\hat{a}_i|...n_i...\rangle
\end{align*}

$$

$$

\begin{align*}
& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...n_j...n_i...|\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}
\hat{a}_j\hat{a}_i|...n_i...n_j...\rangle \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...n_j...n_i...|\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}
|...(n_i-1)...(n_j-1)...\rangle \sqrt{n_in_j} \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...(n_j-1)...(n_i-1)...|...(n_i-1)...(n_j-1)...\rangle (\delta_{ii'}\delta_{jj'} + \delta_{ij'}\delta_{ji'}) n_in_j \\
=& \frac{1}{2} \sum_{ij} (g_{ijji} + g_{jiji}) n_in_j
\end{align*}

$$

$$

\begin{align*}
& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...n_i...|\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}\hat{a}_j\hat{a}_i|...n_i...\rangle \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...n_i...|\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}
|...(n_i-2)...\rangle \delta_{ij} \sqrt{n_i(n_i-1)} \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...(n_i-2)...|...(n_i-2)...\rangle \delta_{ii'}\delta_{ij'} \delta_{ij} n_i(n_i-1) \\
=& \frac{1}{2} \sum_{i} n_i(n_i-1) g_{iiii}
\end{align*}

$$

$$

\bar{\hat{G}} = \frac{1}{2}\sum_{ij}n_in_j(g_{ijji}+g_{jiji}) + \frac{1}{2}\sum_{i}n_i(n_i-1)g_{iiii}

$$

for double excitation $(k,l)\rightarrow(a,b)$  

$$

\begin{align*}
& \langle...(n_b+1)...(n_a+1)...(n_l-1)...(n_k-1)...|\hat{G}|...n_k...n_l...n_a...n_b...\rangle \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...(n_b+1)...(n_a+1)...(n_l-1)...(n_k-1)...|\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}\hat{a}_j\hat{a}_i|...n_k...n_l...n_a...n_b...\rangle \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \sqrt{(n_b+1)(n_a+1)}\sqrt{n_kn_l} (\delta_{i'b}\delta_{j'a} + \delta_{i'a}\delta_{j'b}) (\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk}) \\
& \langle...n_b...n_a...(n_l-1)...(n_k-1)...|...(n_k-1)...(n_l-1)...n_a...n_b...\rangle \\
=& \frac{1}{2} \sum_{ij} \sqrt{(n_b+1)(n_a+1)n_kn_l} (g_{baji} + g_{abji}) (\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk}) \\
=& \frac{1}{2} \sqrt{(n_b+1)(n_a+1)n_kn_l} (g_{balk} + g_{ablk} + g_{bakl} + g_{abkl}) \\
=& (g_{ablk} + g_{abkl}) \sqrt{(n_b+1)(n_a+1)n_kn_l} 
\end{align*}

$$

for double excitation $(k,l)\rightarrow(a,a)$  

$$

\begin{align*}
& \langle...(n_a+2)...(n_l-1)...(n_k-1)...|\hat{G}|...n_k...n_l...n_a...\rangle \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...(n_a+2)...(n_l-1)...(n_k-1)...|\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}\hat{a}_j\hat{a}_i|...n_k...n_l...n_a...\rangle \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \sqrt{(n_a+2)(n_a+1)}\sqrt{n_kn_l} \cdot \delta_{i'a}\delta_{j'a} (\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk}) \\
& \langle...n_a...(n_l-1)...(n_k-1)...|...(n_k-1)...(n_l-1)...n_a...\rangle \\
=& \frac{1}{2} \sum_{ij} \sqrt{(n_a+2)(n_a+1)n_kn_l} \cdot g_{aaji}(\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk}) \\
=& \frac{1}{2} \sqrt{(n_a+2)(n_a+1)n_kn_l} (g_{aalk} + g_{aakl}) \\
=& g_{aalk} \sqrt{(n_a+2)(n_a+1)n_kn_l}
\end{align*}

$$

for double excitation $(k,k)\rightarrow(a,b)$  

$$

\begin{align*}
& \langle...(n_b+1)...(n_a+1)...(n_k-2)...|\hat{G}|...n_k...n_a...n_b...\rangle \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...(n_b+1)...(n_a+1)...(n_k-2)...|\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}\hat{a}_j\hat{a}_i|...n_k...n_a...n_b...\rangle \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \sqrt{(n_b+1)(n_a+1)n_k(n_k-1)} \cdot (\delta_{i'b}\delta_{j'a} + \delta_{i'a}\delta_{j'b}) \delta_{ik}\delta_{jk} \\
& \langle...n_b...n_a...(n_k-2)...|...(n_k-2)...n_a...n_b...\rangle \\
=& \frac{1}{2} \sum_{ij} \sqrt{(n_b+1)(n_a+1)n_k(n_k-1)} \cdot (g_{baji} + g_{abji}) \delta_{ik}\delta_{jk} \\
=& \frac{1}{2} \sqrt{(n_b+1)(n_a+1)n_k(n_k-1)} \cdot (g_{bakk} + g_{abkk}) \\
=& g_{abkk} \sqrt{(n_b+1)(n_a+1)n_k(n_k-1)}
\end{align*}

$$

for double excitation $(k,k)\rightarrow(a,a)$  

$$

\begin{align*}
& \langle...(n_a+2)...(n_k-2)...|\hat{G}|...n_k...n_a...\rangle \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \langle...(n_a+2)...(n_k-2)...|\hat{a}^\dagger_{i'}\hat{a}^\dagger_{j'}\hat{a}_j\hat{a}_i|...n_k...n_a...\rangle \\
=& \frac{1}{2} \sum_{i'j'ij}g_{i'j'ji} \sqrt{(n_a+2)(n_a+1)n_k(n_k-1)} \cdot \delta_{i'a}\delta_{j'a} \delta_{ik}\delta_{jk} \\
& \langle...n_a...(n_k-2)...|...(n_k-2)...n_a...\rangle \\
=& \frac{1}{2} \sqrt{(n_a+2)(n_a+1)n_k(n_k-1)} \cdot g_{aakk}
\end{align*}

$$

## 3.4 - Single and double particle operator of Fermions
__** single-particle operator **__  
for diagonal element  

$$

\begin{align*}
\bar{\hat{F}} &= \langle...n_\alpha...|\hat{F}|...n_\alpha...\rangle \\
&= \sum_{\alpha\beta}f_{\alpha\beta} \langle...n_\alpha...|\hat{a}_\alpha^\dagger\hat{a}_\beta|...n_\alpha...\rangle \\
&= \sum_{\alpha}f_{\alpha\alpha} \langle...n_\alpha...|\hat{a}_\alpha^\dagger\hat{a}_\alpha|...n_\alpha...\rangle \\
&= \sum_{\alpha}f_{\alpha\alpha} \langle...n_\alpha...|\hat{n}_\alpha|...n_\alpha...\rangle \\
&= \sum_{\alpha}f_{\alpha\alpha} \delta_{n_\alpha1} 
\end{align*}

$$

for single-excitation element  

$$

\begin{align*}
& \langle...0_\gamma...1_a...|\hat{F}|...0_a...1_\gamma...\rangle \text{    }(\gamma > a) \\
=& \sum_{\alpha\beta}f_{\alpha\beta} \langle...0_\gamma...1_a...|\hat{a}_\alpha^\dagger\hat{a}_\beta|...0_a...1_\gamma...\rangle \\
=& \sum_{\alpha\beta}f_{\alpha\beta} (-1)^{\sum_{i=1}^{a-1}n_i} (-1)^{\sum_{i=1}^{\gamma-1}n_i} \delta_{a\alpha}\delta_{\gamma\beta} \langle...0_\gamma...0_a...|...0_a...0_\gamma...\rangle \\
=& f_{a\gamma} (-1)^{\sum_{i=a+1}^{\gamma-1}n_i}
\end{align*}

$$

__** Wick's theorem **__  
define the __Fock vacuum__ which consists of $N$ fermions  

$$

|\rangle = |ijk...\rangle = \prod_{i\leq N} \hat{a}_i^\dagger |0\rangle

$$

From the relations $\hat{a}_ {a}\lvert\rangle = 0$ and $\hat{a}_ {i}^\dagger\lvert\rangle = 0$, we can define the quasi-particle operator

$$

\hat{\alpha}_a^\dagger = \hat{a}_a^\dagger \qquad \hat{\alpha}_a = \hat{a}_a \\
\hat{\alpha}_i^\dagger = \hat{a}_i \qquad \hat{\alpha}_i = \hat{a}_i^\dagger

$$

where we have the relation $\hat{\alpha}_{\nu} \lvert\rangle = 0$  
in the __normal product__, the creation operators of quasi-particle should be in the left of the annihilation operators, e.g. :  

$$

\{\hat{a}_a^\dagger\hat{a}_i^\dagger\hat{a}_j\hat{a}_b\} = -\hat{a}_a^\dagger\hat{a}_j\hat{a}_i^\dagger\hat{a}_b

$$

the diagonal element of normal product for Fock vacuum should be zero  

$$

\langle|\{AB...\}|\rangle = \langle|...\hat{\alpha}_\nu|\rangle = 0

$$

 
define __contraction__ as the diagonal element of the operator  

$$

\acute{A}\grave{B} = \langle|AB|\rangle

$$

note that ```\acute``` and ```\grave``` are used for Wick contraction due to ```Markdown``` environment  
we can notice that contraction should be made between creation and annihilation operators  

$$

\acute{\hat{a}_\mu^\dagger}\grave{\hat{a}_\nu^\dagger} = \langle|\hat{a}_\mu^\dagger\hat{a}_\nu^\dagger|\rangle = 0 \qquad \acute{\hat{a}_\mu}\grave{\hat{a}_\nu} = \langle|\hat{a}_\mu\hat{a}_\nu|\rangle = 0

$$

the Wick's theorem goes  

$$

\begin{align*}
ABCD... &= \{ABCD...\} &\text{no contraction} \\
&+ \{\acute{A}\grave{B}CD...\} + \{A\acute{B}\grave{C}D...\} + ... &\text{one contraction} \\
&+ \{\acute{A}\grave{B}\acute{C}\grave{D}...\} + ... &\text{two contraction} \\
&+ ... + \{\acute{A}\grave{B}\acute{C}\grave{D}\acute{E}\grave{F}...\} &\text{more contractions}
\end{align*}

$$

for two-body interactions  

$$

\begin{align*}
\hat{a}_{\alpha'}^\dagger\hat{a}_{\beta'}^\dagger\hat{a}_\beta\hat{a}_\alpha
&= \langle|\hat{a}_{\alpha'}^\dagger\hat{a}_\alpha|\rangle \langle|\hat{a}_{\beta'}^\dagger\hat{a}_\beta|\rangle - \langle|\hat{a}_{\alpha'}^\dagger\hat{a}_\beta|\rangle \langle|\hat{a}_{\beta'}^\dagger\hat{a}_\alpha|\rangle \\
&+ \langle|\hat{a}_{\alpha'}^\dagger\hat{a}_\alpha|\rangle \{\hat{a}_{\beta'}^\dagger\hat{a}_\beta\} + \langle|\hat{a}_{\beta'}^\dagger\hat{a}_\beta|\rangle \{\hat{a}_{\alpha'}^\dagger\hat{a}_\alpha\} \\
&- \langle|\hat{a}_{\alpha'}^\dagger\hat{a}_\beta|\rangle \{\hat{a}_{\beta'}^\dagger\hat{a}_\alpha\} - \langle|\hat{a}_{\beta'}^\dagger\hat{a}_\alpha|\rangle \{\hat{a}_{\alpha'}^\dagger\hat{a}_\beta\} \\
&+ \{\hat{a}_{\alpha'}^\dagger\hat{a}_{\beta'}^\dagger\hat{a}_\beta\hat{a}_\alpha\}
\end{align*}

$$

__** double-particle operator **__  

$$

\begin{align*}
\langle|\hat{G}|\rangle &= \frac{1}{2}\sum_{\alpha\beta\alpha'\beta'}g_{\alpha'\beta'\beta\alpha}\langle|\hat{a}_{\alpha'}^\dagger\hat{a}_{\beta'}^\dagger\hat{a}_\beta\hat{a}_\alpha|\rangle \\
&= \frac{1}{2}\sum_{\alpha\beta\alpha'\beta'}g_{\alpha'\beta'\beta\alpha} \left(\langle|\hat{a}_{\alpha'}^\dagger\hat{a}_\alpha|\rangle \langle|\hat{a}_{\beta'}^\dagger\hat{a}_\beta|\rangle - \langle|\hat{a}_{\alpha'}^\dagger\hat{a}_\beta|\rangle \langle|\hat{a}_{\beta'}^\dagger\hat{a}_\alpha|\rangle\right) \\
&= \frac{1}{2}\sum_{\alpha \neq \beta} n_\alpha n_\beta (g_{\alpha\beta\beta\alpha} - g_{\beta\alpha\beta\alpha})
\end{align*}

$$
