---
title: "Variational Autoencoder"
date: 2023-01-29 22:05:00 +0800
categories:
  - machine-learning
excerpt: "An introduction to variational autoencoders, latent-variable modelling, reparameterization, and the evidence lower bound."
mathjax: true
original_url: "https://www.cnblogs.com/Eureka10shen/articles/17073957.html"
permalink: /blog/variational-autoencoder/
---

> This article was migrated from [Eureka10shen on 博客园]({{ page.original_url }}). The original publication date was 2023-01-29.

---

References :  
苏剑林. (Mar. 18, 2018). 《变分自编码器（一）：原来是这么一回事 》[Blog post]. Retrieved from https://kexue.fm/archives/5253  
苏剑林. (Mar. 28, 2018). 《变分自编码器（二）：从贝叶斯观点出发 》[Blog post]. Retrieved from https://kexue.fm/archives/5343  

---

## Task

we want to model the distribution $p(x)$ from dataset $\mathcal{D} = \{x_ {1},\cdots,x_ {N}\}$ such that we can _generate_ data directly from it  
while direct modeling is very hard, so we use  

$$

p(x) = \sum_z p(x|z)p(z)

$$

where we first generate the _latent_ variable $z$ and then generate the _visible_ variable $x$ with _decoder_ $p(x\vert z)$  
our objective is to minimize the distance between the generated dataset $\{\hat{x}_ {k}\}$ and the original dataset $\{x_ {k}\}$  

$$

\min\sum_k distance\left(\hat{x}_k - x_k\right)^2

$$

---

## Variational Autoencoder

the essential philosophy of VAE is assuming the _posterior_ distribution $p(z\vert x_ {k})$ to be a normal distribution which can be viewed as the _encoder_  
the mean and variance of the normal distribution w.r.t. the specified sample $x_ {k}$ can be modeled with neural network  

$$

\mu_k = f_{NN}(x_k), \quad \log\sigma_k^2 = g_{NN}(x_k)

$$

> we model $\log\sigma_ {k}^2$ rather than $\sigma_ {k}^2$ because $\sigma_ {k}^2$ is non-negative such that we have to deal it with activation function  

---

## Standardization of Normal Distribution

since the latent variable $z_ {k}$ is sampled from the sample distribution $\mathcal{N}(\mu_ {k},\sigma_ {k}^2)$, the result will be influenced by the noise  
to lower the reconstruction error, the model will enforce the variance $\sigma_ {k}^2$ to approach $\mathbf{0}$ in the training process such that the model will become the _trivial_ auto-encoder (without randomness)  
in VAE, we let all posterior distribution $p(z\vert x_ {k})$ approach the _standard_ normal distribution $\mathcal{N}(\mathbf{0},\mathbf{I})$ such that the model can be generative  

$$

p(z) = \sum_x p(z|x)p(x) = \sum_x\mathcal{N}(\mathbf{0},\mathbf{I})p(x) = \mathcal{N}(\mathbf{0},\mathbf{I})\sum_x p(x) = \mathcal{N}(\mathbf{0},\mathbf{I})

$$

where we can generate dataset from the normal distribution with decoder  
we have to add the _loss_ with KL divergence between the posterior distrubution and the normal distribution  

$$

KL\left(\mathcal{N}(\mu_k,\sigma_k^2)\big\Vert\mathcal{N}(\mathbf{0},\mathbf{I})\right) = \frac{1}{2}\sum_{i=1}^d\left(\mu_{(i)}^2+\sigma_{(i)}^2-\log\sigma_{(i)}^2-1\right)

$$

where $d$ is the dimension of latent variable $z$  
>proof :  
for _univariate_ normal distribution  

$$

\begin{aligned}
& KL\left(N(\mu,\sigma^2)\big\Vert N(0,1)\right)\\ 
=& \int \frac{1}{\sqrt{2\pi\sigma^2}}e^{-(x-\mu)^2/2\sigma^2} 
\left(\log \frac{e^{-(x-\mu)^2/2\sigma^2}/\sqrt{2\pi\sigma^2}} 
{e^{-x^2/2}/\sqrt{2\pi}} \right)dx\\ 
=& \int \frac{1}{\sqrt{2\pi\sigma^2}}e^{-(x-\mu)^2/2\sigma^2} 
\log \left\{\frac{1}{\sqrt{\sigma^2}}\exp\left\{\frac{1}{2} 
\left[x^2 - \frac{(x-\mu)^2}{\sigma^2}\right]\right\} \right\}dx\\ 
=& \frac{1}{2}\int \frac{1}{\sqrt{2\pi\sigma^2}}e^{-(x-\mu)^2/2\sigma^2} \left[-\log \sigma^2+x^2 - \frac{(x-\mu)^2}{\sigma^2} \right] dx \\
=& \frac{1}{2}\left(-\log \sigma^2+\mu^2+\sigma^2-1\right)
\end{aligned}

