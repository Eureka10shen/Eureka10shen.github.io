---
title: "理论力学_刘川"
date: 2022-09-15 12:12:00 +0800
categories:
  - mechanics
excerpt: "Notes on analytical mechanics, generalized coordinates, virtual work, Lagrangian mechanics, and Hamiltonian mechanics."
mathjax: true
original_url: "https://www.cnblogs.com/Eureka10shen/articles/16696127.html"
permalink: /blog/theoretical-mechanics-liu-chuan/
---

> This article was migrated from [Eureka10shen on 博客园]({{ page.original_url }}). The original publication date was 2022-09-15.

# 理论力学，Theoretical Mechanics
理论力学，北京大学出版社，刘川编著，2019.09

# Chapter 1 Introduction to Analytic Mechanics
Newtonian mechanics --> "force" as fundamental element --> Vector mechanics  
Analytic mechanics --> "energy" as fundamental element

## 1.1 Language of Analytic Mechanics
analytic mechanics = Lagrangian mechanics + Hamiltian mechanics

planar double pendulum:  
(1) newtonian mechanics --> constraint force unknown before solving;  
(2) analytic mechanics --> get the equation of motion without considering the constraints

## 1.2 Constraints and Generalized Coordinates
considering vector mechanics, we have the equation of motion

$$

m_i\ddot{x}_i = F_i^e+\sum_jF_{j\to i}

$$

where $F_ {i}^e$ is the outer force the $i$ th particle felt, and $\sum_ {j} F_ {j\to i}$ is the inner force from particle $j$ to particle $i$

let the constraints be the equation sets

$$

f_m(\mathbf{x_1},\mathbf{x_2},...,\mathbf{x_N},t)=0,m=1,2,...,N,k

$$

holonomic constraints -- constraint of coordinates and time only  
inholonomic constraints -- constraint of velocity, inequality constraint, etc.  
scleronomous constraint -- constraint not explicitly time dependent  
rheonomous constraint -- constraint explicitly time dependent

k constraints --> total degree of freedom = $3N - k$  
__Generalized Coordinate__ : minimun set of coordinate for all independent degree of freedom of the system with holonomic constraints --> $q_ {1}$, $q_ {2}$, ..., $q_ {N-k}$

for constraint of velocity, we have

$$

\dot{\mathbf{x}}_i = \frac{\partial \mathbf{x}_i}{\partial q_l}\dot{q}_l+\frac{\partial \mathbf{x}_i}{\partial t}

$$

here we used the Einstein summation rule for duplicate indexes

## 1.3 Principle of Virtual Work and d'Alembert's Principle
__principle of virtual work__ :  
considering a system under mechanical equilibrium, we have

$$

\sum_iF_i\cdot\delta\mathbf{x}_i = \sum_iF_i^a\cdot\delta\mathbf{x}_i + \sum_iF_i^c\cdot\delta\mathbf{x}_i = 0

$$

assume that _the virtual work of constraints are zero_, we have

$$

\sum_iF_i^a\cdot\delta\mathbf{x}_i = 0

$$

this is called __the Principle of Virtual Work__

__d'Alembert's principle__ :  
considering the system not under mechanical equilibrium, we have

$$

\sum_i(F_i^a-\dot{\mathbf{p}}_i)\cdot\delta\mathbf{x}_i = 0

$$

this is called __d'Alembert's Principle__

under generalized coordinates, rewrite the left terms in __d'Alembert's Principle__, we have

$$

F_i^a\cdot\delta\mathbf{x}_i = F_i^a\cdot\frac{\partial \mathbf{x}_i}{\partial q_l}\delta q_l = Q_l\delta q_l

$$

where $Q_ {l} = F_ {i}^a\cdot\frac{\partial \mathbf{x}_ {i}}{\partial q_ {l}}$ is called __Generalized Force__, and

$$

\begin{align*}
\dot{\mathbf{p}}_i\cdot\delta\mathbf{x}_i 
&= m_i\ddot{\mathbf{x}}_i\cdot\frac{\partial \mathbf{x}_i}{\partial q_l}\delta q_l \\
&= \frac{\text{d}}{\text{d}t}\left(m_i\dot{\mathbf{x}}_i\cdot\frac{\partial \mathbf{x}_i}{\partial q_l}\right)\delta q_l - 
m_i\dot{\mathbf{x}}_i\cdot\frac{\text{d}}{\text{d}t}\left(\frac{\partial \mathbf{x}_i}{\partial q_l}\right)\delta q_l \\
&= \frac{\text{d}}{\text{d}t}\left(m_i\dot{\mathbf{x}}_i\cdot\frac{\partial \mathbf{v}_i}{\partial \dot{q}_l}\right)\delta q_l - 
m_i\dot{\mathbf{x}}_i\cdot\frac{\text{d}}{\text{d}t}\left(\frac{\partial \mathbf{v}_i}{\partial \dot{q}_l}\right)\delta q_l 
\left(\mathbf{v}_i = \frac{\text{d}\mathbf{x}_i}{\text{d}t}=\frac{\partial \mathbf{x}_i}{\partial q_l}\dot{q}_l + \frac{\partial \mathbf{x}_i}{\partial t}\right) \\
&= \frac{\text{d}}{\text{d}t}\frac{\partial T}{\partial \dot{q}_l}\delta q_l - m_i\dot{\mathbf{x}}_i\cdot\frac{\partial \mathbf{v}_i}{\partial q_l}\delta q_l \\
&= \left(\frac{\text{d}}{\text{d}t}\frac{\partial T}{\partial \dot{q}_l}-\frac{\partial T}{\partial q_l}\right)\delta q_l
\end{align*}

$$

where we have

$$

\left(\frac{\text{d}}{\text{d}t}\frac{\partial T}{\partial \dot{q}_l}-\frac{\partial T}{\partial q_l}-Q_l\right)\delta q_l=0

$$

note that the generalized coordinates $\{q_ {i}\}$ are independent variables, we have

$$

\frac{\text{d}}{\text{d}t}\frac{\partial T}{\partial \dot{q}_l}-\frac{\partial T}{\partial q_l} = Q_l

$$

