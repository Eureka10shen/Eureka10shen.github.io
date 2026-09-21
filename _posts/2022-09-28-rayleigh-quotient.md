---
title: "Rayleigh Quotient"
date: 2022-09-28 17:38:00 +0800
categories:
  - numerical-analysis
excerpt: "A review of conjugate transposes, Hermitian matrices, Rayleigh quotients, and their connection to eigenvalue problems."
mathjax: true
original_url: "https://www.cnblogs.com/Eureka10shen/articles/16739002.html"
permalink: /blog/rayleigh-quotient/
---

> This article was migrated from [Eureka10shen on 博客园]({{ page.original_url }}). The original publication date was 2022-09-28.
---

## conjugate transpose

considering a real vector $\mathbf{x}=[x_ {1},x_ {2},...,x_ {n}]^\top$, we define the 2-norm of the vector as  

$$

\Vert\mathbf{x}\Vert^2 = \mathbf{x}^\top\mathbf{x} = x_1^2+x_2^2+...+x_n^2

$$

for a complex vector $\mathbf{z}=[z_ {1},z_ {2},...,z_ {n}]^\top$, the 2-norm is defined as  

$$

\Vert\mathbf{z}\Vert^2 = \mathbf{z}^\dagger\mathbf{z} = z_1^*z_1+z_2^*z_2+...+z_n^*z_n

$$

where $\dagger$ denotes the _conjugate transpose_ of a vector (matrix), for example  

$$

\mathbf{A}=\begin{bmatrix} 1 & i \\ 0 & 1+i \end{bmatrix} \Rightarrow 
\mathbf{A}^\dagger=\begin{bmatrix} 1 & 0 \\ -i & 1-i \end{bmatrix}

$$

and they have the property  

$$

(\mathbf{u}^\dagger\mathbf{v})^\dagger = \mathbf{v}^\dagger\mathbf{u}

$$

## Hermitian matrix

for a square matrix $\mathbf{A}_ {n\times n}$ with $n$ linearly independent eigenvectors $\mathbf{x}_ {1}$, $\mathbf{x}_ {2}$, ..., $\mathbf{x}_ {n}$, we have  

$$

\mathbf{A}\mathbf{x}_i = \lambda_i\mathbf{x}_i \Rightarrow 
\mathbf{A}\begin{bmatrix} \mathbf{x}_1 & \mathbf{x}_2 & \cdots & \mathbf{x}_n \end{bmatrix}
= \begin{bmatrix} \mathbf{x}_1 & \mathbf{x}_2 & \cdots & \mathbf{x}_n \end{bmatrix}
\begin{bmatrix} \lambda_1 & & & \\ & \lambda_2 & & \\ & & \ddots & \\ & & & \lambda_n \end{bmatrix}

$$

Let the columns of X be x₁, x₂, …, xₙ; then  

$$

\mathbf{X}^{-1}\mathbf{AX} = \begin{bmatrix} \lambda_1 & & & \\ & \lambda_2 & & \\ & & \ddots & \\ & & & \lambda_n \end{bmatrix} := \Lambda

$$

for a real symmetrical matrix $\mathbf{S}_ {n\times n}$, its eigenvectors of different eigenvalues are orthogonal  

$$

\mathbf{x}_i^\top\mathbf{x}_j=0 \quad \forall \lambda_i\neq\lambda_j, \mathbf{x}_i^\top\mathbf{x}_i = 1 
\Rightarrow \mathbf{X}^\top\mathbf{X}=\mathbf{I} \Rightarrow \mathbf{X}^\top=\mathbf{X}^{-1}

$$

for a complex symmetrical matrix $\mathbf{S}_ {n\times n}$, we have $\mathbf{S}^\dagger=\mathbf{S}$, and we call it the _Hermitian matrix_  
>it is easy to prove that  
(1) eigenvalues of Hermitian matrix are all real  
(2) eigenvectors of different eigenvalues are orthogonal  
(3) $\mathbf{z^\dagger Sz}$ is real for all complex vector $\mathbf{z}$

## Rayleigh theorem
define _Rayleigh quitient_ as  

$$

R(\mathbf{A}, \mathbf{x}) = \frac{\mathbf{x}^\dagger\mathbf{Ax}}{\mathbf{x}^\dagger\mathbf{x}}