$$

---

## Reparameterization Trick

every latent variable $z_ {k}$ is sampled from a normal distribution $\mathcal{N}(\mu_ {k},\sigma_ {k}^2)$ such that every sample operation is _different_  
while the sample operation is _not differentiable_ such that we cannot use the gradient descent to optimize the paramaters of the normal distribution  
from the differential relation  

$$

\frac{1}{\sqrt{2\pi\sigma^2}}\exp\left(-\frac{(z-\mu)^2}{2\sigma^2}\right)dz = \frac{1}{\sqrt{2\pi}}\exp\left[-\frac{1}{2}\left(\frac{z-\mu}{\sigma}\right)^2\right]d\left(\frac{z-\mu}{\sigma}\right)

$$

sampling $z$ from $\mathcal{N}(\mu_ {k},\sigma_ {k}^2)$ is equal to sampling $\varepsilon$ from $\mathcal{N}(\mathbf{0},\mathbf{I})$ and then make the transformation  

$$

z = \mu + \sigma\times\varepsilon

$$

such that all sample operation will be the _same_ and the transformation is differentiable w.r.t. the parameters  

---

## Essence of VAE

auto-encoder = encoder + decoder  
VAE $\rightarrow$ encoder = $f_ {NN}$ + $g_ {NN}$  
> $g_ {NN}$ : the variance add the latent variable with noise such that the decoder can be robust w.r.t. noise  
> when decoder is not _ready_ such that the reconstruction error is bigger than the KL divergence, the model will decrease the noise (increase the KL divergence) to help tranining (decrease the reconstruction error)  
> when decoder is _ready_ such that the reconstruction error is smaller than the KL divergence, the model will increase the noise (decrease the KL divergence) to enforce the robustness of decoder (increase the reconstruction error)  

an adversarial process lies between the training of encoder and decoder  

---

## Bayesian View -- MLE

denote the encoder as $q_ {\phi}\left(z\vert x_ {k}\right)$, the decoder as $p_ {\theta}\left(x_ {k}\vert z\right)$  
given dataset $\mathcal{D} = \{x_ {1},\cdots,x_ {N}\}$, we want to maximize the likelihood of the visible variable  

$$

\max_\theta\mathbb{E}_{x\sim\mathcal{D}}[\log p_\theta(x)] = \max_\theta\sum_{k=1}^N \log p_\theta(x_k)

$$

to solve the marginal distribution $p_ {\theta}(x_ {k})$, we use the variational ineference  
$\diamondsuit$ method 1 : from KL divergence  

$$

\begin{aligned}
KL\left(q_\phi(z|x_k)\big\Vert p_\theta(z|x)\right)
&= \mathbf{E}_{q_\phi(z|x_k)} [\log q_\phi(z|x_k) - \log p_\theta(z|x)] \\
&= \mathbf{E}_{q_\phi(z|x_k)} \left[\log q_\phi(z|x_k) - \log \frac{p_\theta(z,x_k)}{p_\theta(x_k)}\right] \\
&= \mathbf{E}_{q_\phi(z|x_k)} [\log q_\phi(z|x_k) - \log p_\theta(z,x_k)] + \log p_\theta(x_k) \\
\end{aligned}

$$

>we have  

$$

\begin{aligned}
\log p_\theta(x_k)
&= \mathbf{E}_{q_\phi(z|x_k)} [\log p_\theta(z,x_k) - \log q_\phi(z|x_k)] + KL\left(q_\phi(z|x_k)\big\Vert p_\theta(z|x)\right) \\
&\geq \mathbf{E}_{q_\phi(z|x_k)} [\log p_\theta(z,x_k) - \log q_\phi(z|x_k)]
\end{aligned}

$$

>the evidence lower bound reads  

$$

ELBO = \mathbf{E}_{q_\phi(z|x_k)}
[\log p_\theta(z,x_k) - \log q_\phi(z|x_k)]

$$

$\heartsuit$ method 2 : from Jensen inequality  

$$

