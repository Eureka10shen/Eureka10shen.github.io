---
layout:     post
title:      Notes for advanced quantum mechanics
subtitle:   On quantum
date:       2022-09-15
author:     Eureka10shen
header-img: img/quantum.jpg
catalog: false
tags:
    - Quantum
---


shen's notes on advanced quantum mechanics  
2895044375@qq.com

---
reference books : 

---

# C1 -- Mathematical Fundamentals and Physical Principles

## 1.1 Basic principles of quantum mechanics

(1) state of a microsystem <--> vector in a __Hilbert space__  
$$|\Psi\rangle = \sum_{i=1}^N c_i|\psi_i\rangle$$
$$|\Psi\rangle := [c_1, c_2, ..., c_N]^\top, \langle\Psi| := [c_1, c_2, ..., c_N]$$
(2) physical quantity of a microsystem <--> __Hermite operatror__ in Hilbert space  
$$\hat{O}|\psi_i\rangle = \lambda_i|\psi_i\rangle$$ 
$$\langle\hat{O}\rangle = \langle\Psi|\hat{O}|\Psi\rangle 
= \langle\sum_{i=1}^Nc_i\psi_i|\hat{O}|\sum_{j=1}^Nc_j\psi_j\rangle
= \sum_{ij}c_ic_j\langle\psi_i|\hat{O}|\psi_j\rangle
= \sum_{ij}c_ic_j\lambda_i\delta_{ij} = \sum_i|c_i|^2\lambda_i$$
(3) commutation between location operator and momentum operator  
$$[\mathbf{x_i}, \mathbf{x_j}] = [\mathbf{p_i}, \mathbf{p_j}] = 0$$
$$[\mathbf{x_i}, \mathbf{p_j}] = i\hbar\delta_{ij}$$
(4) evolution of the state of a microsystem --> Schr$\ddot{\text{o}}$dinger equation  
$$i\hbar\frac{\partial|\Psi(t)\rangle}{\partial t} = \hat{H}|\Psi(t)\rangle$$
(5) symmetry of identical particles --> symmetrical (Boson), antisymmetrical (Fermi)
$$|\Psi(..., \mathbf{q_i}, ..., \mathbf{q_j}, ...)\rangle = \pm|\Psi(..., \mathbf{q_j}, ..., \mathbf{q_i}, ...)\rangle$$

## 1.2 Hilbert space
__vector space__ : a set $\mathcal{H} = \{\psi. \phi, ...\}$ where all elements satisfy the rules  
(1) additon --> $\forall \psi, \phi \in \mathcal{H}$, $\chi = \psi + \phi \in \mathcal{H}$  
(2) multiplication --> $\forall a\in\mathbb{C}$ and $\psi\in\mathcal{H}$, $\chi = a\psi\in\mathcal{H}$  
(3) inner product --> $\forall \psi,\phi\in\mathcal{H}$, $(\psi, \phi) = C \in \mathbb{C}$

__basis vector__ : an orthogonal complete set of the vector space  
projection onto basis vector $|\psi_i\rangle$ --> $|\psi_i\rangle\langle\psi_i|$
--> $\sum_i|\psi_i\rangle\langle\psi_i| = 1$
$$\langle\Phi|\Psi\rangle = \left(\sum_i\langle\Phi|\psi_i\rangle\langle\psi_i|\right)|\Psi\rangle
= \sum_i\langle\Phi|\psi_i\rangle\langle\psi_i|\Psi\rangle$$

__complete space__ : for all __Cauchy sequence__ $\{S_n\}$ in the vector space, $\{S_n\}$ converges to a vector in the space  
Cauchy sequence $\{S_n\}$ --> $\forall\varepsilon>0, \exist N, s.t. \forall m,n>N\Rightarrow|S_n-S_m|<\varepsilon$

__Hilbert space__ : infinite-dimensional complete vector space  
conjugate space : ket --> $|\psi\rangle \in \mathcal{H}$, bra --> $\langle\psi| \in \mathcal{H}^*$ --> $\langle\psi| = |\psi\rangle^*$  

## 1.3 Operator
__operator__ : transformation between vectors in Hilbert space  
$$\forall |\psi\rangle \in \mathcal{H}, \hat{O}|\psi\rangle = |\phi\rangle \in \mathcal{H}$$
$$\hat{O} \{|\psi\rangle+|\phi\rangle\} = \hat{O}|\psi\rangle + \hat{O}|\phi\rangle$$
conjugate of an operator -->
$\langle\psi|\hat{A}^\dagger|\phi\rangle = (\langle\psi|\hat{A}^\dagger)|\phi\rangle
= (\hat{A}|\psi\rangle)^*(\langle\phi|)^* = \langle\phi|\hat{A}|\psi\rangle^*$  
Harmite operator --> $\hat{A}^\dagger = \hat{A}$  
unitrary operator --> $\hat{U}^{-1} = \hat{U}^\dagger$

