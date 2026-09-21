---
title: "Jacobi-Davidson Method"
date: 2022-11-07 22:22:00 +0800
categories:
  - numerical-analysis
excerpt: "An overview of subspace projection, residual correction, and restart strategies in the Jacobi–Davidson eigensolver."
mathjax: true
original_url: "https://www.cnblogs.com/Eureka10shen/articles/16867724.html"
permalink: /blog/jacobi-davidson-method/
---

> This article was migrated from [Eureka10shen on 博客园]({{ page.original_url }}). The original publication date was 2022-11-07.

---

## Subspace Projection

for the standard eigenvalue problem of large sparse matrices $\mathbf{A}\in\mathbb{R}^{n\times n}$  

$$

\mathbf{Ax}=\lambda\mathbf{x}

$$

we want to project the large matrix onto a small subspace  

$$

\mathcal{S}_k := \text{span}(\mathbf{v}_1,\mathbf{v}_2,...,\mathbf{v}_k)

$$

where $\mathbf{v}_ {i}$ is a $n$-dim vector with $\{\mathbf{v}_ {1},\mathbf{v}_ {2},...,\mathbf{v}_ {k}\}$ being a set of standard orthogonal basis  

$$

\mathbf{V}_k = \begin{bmatrix}
\mathbf{v}_1 & \mathbf{v}_2 & \dots & \mathbf{v}_k
\end{bmatrix} \in\mathbb{R}^{n\times k}

$$

and we want to approximate the eigenpair $(\lambda, \mathbf{x})$ of $\mathbf{A}$ with its Ritz-pair $(\theta_ {k}, \mathbf{u}_ {k})$ on the subspace which satisfies the Ritz-Galerkin condition  

$$

\begin{cases}
\left(\mathbf{A}\mathbf{u}_k-\theta_k\mathbf{u}_k\right) \perp \text{span}(\mathbf{v}_1,\mathbf{v}_2,...,\mathbf{v}_k) \\
\mathbf{u}_k = \mathbf{V}_k\mathbf{s}_k
\end{cases} \Rightarrow 
\mathbf{V}_k^\top\mathbf{A}\mathbf{V}_k\mathbf{s}_k-\mathbf{\theta}_k\mathbf{s}_k = 0

$$

  
where we can notice that it is much easier to solve the eigenpair $(\theta_ {k}, \mathbf{s}_ {k})$ of projected matrix $\mathbf{V}_ {k}^\top\mathbf{A}\mathbf{V}_ {k}$

---

## Residue Correction

define the correction for the approximate eigenvector $\mathbf{u}_ {k}$ as $\mathbf{t}_ {k}$  

$$

\begin{cases}
\mathbf{A}\left(\mathbf{u}_k+\mathbf{t}_k\right) = \lambda\left(\mathbf{u}_k+\mathbf{t}_k\right) \\
\mathbf{t}_k \perp \mathbf{u}_k
\end{cases}

$$

assume that $\theta_ {k}$ is a good approximation of $\lambda$, we can rewrite the eigen-problem as  

$$

\left(\mathbf{A}-\theta_k\mathbf{I}\right)\mathbf{t}_k = -\mathbf{r}_k+(\lambda-\theta_k)\mathbf{u}_k+(\lambda-\theta_k)\mathbf{t}_k

$$

where $\mathbf{r}_ {k} = \mathbf{A}\mathbf{u}_ {k}-\theta_ {k}\mathbf{u}_ {k}$ is called the residue  
<font color = OrangeRed>Source of error</font> : regard the third term as high-order small quantity  

$$

\left(\mathbf{A}-\theta_k\mathbf{I}\right)\mathbf{t}_k \approx -\mathbf{r}_k+(\lambda-\theta_k)\mathbf{u}_k

$$

notice that $\mathbf{u}_ {k}^\top\mathbf{r}_ {k}=0$ and $\mathbf{u}_ {k}^\top\mathbf{u}_ {k}=1$, we can make the projection of the problem  

$$

\left(\mathbf{I}-\mathbf{u}_k\mathbf{u}_k^\top\right)\left(\mathbf{A}-\theta_k\mathbf{I}\right)\mathbf{t}_k = -\mathbf{r}_k

$$

notice that $\mathbf{u}_ {k}^\top\mathbf{t}_ {k}=0$, we can rewrite the projection as  

$$

\left(\mathbf{I}-\mathbf{u}_k\mathbf{u}_k^\top\right)\left(\mathbf{A}-\theta_k\mathbf{I}\right)\left(\mathbf{I}-\mathbf{u}_k\mathbf{u}_k^\top\right)\mathbf{t}_k = -\mathbf{r}_k

$$

we can get the correction $\mathbf{t}_ {k}$ by solving the above equation  

---

## Algorithm

1) predefine `max_iteration` $m$, `tolerence` $\varepsilon$, initial subspace $\mathbf{V}_ {1}=\{\mathbf{v}_ {1}\}$, initial approximate eigenvalue $\mathbf{u}_ {1}=\mathbf{v}_ {1}$  
2) for $k=1,2,...,m-1$, perform  
  a. compute projected matrix $\mathbf{H}_ {k}=\mathbf{V}_ {k}^\top\mathbf{A}\mathbf{V}_ {k}$, approximate eigenvalue $\mathbf{\theta}_ {k}=\mathbf{u}_ {k}^\top\mathbf{A}\mathbf{u}_ {k}$, residue $\mathbf{r}_ {k} = \mathbf{A}\mathbf{u}_ {k}-\theta_ {k}\mathbf{u}_ {k}$  
  b. solve the correction equation

$$

\begin{cases}
\left(\mathbf{I}-\mathbf{u}_k\mathbf{u}_k^\top\right)
\left(\mathbf{A}-\theta_k\mathbf{I}\right)
\left(\mathbf{I}-\mathbf{u}_k\mathbf{u}_k^\top\right)\mathbf{t}_k
= -\mathbf{r}_k, \\
\mathbf{t}_k \perp \mathbf{u}_k.
\end{cases}

$$

  c. expand the subspace from $\mathbf{V}_ {k}$ to $\mathbf{V}_ {k+1}$ with $\mathbf{t}_ {k}$ by Schmidt Orthogonalization  
  d. compute the eigenpair $(\theta_ {k+1},\mathbf{s}_ {k+1})$ of new projected matrix $\mathbf{H}_ {k+1}=\mathbf{V}_ {k+1}^\top\mathbf{A}\mathbf{V}_ {k+1}$  
  e. compute the Ritz vector $\mathbf{u}_ {k+1} = \mathbf{V}_ {k+1}\mathbf{s}_ {k+1}$ and the residue $\mathbf{r}_ {k+1} = \mathbf{A}\mathbf{u}_ {k+1}-\theta_ {k}\mathbf{u}_ {k+1}$  
  f. check the convergence : if yes, stop the algorithm; if no, $k=k+1$  
3) restart with initial subspace $\mathbf{V}_ {1}=\{\mathbf{u}_ {m}\}$, and perfrom from `step 2`  

---