\begin{aligned}
\log p_\theta(x_k)
&= \log\left[\int_z p_\theta(z,x_k)dz\right] \\
&= \log\left[\int_z q_\phi(z|x_k)\frac{p_\theta(z,x_k)}{q_\phi(z|x_k)}dz\right] \\
&\geq \int_z \left[q_\phi(z|x_k)\log\frac{p_\theta(z,x_k)}{q_\phi(z|x_k)}\right]dz \\
&= \mathbf{E}_{q_\phi(z|x_k)} [\log p_\theta(z,x_k) - \log q_\phi(z|x_k)]
\end{aligned}

$$

>same as above ELBO  

maximizing the likelihood is equal to maximize the ELBO  
from the ELBO we have  

$$

\begin{aligned}
ELBO
&= \mathbf{E}_{q_\phi(z|x_k)} [\log p_\theta(z,x_k) - \log q_\phi(z|x_k)] \\
&= \mathbf{E}_{q_\phi(z|x_k)} [\log p_\theta(x_k|z) + \log p_\theta(z) - \log q_\phi(z|x_k)] \\
&= \mathbf{E}_{q_\phi(z|x_k)} \left[\log p_\theta(x_k|z) - \log\frac{q_\phi(z|x_k)}{p_\theta(z)}\right] \\
&= \mathbf{E}_{q_\phi(z|x_k)}[\log p_\theta(x_k|z)] - KL\left(q_\phi(z|x_k)\big\Vert p_\theta(z)\right)
\end{aligned}

$$

where the first term can be viewed as the __reconstruction error__ and the second term can be viewed as the __prior regularization error__  

---

## Bayesian View -- Joint Distribution Fitting

denote the encoder as $q_ {\phi}\left(z\vert x_ {k}\right)$, the decoder as $p_ {\theta}\left(x_ {k}\vert z\right)$  
given dataset $\mathcal{D} = \{x_ {1},\cdots,x_ {N}\}$, we want to fit the joint distribution of model and dataset  

$$

\begin{aligned}
KL\left(p(x,z)\big\Vert p_\theta(x,z)\right)
&= \int_x\int_z p(x,z)\log\frac{p(x,z)}{p_\theta(x,z)}dxdz \\
&= \int_x\int_z \tilde{p}(x)q_\phi(z|x) \log\frac{p(x,z)}{p_\theta(x,z)}dxdz \\
&= \int_x\tilde{p}(x) \left[\int_z q_\phi(z|x) \log\frac{p(x,z)}{p_\theta(x,z)}dz\right]dx \\
&= \mathbb{E}_{\tilde{p}(x)} \left[\int_z q_\phi(z|x) \log\frac{\tilde{p}(x)q_\phi(z|x)}{p_\theta(x,z)}dz\right] \\
&= \mathbb{E}_{\tilde{p}(x)} \left[\int_z q_\phi(z|x) \left(\log\tilde{p}(x) + \log\frac{q_\phi(z|x)}{p_\theta(x,z)}\right)dz\right] \\
&= \mathbb{E}_{\tilde{p}(x)} \left[\log\tilde{p}(x) + \int_z q_\phi(z|x) \log\frac{q_\phi(z|x)}{p_\theta(x,z)}dz\right] \\
&= const + \mathbb{E}_{\tilde{p}(x)} \left[\int_z q_\phi(z|x) \log\frac{q_\phi(z|x)}{p_\theta(x,z)}dz\right] \\
&= const + \mathbb{E}_{\tilde{p}(x)} \left[\int_z q_\phi(z|x) \log\frac{q_\phi(z|x)}{p_\theta(x|z)p_\theta(z)}dz\right] \\
&= const + \mathbb{E}_{\tilde{p}(x)} \left[\int_z q_\phi(z|x) \left(\log\frac{q_\phi(z|x)}{p_\theta(z)} - \log p_\theta(x|z)\right)dz\right] \\
&= const + \mathbb{E}_{\tilde{p}(x)} \left\{KL\left(q_\phi(z|x)\big\Vert p_\theta(z)\right) - \mathbb{E}_{q_\phi(z|x)}[\log p_\theta(x|z)]\right\} \\
\end{aligned}

$$

minimizing the divergence is equal to minimizing the loss  

$$

\mathcal{L} = \sum_{k=1}^N KL\left(q_\phi(z|x_k)\big\Vert p_\theta(z)\right) - \mathbb{E}_{q_\phi(z|x_k)}[\log p_\theta(x_k|z)]

$$

which equals to maximizing the ELBO  

---