$$

where $\mathbf{x}$ is a non-zero vector, $\mathbf{A}$ is a Hermitian matrix  
the _Rayleigh theorem_ tells that  
>(1) eigenvectors of $\mathbf{A}$ are critical points of $R(\mathbf{A}, \mathbf{x})$  
(2) extreme values of $R(\mathbf{A}, \mathbf{x})$ equals to extreme eigenvalues of $\mathbf{A}$ $\left(\lambda_ {\min} \leq R(\mathbf{A}, \mathbf{x}) \leq \lambda_ {\max}\right)$

__`Proof`__ :  
according to property (3) of Hermitian matrix, $\mathbf{x^\dagger Ax}$ is real; obviously $\mathbf{x^\dagger x}$ is real, so $R(\mathbf{A}, \mathbf{x})$ is real  
for critical points of $R$  

$$

\frac{\text{d}R(\mathbf{x})}{\text{d}\mathbf{x}} = \mathbf{0}^\top

$$

let $\mathbf{x}=\mathbf{x}^R+i\mathbf{x}^I$, we have  

$$

\frac{\text{d}R(\mathbf{x})}{\text{d}\mathbf{x}} = \frac{\text{d}R(\mathbf{x})}{\text{d}\mathbf{x}^R} + i\frac{\text{d}R(\mathbf{x})}{\text{d}\mathbf{x}^I}

$$

then goes  

$$

\frac{\text{d}R(\mathbf{x})}{\text{d}\mathbf{x}^R} = \frac{\text{d}R(\mathbf{x})}{\text{d}\mathbf{x}^I} = \mathbf{0}^\top

$$

for the "real" term  

$$

\begin{align*}
\frac{\text{d}R(\mathbf{x})}{\text{d}\mathbf{x}^R} &=
\frac{\text{d}}{\text{d}\mathbf{x}^R} \left(\frac{\mathbf{x^\dagger Ax}}{\mathbf{x^\dagger x}}\right) \\
&= \frac{1}{(\mathbf{x^\dagger x})^2} \left(\frac{\text{d}(\mathbf{x^\dagger Ax})}{\text{d}\mathbf{x}^R}\mathbf{x^\dagger x} - \mathbf{x^\dagger Ax} \frac{\text{d}(\mathbf{x^\dagger x})}{\text{d}\mathbf{x}^R}\right) \\
&= \frac{1}{\mathbf{x^\dagger x}} \left(\frac{\text{d}(\mathbf{x^\dagger Ax})}{\text{d}\mathbf{x}^R} - R(\mathbf{x}) \frac{\text{d}(\mathbf{x^\dagger x})}{\text{d}\mathbf{x}^R}\right) \\
&= \frac{1}{\mathbf{x^\dagger x}} \left(\mathbf{x^\dagger A}\frac{\text{d}\mathbf{x}}{\text{d}\mathbf{x}^R} + \mathbf{x^\top A^\top}\frac{\text{d}\mathbf{x}^*}{\text{d}\mathbf{x}^R} - R(\mathbf{x})\mathbf{x}^\dagger\frac{\text{d}\mathbf{x}}{\text{d}\mathbf{x}^R} - R(\mathbf{x})\mathbf{x}^\top\frac{\text{d}\mathbf{x}^*}{\text{d}\mathbf{x}^R}\right) \\
&= \frac{1}{\mathbf{x^\dagger x}} \left(\mathbf{x^\dagger A} + \mathbf{x^\top A^\top} - R(\mathbf{x})\mathbf{x}^\dagger - R(\mathbf{x})\mathbf{x}^\top\right) \\
&= \frac{1}{\mathbf{x^\dagger x}} \left(\mathbf{x^\dagger A} + (\mathbf{x^\dagger A^\dagger})^* - R(\mathbf{x})\mathbf{x}^\dagger - R(\mathbf{x})(\mathbf{x}^\dagger)^*\right) \\
&= \frac{1}{\mathbf{x^\dagger x}} \left(\mathbf{x^\dagger A} + (\mathbf{x^\dagger A})^* - 2R(\mathbf{x})\mathbf{x}^\dagger_R\right) \\
&= \frac{2(\mathbf{x^\dagger A})_R - 2R(\mathbf{x})\mathbf{x}^\dagger_R}{\mathbf{x^\dagger x}} 
= \mathbf{0}^\top = \mathbf{0}^\dagger
\end{align*}

