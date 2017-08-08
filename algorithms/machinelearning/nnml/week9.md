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

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.28.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.29.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.30.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.31.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.32.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.33.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.34.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.35.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

Assumption $1$: the model makes a Gaussian prediction.

$$
\begin{align}
  D|W &\sim Normal(0, \sigma_{D}^{2}) \\
  p(D|W) &= \prod\limits_{i} p(t_{i}|W) = \prod\limits_{i} \frac{1}{\sqrt{2 \pi} \sigma_{D}} e^{-\frac{(t_{i} - y_{i})^2}{2 \sigma_{D}^{2}}} \\
         &= \prod\limits_{i} \frac{1}{\sqrt{2 \pi} \sigma_{D}} e^{-\frac{ \big( t_{i} - f(x_{i}, \ W) \big) ^2}{2 \sigma_{D}^{2}}} \\
  - \log p(D|W) &= - \sum\limits_{i} \log p(t_{i}|W) = \frac{1}{2 \sigma_{D}^{2}} \sum\limits_{i} (t_{i} - y_{i})^2 + k \\
                &= \frac{1}{2 \sigma_{D}^{2}} \sum\limits_{i} \big( t_{i} - f(x_{i}, \ W) \big) ^2 + k
\end{align}
$$

Assumption $2$: Prior distribution of weights $W$ follows a zero-mean Gaussian distribution.

$$
\begin{align}
  W &\sim Normal(0, \sigma_{W}^{2}) \\
  p(W) &= \prod\limits_{j} p(w_{j}) = \prod\limits_{j} \frac{1}{\sqrt{2 \pi} \sigma_{W}} e^{- \frac{w_{j}^{2}}{2 \sigma_{W}^{2}}} \\
  - \log p(W) &= - \sum\limits_{j} \log p(w_{j}) = \frac{1}{2 \sigma_{W}^{2}} \sum\limits_{j} w_{j}^{2} + k
\end{align}
$$

Posterior distribution:

$$
p(W|D) = \frac{p(D|W) \cdot p(W)}{p(D)}
$$

Maximum a Posteriori:

$$
\begin{align}
  argmax_{W} \ p(W|D) &= argmin_{W} \ \bigl\{ - \log p(w|D) \bigr\} \\
  &= argmin_{W} \ \bigl\{ - \log p(D|W) - \log p(W) + \log p(D) \bigr\} \\
  &= argmin_{W} \ \bigl\{ - \log p(D|W) - \log p(W) \bigr\} \\
  &= argmin_{W} \ \Bigg\{ \frac{1}{2 \sigma_{D}^{2}} \sum\limits_{i} \big( t_{i} - f(x_{i}, \ W) \big) ^2 + \frac{1}{2 \sigma_{W}^{2}} \sum\limits_{j} w_{j}^{2} \Bigg\} \\
  &= argmin_{W} \ \Bigg\{ \sum\limits_{i} \big( t_{i} - f(x_{i}, \ W) \big) ^2 + \frac{\sigma_{D}^{2}}{\sigma_{W}^{2}} \sum\limits_{j} w_{j}^{2} \Bigg\} \\
  &= argmin_{W} \ \Bigg\{ \text{ squared error } + \frac{\sigma_{D}^{2}}{\sigma_{W}^{2}} \sum\limits_{j} w_{j}^{2} \Bigg\} \\
\end{align}
$$

<br>

### f. MacKay's Quick and Dirty Method of Setting Weight Costs

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.36.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.37.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.38.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/9.39.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### Reading
---
+ [Week 9 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/slides/Week9.pdf "Week 9 - Ways to Make Neural Networks Generalize Better") <br>

<br><br>
