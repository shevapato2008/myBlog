---
layout: nnml
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Week 9 - Ways to Make Neural Networks Generalize Better

<br>

### a. Overview of Ways to Improve Generalization

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.1.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.2.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.3.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.4.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.5.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.6.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.7.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.8.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### b. Limiting the Size of the Weights

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.9.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.10.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.11.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.12.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.13.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### c. Using Noise as a Regularizer

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.14.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.15.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.16.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.17.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.18.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### d. Introduction to the Full Bayesian Approach

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.19.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.20.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.21.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.22.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.23.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.24.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

$1$st data point:

$$
\text{prior distribution:} \quad P(p) = \frac{1}{1-0} = 1 \ \text{for} \ p \in [0, \ 1]\\
\begin{align}
  P(&p | x_{1} = 1)\\
  &= \frac{P(p) \cdot P(x_{1} = 1 | p)}{P(x_{1} = 1)} \qquad \qquad \text{(} P(x_{1} = 1) \text{ is the rescaling factor.)}\\
  &= \frac{1 \cdot p^{x_{1}}(1 - p)^{1 - x_{1}}}{P(x_{1} = 1)} \\
  &= 2p
\end{align}
$$

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.25.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

$2$nd data point:

$$
\begin{align}
  P(&p | x_{1} = 1, \ x_{2} = 0) \\
  &= P(p | x_{2} = 0) \qquad \qquad &&\text{(Since } x_{1} \text{ and } x_{2} \text{ are independent.)}\\
  &= \frac{P(p) \cdot P(x_{2} = 0 | p)}{P(x_{2} = 0)} && \text{(} P(x_{2} = 0) \text{ is the rescaling factor.)}\\
  &= \frac{1 \cdot p^{x_{2}}(1 - p)^{1 - x_{2}}}{P(x_{2} = 0)} \\
  &= 2(1 - p)
\end{align}
$$

Combining the influence of the first two data points, we get the parabola-shaped curve as the posterior distribution density function.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.26.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.27.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### e. The Bayesian Interpretation of Weight Decay

<br>

<br>

### f. MacKay's Quick and Dirty Method of Setting Weight Costs

<br>

<br>

### Reading
---


<br><br>
