---
title: "交换相关泛函的发展（Development of Exchange–Correlation Functionals）"
date: 2024-07-11 16:17:00 +0800
categories:
  - quantum-chemistry
tags:
  - DFT
  - Density Functional Theory
  - Quantum Chemistry
excerpt: "Technical notes on the development of exchange–correlation functionals in density functional theory, from the Hohenberg–Kohn theorems and Kohn–Sham DFT to LSDA and GGA."
mathjax: true
original_url: "https://www.cnblogs.com/Eureka10shen/p/18296492"
permalink: /blog/exchange-correlation-functionals/
---

*Technical notes on density functional theory in quantum chemistry.*

> This article was migrated from [Eureka10shen on 博客园]({{ page.original_url }}). The original publication date was July 11, 2024.

Reference: Mardirossian, N., & Head-Gordon, M. (2017). [Thirty years of density functional theory in computational chemistry: an overview and extensive assessment of 200 density functionals](https://doi.org/10.1080/00268976.2017.1333644). *Molecular Physics*, 115(19), 2315–2372.

## The Hohenberg–Kohn Theorems

Within the Born–Oppenheimer approximation, the electronic energy is a functional of the electron density:

$$

E_e[\rho(\mathbf{r})] =
T[\rho(\mathbf{r})] +
V_{en}[\rho(\mathbf{r})] +
J[\rho(\mathbf{r})] +
Q[\rho(\mathbf{r})].

$$

The nuclear–electron attraction energy is

$$

V_{en}[\rho(\mathbf{r})] =
-\sum_{A=1}^M \int
\frac{Z_A}{|\mathbf{r}-\mathbf{R}_A|}
\rho(\mathbf{r})\,\mathrm{d}\mathbf{r},

$$

and the classical electron–electron repulsion energy is

$$

J[\rho(\mathbf{r})] =
\frac{1}{2}\int\int
\frac{\rho(\mathbf{r}_1)\rho(\mathbf{r}_2)}{r_{12}}
\mathrm{d}\mathbf{r}_1\mathrm{d}\mathbf{r}_2.

$$

The central objective of density functional theory is to construct accurate approximations for the electronic kinetic energy and the non-classical electron–electron interaction energy.

## Kinetic-energy functionals

The kinetic-energy functional is the largest unknown contribution. The Thomas–Fermi model provides the simplest approximation and is exact for an infinite uniform electron gas:

$$

T[\rho(\mathbf{r})] =
\frac{3}{10}(3\pi^2)^{2/3}
\int \rho(\mathbf{r})^{5/3}\,\mathrm{d}\mathbf{r}.

$$

Accurate kinetic-energy functionals remain difficult to construct, particularly for strongly inhomogeneous densities.

## Kohn–Sham density functional theory

Kohn–Sham theory introduces a fictitious system of non-interacting electrons with the same density as the interacting system. Its kinetic energy is represented using orbitals:

$$

T_s[\{\psi_i\}] =
-\frac{1}{2}\sum_{i=1}^{n}
\int \psi_i^*(\mathbf{r})\nabla^2\psi_i(\mathbf{r})\,
\mathrm{d}\mathbf{r}.

$$

The exchange–correlation functional collects the difference between the exact and non-interacting kinetic energies together with the non-classical electron–electron interaction:

$$

E_{xc}[\rho(\mathbf{r})] =
T[\rho(\mathbf{r})] -
T_s[\{\psi_i\}] +
Q[\rho(\mathbf{r})].

$$

The introduction of orbitals increases computational cost, motivating orbital-free density functional approaches as well as improved approximations for exchange and correlation.

## Local spin-density approximation

The local spin-density approximation (LSDA) is exact for an infinite uniform electron gas but can be inaccurate for molecular properties. Its exchange energy has the Slater–Dirac form:

$$

E_x^{\mathrm{LSDA}} =
-\frac{3}{2}\left(\frac{3}{4\pi}\right)^{1/3}
\sum_{\sigma\in\{\alpha,\beta\}}
\int \rho_\sigma(\mathbf{r})^{4/3}\,\mathrm{d}\mathbf{r}.

$$

The correlation energy has no exact closed form and is commonly represented through parameterizations such as VWN5, PZ81, PW92, and C16. The local Seitz radius and spin polarization are

$$

r_s =
\left[
\frac{3}{4\pi(\rho_\alpha+\rho_\beta)}
\right]^{1/3},
\qquad
\zeta =
\frac{|\rho_\alpha-\rho_\beta|}
{|\rho_\alpha+\rho_\beta|}.

$$

## Generalized gradient approximation

The generalized gradient approximation (GGA) extends LSDA by incorporating the density gradient and an inhomogeneity correction:

$$

E_x^{\mathrm{GGA}} =
\sum_{\sigma\in\{\alpha,\beta\}}
\int e_{x,\sigma}^{\mathrm{UEG}}
g_{x,\sigma}^{\mathrm{GGA}}\,\mathrm{d}\mathbf{r}.

$$

Important GGA functionals include B88, LYP, PW91, and PBE. For example, the PBE exchange enhancement factor is

$$

F_x(s) =
1+\kappa-\frac{\kappa}{1+\mu s^2/\kappa},

$$

Here s denotes a dimensionless reduced density gradient. These functionals improve the treatment of non-uniform electron densities while retaining the uniform-electron-gas limit.

Meta-GGA and later developments will be discussed in a future note.
