---
title: "Runge-Kutta Method"
date: 2024-01-07 22:52:00 +0800
categories:
  - numerical-analysis
tags:
  - "Numerical Analysis"
  - "Ordinary Differential Equation"
excerpt: "Notes on explicit Runge–Kutta methods, Butcher tableaux, adaptive step-size control, and embedded Runge–Kutta schemes."
mathjax: true
original_url: "https://www.cnblogs.com/Eureka10shen/articles/17951392"
permalink: /blog/runge-kutta-method/
---

> This article was migrated from [Eureka10shen on 博客园]({{ page.original_url }}). The original publication date was 2024-01-07.

---

# Runge Kutta Method

Consider the IVP of an ODE  

$$

\frac{dy}{dt} = f(t,y), \quad y(t_0)=y_0

$$

General formulation of explicit Runge-Kutta methods  

$$

\begin{aligned}
    y_{n+1} &= y_n + h_n \sum_{i=1}^s b_ik_i \\
    k_1 &= h_n f(t_n, y_n) \\
    k_i &= h_n f\left(t_n + c_ih_n, y_n + \sum_{j=1}^{i-1} a_{ij} k_j\right) \\
    i &= 1,2,\cdots,s
\end{aligned}

$$

The coefficients are in the **Butcher tableau** format  

$$

\begin{array}{c|ccccc}
0 & & & & & \\
c_2 & a_{21} & & & & \\
c_3 & a_{31} & a_{32} & & & \\
\vdots & \vdots & \vdots & \ddots & & \\
c_s & a_{s1} & a_{s2} & \cdots & a_{s, s - 1} & \\
\hline \ & b_1 & b_2 & \cdots & b_{s - 1} & b_s
\end{array}

$$

---

# Adaptive RK Method / Embeded Method

Use two RK methods in one time-step (one in $p$-order, another in $(p-1)$-order) [1]  
high order scheme  

$$

y_{n+1} = y_n + h_n \sum_{i=1}^s b_ik_i

$$

low order scheme  

$$

y_{n+1}^* = y_n + h_n \sum_{i=1}^s b_i^* k_i

$$

the Butcher tableau becames  

$$

\begin{array}{c|ccccc}
0 & & & & & \\
c_2 & a_{21} & & & & \\
c_3 & a_{31} & a_{32} & & & \\
\vdots & \vdots & \vdots & \ddots & & \\
c_s & a_{s1} & a_{s2} & \cdots & a_{s, s - 1} & \\
\hline \ & b_1 & b_2 & \cdots & b_{s - 1} & b_s \\
 & b_1^* & b_2^* & \cdots & b_{s - 1}^* & b_s^* \\
\end{array}

$$

the **local error** reads  

$$

e_{n+1} = y_{n+1} - y_{n+1}^* = h_n\sum_{i=1}^s (b_i-b_i^*)k_i \sim \mathcal{O}(h_n^p)

$$

the **error tolerence** for step size control reads [2]  

$$

\varepsilon = Atol + \max(|y_n|, |y_{n+1}|) \cdot Rtol

$$

where $Atol$ is the absolute tolerence and $Rtol$ is the relative tolerence  

---

# Runge-Kutta-Fehlberg Method (RKF45)

a product of Shampine and Watts’ programming art based on Fehlberg’s pair of orders 4 and 5 [3]  
the Butcher tableau reads  

$$

\begin{array}{c|ccccccc}
0 & & & & & & \\
\frac{1}{4} & \frac{1}{4} & & & & & \\
\frac{3}{8} & \frac{3}{32} & \frac{9}{32} & & & & \\
\frac{12}{13} & \frac{1932}{2197} & -\frac{7200}{2197} & \frac{7296}{2197} & & & \\
1 & \frac{439}{216} & -8 & \frac{3680}{513} & -\frac{845}{4104} & & \\
\frac{1}{2} & -\frac{8}{27} & 2 & -\frac{3544}{2565} & \frac{1859}{4104} & -\frac{11}{40} & \\
\hline & \frac{25}{216} & 0 & \frac{1408}{2565} & \frac{2197}{4101} & -\frac{1}{5} \\
& \frac{16}{135} & 0 & \frac{6656}{12825} & \frac{28561}{56430} & -\frac{9}{50} & \frac{2}{55}\\ 
\end{array}

$$

*Python* implementation codes : https://github.com/Borroot/RKF45/blob/master/RKF45.ipynb  
*C* and *Matlab* implementation codes : https://zhuanlan.zhihu.com/p/607546969  

---

# Dormand-Prince Method

The Dormand–Prince (RKDP) method or DOPRI method is a member of the adaptive Runge–Kutta family of ODE solvers [4][5]  
the Butcher tableau reads  

$$

\begin{array}{c|ccccccc}
0 & & & & & & & \\
\frac{1}{5} & \frac{1}{5} & & & & & & \\
\frac{3}{10} & \frac{3}{40} & \frac{9}{40} & & & & & \\
\frac{4}{5} & \frac{44}{45} & -\frac{56}{15} & \frac{32}{9} & & & & \\
\frac{8}{9} & \frac{19372}{6561} & -\frac{25360}{2187} & \frac{64448}{6561} & -\frac{212}{729} & & & \\
1 & \frac{9017}{3168} & -\frac{355}{33} & \frac{46732}{5247} & \frac{49}{176} & -\frac{5103}{18656} & & \\
1 & \frac{35}{384} & 0 & \frac{500}{1113} & \frac{125}{192} & -\frac{2187}{6784} & \frac{11}{84} & \\
\hline & \frac{35}{384} & 0 & \frac{500}{1113} & \frac{125}{192} & -\frac{2187}{6784} & \frac{11}{84} & \\
& \frac{5179}{57600} & 0 & \frac{7571}{16695} & \frac{393}{640} & -\frac{92097}{339200} & \frac{187}{2100} & \frac{1}{40} \\ 
\end{array}

$$

7 substeps in one timestep ($s=7$), but only caculate the function values 6 times ($k_ {1}^{(n+1)} = k_ {s}^{(n)}$)  
*Scipy* codes : https://github.com/scipy/scipy/blob/v1.11.4/scipy/integrate/_ivp/rk.py  

---

refs :  
[1] https://www.zhihu.com/question/450297681/answer/1871226868  
[2] Hairer, Ernst & Norsett, Syvert & Wanner, Gerhard. (1993). Solving Ordinary Differential Equations I: Nonstiff Problems. 10.1007/978-3-540-78862-1. p167.  
[3] Hairer, Ernst & Norsett, Syvert & Wanner, Gerhard. (1993). Solving Ordinary Differential Equations I: Nonstiff Problems. 10.1007/978-3-540-78862-1. p249.  
[4] https://en.wikipedia.org/wiki/Dormand%E2%80%93Prince_method  
[5] Dormand, J. R. and P. J. Prince. “A family of embedded Runge-Kutta formulae.” Journal of Computational and Applied Mathematics 6 (1980): 19-26.
