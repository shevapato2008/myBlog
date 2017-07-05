---
layout: algorithm
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
---

## Week 2 - The Perceptron learning procedure

### Lecture 2a - An Overview of the Main Types of Neural Network Architecture

`1.` Feed-Forward Neural Networks

  + commonest type of neural network in practice
  + input layer, hidden layer, and output layer
  + number of hidden layers >= 2 => **deep neural networks**
  + The activities of the neurons in each layer are a **non-linear** function of the activities in the layer below

    <img src="{{site.baseurl}}/algorithms/machinelearning/nnml/2.1_feed-forward-nn.png" alt="[Image] Feed-Forward Neural Network" style="width: 300px; align: middle;"/>
    <p style="align: middle;">Figure: Feed-Forward Neural Network</p>

`2.` Recurrent Neural Networks (RNN)

  + directed cycles in their connection graph: you may get back to the starting point
  + complicated dynamics => more difficult to train
  + more biologically realistic

    <img src="{{site.baseurl}}/algorithms/machinelearning/nnml/2.2_recurrent-nn.png" alt="[Image] Recurrent Neural Network" style="width: 200px; align: middle;"/>
    <p style="align: middle;">Figure: Recurrent Neural Network</p>

  Recurrent NN for modeling sequences
  + a very natural way to model sequential data
    - **equivalent to very deep nets with one hidden layer per time slice**
    - exception 1: use the same weights at every time slice
    - exception 2: get input at every time slice
  + can remember information in their hidden states for a long time
    - but hard to train them to use this potential

  An example of RNN:
  + Ilya Sutskever (2011) trained a special type of recurrent neural net to predict the next character in a sequence.

`3.` Symmetrically Connected Networks (SCN)
  + like RNN, but connection between units are symmetrical
    - same weight in both directions
    - more restricted: obey an energy function, cannot model cycles
  + SCN without hidden units => **Hopfield Nets**
  + SCN with hidden units => **Boltzmann Machines**
    - more powerful models than Hopfield nets
    - less powerful than RNNs
    - simple learning algorithm

<br>

### Lecture 2b - Perceptrons: The First Generation of Neural Networks




<br><br>

[Week 2 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/Week2.pdf "Week 2 - The Perceptron learning procedure")
