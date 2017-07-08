---
layout: algorithm
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Week 2 - The Perceptron learning procedure

### a. An Overview of the Main Types of Neural Network Architecture
---
**`1.` Feed-Forward Neural Networks**

  + commonest type of neural network in practice
  + input layer, hidden layer, and output layer
  + number of hidden layers >= 2 => **deep neural networks**
  + The activities of the neurons in each layer are a **non-linear** function of the activities in the layer below

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/2.1_feed-forward-nn.png" alt="[Image] Feed-Forward Neural Network" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 2-1: Feed-Forward Neural Network</p>

**`2.` Recurrent Neural Networks (RNN)**

  + directed cycles in their connection graph: you may get back to the starting point
  + complicated dynamics => more difficult to train
  + more biologically realistic

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/2.2_recurrent-nn.png" alt="[Image] Recurrent Neural Network" style="width: 200px; margin: auto;"/>
<p style="text-align: center">Figure 2-2: Recurrent Neural Network</p>

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

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/2.3_perceptron-architecture.png" alt="[Image] Perceptron Architecture" style="width: 250px; margin: auto;"/>
<p style="text-align: center">Figure 2-3: Perceptron Architecture</p>

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

**Weight Space**
  + one dimension per weight
  + a point in weight space = a particular setting of all the weights $(w_{1}, w_{2}, ..., w_{p})$
  + assume we have eliminated the threshold --> each training case = a hyperplane through the origin
    - weights must lie on one side of this hyperplane to get the answer correct
  + each training case $(\boldsymbol{x})_{i = 1}^{m}$ defines a plane (black line)
    - the plane goes through the origin and is perpendicular to the **_input vector_**
    - on one side of the plane the output is wrong because the scalar product of the weight vector with input vector has the wrong sign

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/2.4_weight-space-1.png" alt="[Image] Weight Space 1" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 2-4: Weight Space of Perceptrons - 1st input vector</p>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/2.5_weight-space-2.png" alt="[Image] Weight Space 1" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 2-5: Weight Space of Perceptrons - 2nd input vector</p>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/2.6_weight-space-3.png" alt="[Image] Weight Space 1" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 2-6: Weight Space of Perceptrons - combined effect</p>

  + to get all training cases right we need to find a point on the right side of all the planes
    - there might not be such a point (weight vector)
  + if there exits such weight vectors, they lie in the **_hyper-cone_** with its apex at the origin
    - so the average of two good weight vectors is a good weight vector
    - <span style="color: red;">the problem is convex</span>

<br>

### d. Why the Learning Works?
---

**Why the Learning Procedure Works (First Attempt)**
  + So consider “generously feasible” weight vectors that lie within the feasible region by a margin at least as great as the length of the input vector that defines each constraint plane.
    - Every time the perceptron makes a mistake, the squared distance to all of these generously feasible weight vectors is always decreased by at least the squared length of the update vector.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/2.7_why-learning-works.png" alt="[Image] Why Learning Works" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 2-7: Why Learning Procedure Works</p>

**Informal Sketch of Proof of Convergence**
  + Each time the perceptron makes a mistake, the current weight vector moves to decrease its squared distance from every weight vector in the “generously feasible” region.
  + The squared distance decreases by at least the squared length of the input vector.
  + So after a finite number of mistakes, the weight vector must lie in the feasible region <span style="color: red;">if this region exists</span>.

<br>

### e. What Perceptrons Can't Do?
---

**The Limitations of Perceptrons**
  + If you are allowed to choose the features by hand and if you use enough features, you can do almost anything.
    -  For binary input vectors, we can have a separate feature unit for each of the exponentially many binary vectors and so we can make any possible discrimination on binary input vectors.
  + But once the hand-coded features have been determined, there are very strong limitations on what a perceptron can learn.

**A Geometric View of What Binary Threshold Neurons Cannot Do**
  + Imagine “**data-space**” in which the axes correspond to components of an input vector.
    - Each _**input vector**_ is _**a point**_ in this space.
    - A _**weight vector**_ defines _**a plane**_ in data-space.
    - The weight plane is perpendicular to the weight vector and misses the origin by a distance equal to the threshold.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/2.8_limitation-of-binary-threshold.png" alt="[Image] Limitation of Binary Threshold Neurons" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 2-8: Limitation of Binary Threshold Neurons</p>

**Discriminating Simple Patterns Under Translation With Wrap-Around**
  + Suppose we just use pixels as the features.
  + Can a binary threshold unit discriminate between different patterns that have the same number of on pixels?
    - <span style="color: red;">Not if the patterns can translate with wrap-around!</span>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/2.9_patterns-with-wrap-around.png" alt="[Image] Patterns With Wrap-Around" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 2-9: Patterns With Wrap-Around</p>

**Why This Result Is Devastating for Perceptrons**
  + The whole point of pattern recognition is to recognize patterns despite transformations like translation.
  + Minsky and Papert’s “**Group Invariance Theorem**” says that the part of a Perceptron that learns cannot learn to do this <span style="color: red;">if the transformations form a group</span>.
    - Translations with wrap-around form a group.
  + To deal with such transformations, a Perceptron needs to use multiple feature units to recognize transformations of informative sub-patterns.
    - <span style="color: red;">So the tricky part of pattern recognition must be solved by the hand-coded feature detectors, not the learning procedure.</span>

**Learning With Hidden Units**
  + Networks without hidden units are very limited in the input-output mappings they can learn to model.
    - <span style="color: red;">More layers of linear units do not help. Its still linear.</span>
    - Fixed output non-linearities are not enough.
  + We need multiple layers of <span style="color: red;">adaptive, non-linear hidden units</span>. But how can we train such nets?
    - We need an efficient way of adapting <span style="color: red;">all</span> the weights, not just the last layer. This is hard.
    - <span style="color: red;">Learning the weights going into hidden units is equivalent to learning features.</span>
    - This is difficult because nobody is telling us directly what the hidden units should do.

<br>

### Reading
---
[Week 2 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/Week2.pdf "Week 2 - The Perceptron learning procedure")

<br>