$$

it follows  

$$

\begin{align*}
\mathbf{0} &= [(\mathbf{x^\dagger A})_R - R(\mathbf{x})\mathbf{x}^\dagger_R]^\dagger \\
&= (\mathbf{A^\dagger x})_R - R(\mathbf{x})\mathbf{x}_R \\
&= (\mathbf{Ax})_R - R(\mathbf{x})\mathbf{x}_R
\end{align*}

$$

for the "imagionary" term  

$$

\begin{align*}
\frac{\text{d}R(\mathbf{x})}{\text{d}\mathbf{x}^I} &=
\frac{\text{d}}{\text{d}\mathbf{x}^I} \left(\frac{\mathbf{x^\dagger Ax}}{\mathbf{x^\dagger x}}\right) \\
&= \frac{1}{(\mathbf{x^\dagger x})^2} \left(\frac{\text{d}(\mathbf{x^\dagger Ax})}{\text{d}\mathbf{x}^I}\mathbf{x^\dagger x} - \mathbf{x^\dagger Ax} \frac{\text{d}(\mathbf{x^\dagger x})}{\text{d}\mathbf{x}^I}\right) \\
&= \frac{1}{\mathbf{x^\dagger x}} \left(\frac{\text{d}(\mathbf{x^\dagger Ax})}{\text{d}\mathbf{x}^I} - R(\mathbf{x}) \frac{\text{d}(\mathbf{x^\dagger x})}{\text{d}\mathbf{x}^I}\right) \\
&= \frac{1}{\mathbf{x^\dagger x}} \left(\mathbf{x^\dagger A}\frac{\text{d}\mathbf{x}}{\text{d}\mathbf{x}^I} + \mathbf{x^\top A^\top}\frac{\text{d}\mathbf{x}^*}{\text{d}\mathbf{x}^I} - R(\mathbf{x})\mathbf{x}^\dagger\frac{\text{d}\mathbf{x}}{\text{d}\mathbf{x}^I} - R(\mathbf{x})\mathbf{x}^\top\frac{\text{d}\mathbf{x}^*}{\text{d}\mathbf{x}^I}\right) \\
&= \frac{1}{\mathbf{x^\dagger x}} \left(i\mathbf{x^\dagger A} - i\mathbf{x^\top A^\top} - iR(\mathbf{x})\mathbf{x}^\dagger + iR(\mathbf{x})\mathbf{x}^\top\right) \\
&= \frac{i}{\mathbf{x^\dagger x}} \left(\mathbf{x^\dagger A} - (\mathbf{x^\dagger A^\dagger})^* - R(\mathbf{x})\mathbf{x}^\dagger + R(\mathbf{x})(\mathbf{x}^\dagger)^*\right) \\
&= \frac{i}{\mathbf{x^\dagger x}} \left(\mathbf{x^\dagger A} - (\mathbf{x^\dagger A})^* - 2R(\mathbf{x})\mathbf{x}^\dagger_I\right) \\
&= i\frac{2(\mathbf{x^\dagger A})_I - 2R(\mathbf{x})\mathbf{x}^\dagger_I}{\mathbf{x^\dagger x}} 
= \mathbf{0}^\top = \mathbf{0}^\dagger
\end{align*}

$$

it follows  

$$

\begin{align*}
\mathbf{0} &= [(\mathbf{x^\dagger A})_I - R(\mathbf{x})\mathbf{x}^\dagger_I]^\dagger \\
&= (\mathbf{A^\dagger x})_I - R(\mathbf{x})\mathbf{x}_I \\
&= (\mathbf{Ax})_I - R(\mathbf{x})\mathbf{x}_I
\end{align*}

$$

to conclude, we have  

$$

\mathbf{A}\tilde{\mathbf{x}} - R(\tilde{\mathbf{x}})\tilde{\mathbf{x}} = \mathbf{0}

$$

where $\tilde{\mathbf{x}}$ is a critical point of $R(\mathbf{x})$, and also an eigenvector of $\mathbf{A}$
