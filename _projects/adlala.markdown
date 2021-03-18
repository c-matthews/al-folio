---
layout: page
title: AdLaLa
description: Efficient training of neural networks using Adaptive Langevin in Layers
img: /assets/img/spiral.png
importance: 3
pdf: http://dx.doi.org/10.3934/fods.2019019
github: https://github.com/TiffanyVlaar/ThermodynamicParameterizationOfNNs
---
Traditionally, neural networks are parameterized using optimization procedures such as stochastic gradient descent, RMSProp and ADAM. These are optimization schemes, meant to drive the system towards a minimum. We propose alternative _sampling_ algorithms (referred to in the article as "thermodynamic parameterization methods") which rely on discretized stochastic differential equations for a defined target distribution on parameter space. The purpose of this project is to show that the thermodynamic perspective already improves neural network training, and by partitioning the parameters based on natural layer structure we obtain schemes with very rapid convergence for data sets with complicated loss landscapes.

We describe easy-to-implement hybrid partitioned numerical algorithms, based on discretized stochastic differential equations, which are adapted to feed-forward neural networks, including a multi-layer Langevin algorithm, AdLaLa (combining the adaptive Langevin and Langevin algorithms) and LOL (combining Langevin and Overdamped Langevin); we examine the convergence of these methods using numerical studies and compare their performance among themselves and in relation to standard alternatives such as stochastic gradient descent and ADAM. We present evidence that thermodynamic parameterization methods can be (ⅰ) faster, (ⅱ) more accurate, and (ⅲ) more robust than standard algorithms used within machine learning frameworks


Check out the [code](https://github.com/TiffanyVlaar/ThermodynamicParameterizationOfNNs) and the [article](http://dx.doi.org/10.3934/fods.2019019) for more information.
