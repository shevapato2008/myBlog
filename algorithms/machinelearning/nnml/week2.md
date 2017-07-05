---
layout: algorithm
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
---

## Week 2 - The Perceptron learning procedure

### a. An Overview of the Main Types of Neural Network Architecture
---
**`1.` Feed-Forward Neural Networks**

  + commonest type of neural network in practice
  + input layer, hidden layer, and output layer
  + number of hidden layers >= 2 => **deep neural networks**
  + The activities of the neurons in each layer are a **non-linear** function of the activities in the layer below

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/2.1_feed-forward-nn.png" alt="[Image] Feed-Forward Neural Network" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure: Feed-Forward Neural Network</p>

**`2.` Recurrent Neural Networks (RNN)**

  + directed cycles in their connection graph: you may get back to the starting point
  + complicated dynamics => more difficult to train
  + more biologically realistic

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/2.2_recurrent-nn.png" alt="[Image] Recurrent Neural Network" style="width: 200px; margin: auto;"/>
<p style="text-align: center">Figure: Recurrent Neural Network</p>

  Recurrent NN for modeling sequences
  + a very natural way to model sequential data
    - **equivalent to very deep nets with one hidden layer per time slice**
    - exception 1: use the same weights at every time slice
    - exception 2: get input at every time slice
  + can remember information in their hidden states for a long time
    - but hard to train them to use this potential

  An example of RNN:
  + Ilya Sutskever (2011) trained a special type of recurrent neural net to predict the next character in a sequence.

**`3.` Symmetrically Connected Networks (SCN)**
  + like RNN, but connection between units are symmetrical
    - same weight in both directions
    - more restricted: obey an energy function, cannot model cycles
  + SCN without hidden units => **Hopfield Nets**
  + SCN with hidden units => **Boltzmann Machines**
    - more powerful models than Hopfield nets
    - less powerful than RNNs
    - simple learning algorithm

<br>

### b. Perceptrons: The First Generation of Neural Networks
---
**Standard Paradigm for Statistical Pattern Recognition**
  1. convert raw input vector => a vector of feature activations
  2. learn to weight each feature activation => a scalar
  3. compare scalar with a threshold and decide if input vector is a positive example of target class

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/2.3_perceptron-architecture.png" alt="[Image] Perceptron Architecture" style="width: 250px; margin: auto;"/>
<p style="text-align: center">Figure: Perceptron Architecture</p>

**History of Perceptrons**
  + popularized by Frank Rosenblatt in the early 1960's
  + In 1969, Minsky and Papert analysed what they can do and showed their limitations
  + still widely used today for tasks with enormous feature vectors that contain many millions of features

**Binary Threshold Neurons (Decision Units)**

$$
z = b + \sum_{i} x_{i}w_{i}
$$

$$
y =
\left\{
  \begin{array}{rcl}
    1 & \mbox{if} \ z \geq 3 \\
    0 & \mbox{otherwise}
  \end{array}
\right.
$$

  + Note: A **bias** is treated as an extra input line that always has an activity of 1.

**Perceptron Convergence Procedure: Training Binary Output Neurons as Classifiers**
  + For each iteration:
    - if output unit is correct, leave its weight alone
    - if output unit _incorrectly_ outputs a 0, add input vector to weight vector
    - if output unit _incorrectly_ outputs a 1, subtract input vector from weight vector
  + This is guaranteed to find a set of weights that gets the right answer for all training cases <span style="color:red">if any such set exits</span>.

<br>

### c. A Geometrical View of Perceptrons
---

To be continued.

<br>

### Reference
---
[[Week 2 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/Week2.pdf "Week 2 - The Perceptron learning procedure")]

<br>
