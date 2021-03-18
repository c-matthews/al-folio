---
layout: page
title: Ensemble Quasi-Newton
description: Scale-invariant, Langevin dynamics-based MCMC
img: /assets/img/landscapes2.jpg
importance: 8
repo: http://bitbucket.org/c%5fmatthews/ensembleqn
pdf: https://doi.org/10.1007/s11222-017-9730-1
---

In this project we are looking to compute samples $$x\in X\subseteq\mathbb{R}^N$$ weighted according to a probability distribution $$\pi(x)\propto\exp(-V(x))$$ where the dimension $$N$$ is large and $$V$$ is sometimes called the _potential energy_ or the _negative log posterior_. The energy landscape of $$\pi(x)$$ can be scaled poorly so that some directions can be explored much slower than others. Consider a valley-like landscape, where if we move too quickly isotropically we will hit a steep incline and be bounced out.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/landscapes2.jpg' | relative_url }}" alt="" title=""/>
    </div>
</div>
<div class="caption">
    Ensemble Quasi-Newton maps the landscape by looking at the covariance of multiple copies of the system. The dynamics are rescaled so that we explore more efficiently by moving in slow directions at an improved rate.
</div>

In a schemes for the conventional over-damped dynamics (such as in Euler-Maruyama integrating Brownian dynamics), we make moves like

$$x_{k+1} \leftarrow x_k + \delta t \nabla \log\pi(x_k) + \sqrt{2 \delta t} R_{k},$$

at iteration $$k$$, for a random number $$R_k \sim N(0,I)$$. If the timestep $$\delta t>0$$ is too large, then we will (proverbially) ping off the edges of the valley and the system will go off to infinity. Ideally, we would like to _pre-condition_ the system, so that moves in the direction perpendicular to the valley's edges are made longer and we move more efficiently.

The difficulty lies in figuring out the direction in which to bias the movement. In Newton-iteration schemes the Hessian matrix provides this information, but second derivatives are not always available and expensive to compute at each step. Instead, we approximate the Hessian with the covariance of independent copies of the system.

Consider an _ensemble_ of $$L$$ independent walkers, with positions $$Q = (x^{(i)} )_{i=1,\ldots,L}$$, and use the update for walker $$i$$ as

$$x^{(i)}_{k+1} \leftarrow x^{(i)}_k + B(Q_{[i]})\delta t \nabla \log\pi(x^{(i)}_k) + \sqrt{2 B(Q_{[i]}) \delta t} R^{(i)}_{k},$$

where $$B(Q):=\text{cov}(Q)$$ is the Euclidean $$N\times N$$ covariance matrix, and $$Q_{[i]}$$ is the set of all positions _except_ walker $$i$$. This choice removes the divergence term as then $$\nabla_{i} \cdot B(Q_{[i]})\equiv 0$$. This choice of $B$ makes the dynamics _affine invariant_ for a large enough (ie $$O(N)$$ ) number of walkers $$L$$, so the performance will be constant regardless of rescalings of the problem. This is a hugely important feature when we are trying to sample from distributions without physical intuition.

In the article we go into more detail about the convergence results, and demonstrate some numerical experiments showing the power of this formalism. We also show a second-order method with momentum, in the case where barriers stymie progress.

For more details, checkout [the article](https://doi.org/10.1007/s11222-017-9730-1) and the [Python code](http://bitbucket.org/c%5fmatthews/ensembleqn).
