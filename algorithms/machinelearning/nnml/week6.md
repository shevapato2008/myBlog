---
layout: nnml
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Week 6 - Optimization: How to Make the Learning Go Faster

<br>

### a. Overview of Mini-Batch Gradient Descent

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.1.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.2.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.3.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.4.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.5.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.6.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.7.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### b. A Bag of Tricks for Mini-Batch Gradient Descent

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.8.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.9.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.10.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.11.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.12.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.13.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.14.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.15.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### c. The Momentum Method

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.16.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.17.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.18.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.19.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.20.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.21.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### d. Adaptive Learning Rates for Each Connection

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.22.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.23.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.24.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.25.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### e. Rmsprop: Divide the Gradient by a Running Average of Its Recent Magnitude

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.26.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.27.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/6.28.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### Reading
---
+ [Week 6 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/slides/Week6.pdf "Week 6 - Optimization: How to Make the Learning Go Faster") <br>
+ I. Sutskever, J. Martens, G. E. Dahl, and G. E. Hinton. On the importance of initialization and momentum in deep learning. In _ICML_, volume 28 of _JMLR Proceedings_, pages 1139–1147. JMLR.org, 2013. [[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/sutskever13.pdf)]<br>

<br><br>
