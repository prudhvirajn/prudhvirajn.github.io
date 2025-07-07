---
title: "Taylor expansion of Model Behaviour"
date: 2025-07-06T15:51:49-07:00
draft: false
ShowToc: false
tags: ["math", "machine-learning", "statistics"]
categories: ["machine-learning"]
summary: "Model behaviour changes maybe dependent on Hessian, Learning Rate and Weight Norms"
math: true
---

*Warning: First draft, read at your own peril*

## Background

Language models are probabilistic models $P\_{\theta}(x)$ where $x$ is a string and $\theta$ is the model parameters. During gradient descent, we update $\theta$ and calculate loss (or error function) $L(\theta)$. 

In this article, I want to understand how the model changes when we change $\theta$ at timestep $t+1$ w.r.t the previous timestep $\theta\_t$. This article is partially motivated by Natural Gradients[^1] and partly because I am driven by nightmares that I am not setting the learning rate correctly! xD

These derivations were shown by Andy[^1], I just want to re-write them for my understanding. 

## The first two terms are zero

Let $P\_{\theta}$ refer to the probability measure induced by $\theta$ on some set of strings $X$.

<div>
$$
\begin{aligned}
D_{KL}(P_{\theta}, P_{\theta_t}) &\approx D_{KL}(P_{\theta_t}, P_{\theta_t}) \\
&\quad + (\nabla_{\theta} D_{KL}(P_{\theta}, P_{\theta_t}) \left. \right|_{\theta=\theta_t}) (\theta - \theta_t) \\
&\quad + (\theta - \theta_t)^{\top} H(\theta_t) (\theta - \theta_t)
\end{aligned}
$$
</div>

where H is the Hessian w.r.t $\theta$.

The first term $D_{KL}(P_{\theta_t}, P_{\theta_t})$ is $0$ as the probability distributions are the same. 

The second term is also $0$. This is quite interesting.  

<div>
$$
\begin{aligned}
\nabla_{\theta} D_{KL}(P_{\theta}, P_{\theta_t}) \left. \right|_{\theta=\theta_t} &= \nabla_{\theta}\ \mathbb{E}_{x \sim P_{\theta_t}} \left[\log \frac{P_{\theta} (x)}{P_{\theta_t} (x)} \right] \\
\text{ Since the $x$ is drawn from $P_{\theta_t}$ which does not depend on $\theta$} \\
&= \mathbb{E}_{x \sim P_{\theta_t}} \nabla_{\theta}\ \left[\log \frac{P_{\theta} (x)}{P_{\theta_t} (x)} \right] \\
&= \mathbb{E}_{x \sim P_{\theta_t}} \nabla_{\theta}\ \left[\log P_{\theta} (x) - \log P_{\theta_t} (x) \right] \\
\text{Since $P_{\theta_t} (x)$ does on depend on $\theta$} \\
&= \mathbb{E}_{x \sim P_{\theta_t}} \nabla_{\theta}\ \left[\log P_{\theta} (x) \right] \left. \right|_{\theta=\theta_t} \\ 
\text{As we are evaluating the gradient at $\theta=\theta_t$ } \\
&= \mathbb{E}_{x \sim P_{\theta_t}} \frac{1}{P_{\theta_t} (x)} \nabla_{\theta}\ P_{\theta} (x) \left. \right|_{\theta=\theta_t}\\
&= \sum_{x} P_{\theta_t} (x) \frac{1}{P_{\theta_t} (x)} \nabla_{\theta}\ P_{\theta} (x) \left. \right|_{\theta=\theta_t}\\
&= \sum_{x} \nabla_{\theta}\ P_{\theta} (x) \left. \right|_{\theta=\theta_t}\\
\text{By the magic of linearity} \\
&= \nabla_{\theta}\ \sum_{x} P_{\theta} (x) \left. \right|_{\theta=\theta_t}\\
&= \nabla_{\theta}\ 1 \\
&= 0 \\
\end{aligned}
$$
</div>

This means $D_{KL}(P_{\theta}, P_{\theta_t}) \approx (\theta - \theta_t)^{\top} H(\theta_t) (\theta - \theta_t)$.

## Bounded weight updates bound behaviour

Let's ask the question what is the maximum $D_KL(P_{\theta}, P_{\theta_t})$ given finite weight updates $\Delta \theta$. 

<div>
$$
\begin{aligned}
D_{KL}(P_{\theta}, P_{\theta_t}) &\approx (\Delta \theta)^{\top} H(\theta_t) (\Delta \theta) \\
&\le (\Delta \theta)^{\top} \lambda_{max}(\theta_t) I (\Delta \theta) \\
&\le \lambda_{max}(\theta_t) (\Delta \theta)^{\top} (\Delta \theta) \\
&\le \lambda_{max}(\theta_t) \| \Delta \theta \|^2_2 \\
\end{aligned}
$$
</div>

where $\lambda_{max}(\theta_t)$ is the largest eigenvalue of $H(\theta_t)$

If we consider a weight update in SGD with l2 regularization:

<div>
$$
\theta_{t+1} = \theta_{t} - \nu_t (g_t + \gamma \theta_t)
$$
</div>

where $\nu_t$ is the step multiplier (or learning rate at step t) and $\gamma$ is the weight decay coefficient. Furthermore, let's presume that the gradient norm is clipped to 1 which is a standard practice. 

<div>
$$
\begin{aligned}
D_{KL}(P_{\theta}, P_{\theta_t}) &\le \lambda_{max}(\theta_t) \| \Delta \theta \|^2_2 \\
&\le \lambda_{max}(\theta_t) \| \nu_t (g_t + \gamma \theta_t) \|^2_2 \\
&\le \lambda_{max}(\theta_t) \nu_t^2 \| (g_t + \gamma \theta_t) \|^2_2 \\
&\le \lambda_{max}(\theta_t) \nu_t^2 \left( \| g_t \|^2_2 + \| \gamma \theta_t \|^2_2 \right) \\
&\le \lambda_{max}(\theta_t) \nu_t^2 \left( 1 + \gamma ^2_2 \| \theta_t \|^2_2 \right) \\
\end{aligned}
$$
</div>

We can conclude three things from the bound $D_{KL}(P_{\theta}, P_{\theta_t})$:

1. The eigenvalues of the Hessian influence model behaviour. 

2. Weight regularization only increases the magnitude of KL-divergence. 

3. Smaller learning rate limits change in model behaviour in accordance with expectation. 


It would be interesting to see how problem formulation or model architecture can change the Hessian. This may suggest certain training methodologies more readily change model behaviours. 

In fine-tuning, practioners use small learning rates. Despite this, the model behaviours seems to change drastically. This maybe because of we measure other metrics rather than KL-divergence but it may also hint that the eigenvalues of the Hessian are large. 

Ghorbani et al, 2019[^2] shows the eigenvalues of the Hessian getting larger during training. They demonstrated this for ResNet over image datasets. 

We could view pre-training through the lens of eigenstructure of the hessian. Pre-training neural networks helps with finetuning. Measure the PSD-ness of the Hessian could serve as an indicator of how much the behaviour could change during fine-tuning (even RL-finetuning). 

### Footnotes

[^1]: [Andy Jones. "Natural gradients"](https://andrewcharlesjones.github.io/journal/natural-gradients.html)

[^2]: [Behrooz Ghorbani, Shankar Krishnan, Ying Xiao. ICML 2019. "An Investigation into Neural Net Optimization via Hessian Eigenvalue Density"](https://proceedings.mlr.press/v97/ghorbani19b.html)
