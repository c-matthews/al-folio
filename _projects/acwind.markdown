---
layout: page
title: ACWind
description: A package using transferable neural networks to classify wind turbine performance
img: /assets/img/turbines.jpg
importance: 6
github: https://github.com/amartinsson/acwind
pdf: https://doi.org/10.1088/1742-6596/1222/1/012041
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/acwindbanner.jpg' | relative_url }}" alt="" title="Wind turbines"/>
    </div>
</div>
<div class="caption">
Wind power management has experienced a significant uptake of machine learning methods in recent years.
</div>

Classification  of  operational  status  is  an  important  step  for  performance  analysis of  wind  farms  using  SCADA  (Supervisory  Control  and  Data  Acquisition) data, essentially time series data corresponding to physical readouts from the hardware.   The  main  goal  of  the  analysis  is  future  energy  production  assessment  and the  identification  of  performance  issues, though this will require using data from  hundreds of millions of SCADA timepoint records in a  typical  wind  farm.  Until recently, classification of under-performance and different operational states has often been performed by a human analyst. Automatization of this process can save many working hours and provide additional insight  into  wind  turbine  operations.   Training data is readily available as companies typically possess  historical  data from  various  farms  where  the  power  generation  status  has  already  been  analyzed. Understanding  the  operational  status  can  explain  under-performance,  for  example by  indicating  when  the  turbine  may  require  maintenance.   This  under-performance may be a consequence of power derating, blade icing, or other conditions.  In order to automate this task, we use the knowledge of these under-performing operations within a supervised learning model, which is then employed to classify unlabeled data from various turbine types and farms.

The primary difficulty in automation lies in the transferability of models between farms. The elevation, local topography, climate, and proximity to human population can all affect the resulting power curve that the model will be trained upon. Training a model for one farm means that it will not produce reliable results for the next.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/transf.png' | relative_url }}" alt="" title="Wind farm power/speed curves for different farms"/>
    </div>
</div>
<div class="caption">
Characteristic  power  curves  from  six  wind  turbine  farms, taken from historical time-series of wind speed and power signals.
</div>

We tackled this problem in two ways. The first was to normalize the data on to one master power curve via an affine rescaling of the SCADA data, parameterized to minimize the KL divergence between the observed data and the reference curve. Differing wind farms can be transformed so that only one model needs to be trained.

The second technique was the use of a time point matrix as the input to a convolutional neural network. Rather than input the SCADA data at time $$t$$, we spiral time points outward from the centre of a matrix and feed this into the neural network. This allows the model to "look back in time" and compare the current result relative to previous results. This gives a similar effect to a recurrent neural network, but makes it much simpler to train.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/tmatrix.png' | relative_url }}" alt="" title="Time points organized into matrix data"/>
    </div>
</div>

We developed a Python package [acwind](https://github.com/amartinsson/acwind) which takes the data as input and automatically reparameterizes and trains a model. The package requires [PyTorch](https://pytorch.org/) and can be used to train CNNs to classify the operational status  of  SCADA  data.   The package is currently in use by our industry partner DNV GL who have reported saving analysts' time by over fifty percent.


Check out the  [article](https://doi.org/10.1088/1742-6596/1222/1/012041) for more information and comparisons with other models such as a KNN  or a simpler feed-forward neural network with baseline normalization. The [code](https://github.com/amartinsson/acwind) is also available as a repo, or by installation through pip via
```bash
pip install acwind
```
