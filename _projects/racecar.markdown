---
layout: page
title: Racecar
description: Sampling high-dimensional problems using efficient, on-the-fly estimations of the stochastic gradient noise
img: https://raw.githubusercontent.com/c-matthews/racecar/main/img/logo.png
importance: 1
github: https://github.com/c-matthews/racecar
---

Racecar is a lightweight Python library for sampling distributions in high dimensions using cutting-edge algorithms. It can also be used for rapid prototyping of novel methods and application to high dimensional use-cases. Pass a function evaluating the log posterior and/or its gradient, and away you go! Designed for use with stochastic gradients in mind. Ideal for usage with big data applications, neural networks, regression, mixture modelling, and all sorts of Bayesian inference and sampling problems.

Easily installed with __pip__ via

```bash
pip install racecar
```
The algorithm learns the gradient noise covariance on-the-fly, and uses the learned representation to damp the dynamics and improve the sampling properties. At no extra computational cost, it offers a significant improvement over state of the art methods like SGHMC or SGLD.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ 'https://raw.githubusercontent.com/c-matthews/racecar/main/img/example_result.png' | relative_url }}" alt="" title="Sampling results"/>
    </div>
</div>
<div class="caption">
    An example comparing the experimental results (in black) to the true results (in red).
</div>

The name _RACECAR_ comes from the splitting of the Langevin dynamics into pieces A,C,E and R, and solving them in a palendromic order.

Check out the [code](https://github.com/c-matthews/racecar) and try out the algorithm and examples. Also take a look at another stochastic gradient scheme I have worked on, called [NOGIN](/projects/nogin/).