__eigenvalue__
$$\hat{A}|\psi_i\rangle = a_i|\psi_i\rangle, \hat{A}\langle\psi_i| = a_i'\langle\psi_i|$$
linear operator --> left and right eigenvalue spectrums are identical  
Hermite operator --> eigenvalues are real, eigenvectors of different eigenvalues are orthogonal

__projective operator__ --> $\hat{P_S}|\psi\rangle = |\psi_S\rangle \in \mathcal{S} \subset \mathcal{H}, \forall |\psi\rangle \in\mathcal{H}$  
(1) idempotent --> $\hat{P_S}^2 = \hat{P_S}$  
_Proof_ : 
$$\hat{P_S}^2|\psi\rangle = \hat{P_S}|\psi_S\rangle = |\psi_S\rangle$$  
(2) eigenvalues of $\hat{P_S}$ are 0 and 1, eigenvectors span the whole Hilbert space $\mathcal{H} = \mathcal{S} + \mathcal{S'}$  
_Proof_ : 
$$\hat{P_S}|\psi_S\rangle = |\psi_S\rangle \Rightarrow (\hat{P_S}-1)|\psi_S\rangle = 0, 
\forall|\psi_S\rangle\in\mathcal{S}$$
$$\hat{P_S}|\psi_{S'}\rangle = 0 \Rightarrow (\hat{P_S}-0)|\psi_{S'}\rangle = 0, 
\forall|\psi_{S'}\rangle\in\mathcal{S'}$$
$$|\psi\rangle = |\psi_S\rangle + |\psi_{S'}\rangle, \forall|\psi\rangle\in\mathcal{H}$$
(3) $\hat{P} = |\psi_i\rangle\langle\psi_i|$ is a projective operator  
_Proof_ : 
$$\forall |\Psi\rangle \in\mathcal{H}, \hat{P}|\Psi\rangle = |\psi_i\rangle\langle\psi_i|\Psi\rangle = c_i|\psi_i\rangle$$

## 1.4 Representation theory
__matrix representation__ --> in the basis $\{|\psi_i\rangle\}$, we have  
$\diamonds$ _ket_
$$|\Psi\rangle = \sum_i|\psi_i\rangle\langle\psi_i|\Psi\rangle 
= \begin{bmatrix}|\psi_1\rangle & |\psi_2\rangle & \dots & |\psi_N\rangle\end{bmatrix}
\begin{bmatrix}c_1 \\ c_2 \\ \vdots \\ c_N\end{bmatrix}
:= \begin{bmatrix}c_1 \\ c_2 \\ \vdots \\ c_N\end{bmatrix}$$
$\hearts$ _bra_
$$\langle\Psi| = \sum_i\langle\Psi|\psi_i\rangle\langle\psi_i| 
= \begin{bmatrix}c_1^* & c_2^* & \dots & c_N^*\end{bmatrix}
\begin{bmatrix}|\psi_1\rangle \\ |\psi_2\rangle \\ \vdots \\ |\psi_N\rangle\end{bmatrix}
:= \begin{bmatrix}c_1^* & c_2^* & \dots & c_N^*\end{bmatrix}$$
$\clubs$ _inner product_
$$\begin{align*}
\langle\Psi|\Phi\rangle 
&= \sum_i\langle\Psi|\psi_i\rangle\langle\psi_i| \sum_j|\psi_j\rangle\langle\psi_j|\Phi\rangle 
= \sum_{ij} \langle\Psi|\psi_i\rangle\langle\psi_i|\psi_j\rangle\langle\psi_j|\Phi\rangle \\
&= \sum_i \langle\Psi|\psi_i\rangle\langle\psi_i|\Phi\rangle 
= \begin{bmatrix}c_1^* & c_2^* & \dots & c_N^*\end{bmatrix}
\begin{bmatrix}c_1 \\ c_2 \\ \vdots \\ c_N\end{bmatrix}
\end{align*}$$
$\spades$ _operator_
$$\begin{align*}
\hat{A}|\Psi\rangle 
&= \sum_{ij}|\psi_i\rangle\langle\psi_i| \left(\hat{A}|\psi_j\rangle\langle\psi_j|\Psi\rangle\right) 
= \sum_{ij}|\psi_i\rangle \left(\langle\psi_i|\hat{A}|\psi_j\rangle\right)\langle\psi_j|\Psi\rangle \\
&= \begin{bmatrix}|\psi_1\rangle & |\psi_2\rangle & \dots & |\psi_N\rangle\end{bmatrix}
\begin{bmatrix}
\langle\psi_1|\hat{A}|\psi_1\rangle & \langle\psi_1|\hat{A}|\psi_2\rangle & \dots & \langle\psi_1|\hat{A}|\psi_N\rangle \\
\langle\psi_2|\hat{A}|\psi_1\rangle & \langle\psi_2|\hat{A}|\psi_2\rangle & \dots & \langle\psi_2|\hat{A}|\psi_N\rangle \\
\vdots & \vdots & \ddots & \vdots\\
\langle\psi_N|\hat{A}|\psi_1\rangle & \langle\psi_N|\hat{A}|\psi_2\rangle & \dots & \langle\psi_N|\hat{A}|\psi_N\rangle \\
\end{bmatrix}
\begin{bmatrix}c_1 \\ c_2 \\ \vdots \\ c_N\end{bmatrix}
\end{align*}$$

__representation transformation__  
in the basis $\{|\psi_i\rangle\}$, we have
$$|\Psi\rangle = \sum_i|\psi_i\rangle\langle\psi_i|\Psi\rangle 
:= \begin{bmatrix}c_1 & c_2 & \dots & c_N\end{bmatrix}^\top$$
in the basis $\{|\phi_i\rangle\}$, we have
$$|\Psi\rangle = \sum_i|\phi_i\rangle\langle\phi_i|\Psi\rangle 
:= \begin{bmatrix}b_1 & b_2 & \dots & b_N\end{bmatrix}^\top$$
transformation from basis $\{|\phi_i\rangle\}$ to basis $\{|\psi_i\rangle\}$
$$\langle\psi_i|\Psi\rangle = \sum_j\langle\psi_i|\phi_j\rangle\langle\phi_j|\Psi\rangle$$
$$\begin{bmatrix}c_1 \\ c_2 \\ \vdots \\ c_N\end{bmatrix}
= \begin{bmatrix}
\langle\psi_1|\phi_1\rangle & \langle\psi_1|\phi_2\rangle & \dots & \langle\psi_1|\phi_N\rangle \\
\langle\psi_2|\phi_1\rangle & \langle\psi_2|\phi_2\rangle & \dots & \langle\psi_2|\phi_N\rangle \\
\vdots & \vdots & \ddots & \vdots\\
\langle\psi_N|\phi_1\rangle & \langle\psi_N|\phi_2\rangle & \dots & \langle\psi_N|\phi_N\rangle \\
\end{bmatrix}
\begin{bmatrix}b_1 \\ b_2 \\ \vdots \\ b_N\end{bmatrix}
:= \hat{U}_{\phi\to\psi}\begin{bmatrix}b_1 \\ b_2 \\ \vdots \\ b_N\end{bmatrix}$$
$$\langle\psi_i|\hat{A}|\psi_j\rangle 
= \sum_{kl}\langle\psi_i|\phi_k\rangle\langle\phi_k|\hat{A}|\phi_l\rangle\langle\phi_l|\psi_j\rangle$$
$$
\begin{bmatrix}
\langle\psi_1|\hat{A}|\psi_1\rangle & \dots & \langle\psi_1|\hat{A}|\psi_N\rangle \\
\vdots & \ddots & \vdots\\
\langle\psi_N|\hat{A}|\psi_1\rangle & \dots & \langle\psi_N|\hat{A}|\psi_N\rangle \\
\end{bmatrix} :=
\hat{U}_{\phi\to\psi}
\begin{bmatrix}
\langle\phi_1|\hat{A}|\phi_1\rangle & \dots & \langle\phi_1|\hat{A}|\phi_N\rangle \\
\vdots & \ddots & \vdots\\
\langle\phi_N|\hat{A}|\phi_1\rangle & \dots & \langle\phi_N|\hat{A}|\phi_N\rangle \\
\end{bmatrix}
\hat{U}_{\psi\to\phi}
$$
_axiom_ : representation transformations are unitary transformation  
_Proof_ :
$$\begin{bmatrix}b_1 \\ b_2 \\ \vdots \\ b_N\end{bmatrix} 
= \hat{U}_{\phi\to\psi}^{-1} \begin{bmatrix}c_1 \\ c_2 \\ \vdots \\ c_N\end{bmatrix}
= \hat{U}_{\psi\to\phi} \begin{bmatrix}c_1 \\ c_2 \\ \vdots \\ c_N\end{bmatrix}$$
$$\hat{U}_{\psi\to\phi}^\dagger = [(\langle\phi_i|\psi_j\rangle)^*]^\top
= [(\langle\phi_j|\psi_i\rangle)^*] = [\langle\psi_i|\phi_j\rangle] = \hat{U}_{\phi\to\psi}$$
$$\hat{U}_{\psi\to\phi}^\dagger = \hat{U}_{\psi\to\phi}^{-1}$$
