---
layout: nnml
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Week 7 - Recurrent Neural Networks

<br>

### a. Modeling Sequences: A Brief Overview

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.1.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.2.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.3.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.4.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.5.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.6.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.7.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.8.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.9.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.10.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### b. Training RNNs with Backpropagation

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.11.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.12.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.13.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.14.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.15.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.16.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.17.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### c. A Toy Example of Training An RNN

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.18.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.19.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.20.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.21.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.22.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.23.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.24.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### d. Why it is Difficult to Train an RNN

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.25.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.26.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.27.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.28.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.29.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### e. Long-Term Short-Term Memory

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.30.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.31.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.32.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.33.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.34.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/7.35.png" alt="[Image] quiz image" style="width: 800px; margin: 10px; border: 1px solid black;"/>

<br>

### Reading
---
+ [Week 7 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/slides/Week7.pdf "Week 7 - Recurrent Neural Networks") <br>
+ M. Liwicki, A. Graves, S. Fernandez, H. Bunke, and J. Schmidhuber. A novel approach to on-line handwriting recognition based on bidirectional long short-term memory networks. In _Proc. 9th Int. Conf. on Document Analysis and Recognition_, Curitiba, Brazil, Sep. 2007. [[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/A Novel Approach to On-Line Handwriting Recognition Based on Bidirectional Long Short-Term Memory Networks.pdf)]<br>

**More**
+ About the HF optimizer:<br>
J. Martens, I. Sutskever, "Learning Recurrent Neural Networks with Hessian-Free Optimization", _Proc. Int'l Conf. Machine Learning_, 2011. [[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/Learning Recurrent Neural Networks with Hessian-Free Optimization.pdf)]<br>
+ The original paper for Long Short Term Memory (LSTM):<br>
S. Hochreiter and J. Schmidhuber. Long short-term memory. _Neural computation_, 9(8):1735–1780, 1997.
[[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/lstm.pdf)]<br>
+ Graves, A., & Schmidhuber, J. (2009). Offline handwriting recognition with multidimensional recurrent neural networks. In _Advances in neural information processing systems (NIPS)_, vol. 21 (pp. 545–552). Cambridge, MA: MIT Press [[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/Offline Handwriting Recognition with Multidimensional Recurrent Neural Networks.pdf)]<br>

<br><br>
