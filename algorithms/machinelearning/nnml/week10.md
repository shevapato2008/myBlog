---
layout: nnml
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Week 10 - Combining Multiple Neural Networks to Improve Generalization

<br>

### a. Why it Helps to Combine Models?

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.1.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.2.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.3.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.4.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.5.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.6.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.7.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.8.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

**Bagging vs. Boosting** [**[Quora]**](https://www.quora.com/Whats-the-difference-between-boosting-and-bagging "What's the difference between boosting and bagging?")

Boosting and bagging are similar, in that they are both ensemble methods, where a number of weak learners (classifiers/regressors that are barely better than guessing) combine (through averaging or max vote) to create a strong learner that can make accurate predictions. Bagging means that you take bootstrap samples (with replacement) of your data set and each sample trains a (potentially) weak learner. Boosting, on the other hand, uses all data to train each learner, but instances that were misclassified by the previous learners are given more weight so that subsequent learners give more focus to them during training.

+ **Bootstrap Aggregating / Bagging** [**[Wikipedia]**](https://en.wikipedia.org/wiki/Bootstrap_aggregating "Bootstrap Aggregating")
+ **Bootsting** [**[Wikipedia]**](https://en.wikipedia.org/wiki/Boosting_(machine_learning) "Boosting")

<br>

### b. Mixture Experts

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.9.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.10.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.11.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.12.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.13.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.14.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.15.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.16.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.17.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.18.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.19.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.20.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### c. The Idea of Full Bayesian Learning

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.21.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.22.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.23.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.24.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.25.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.26.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### d. Making Full Bayesian Learning Practical

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.27.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.28.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.29.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.30.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.31.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.32.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### e. Dropout

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.33.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.34.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.35.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.36.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.37.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.38.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.39.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.40.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/10.41.png" alt="[Image] slide image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### Reading
---
+ [Week 10 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/slides/Week10.pdf "Week 10 - Combining Multiple Neural Networks to Improve Generalization") <br>
+ R.A. Jacobs, M.I. Jordan, S.J. Nowlan, and G.E. Hinton, "Adaptive Mixtures of Local Experts," _Neural Computation_, vol. 3, pp. 79-87, 1991. [[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/Adaptive Mixtures of Local Experts.pdf)]<br>
+ G.E. Hinton, N. Srivastava, A. Krizhevsky, I. Sutskever, and R.R. Salakhutdinov. Improving neural networks by preventing co-adaptation of feature detectors. _arXiv preprint arXiv:1207.0580_, 2012. [[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/Improving neural networks by preventing co-adaptation of feature detectors.pdf)]<br>

**More**
+ Ahn, S., Balan, A. K., and Welling, M. Bayesian posterior sampling via stochastic gradient Fisher scoring. In _ICML_, 2012. [[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/Bayesian posterior sampling via stochastic gradient Fisher scoring.pdf)]<br>

<br><br>
