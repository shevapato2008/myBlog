---
layout: algorithm
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Week 4 - The Backpropagation Learning Procedure

### a. Learning to Predict the Next Word
---

**A Simple Example of Relational Information**

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.1_relational-info.png" alt="[Image] Relational Information" style="width: 450px; margin: auto;"/>
<p style="text-align: center">Figure 4-1: An Example of Relational Information</p>

<br>

**Another Way to Express the Same Information**
  + Make a set of propositions using the <span style="color:blue;">12 relationships</span>:
    - son, daughter, nephew, niece, father, mother, uncle, aunt, brother, sister, husband, wife
  + Example 1:
    - (1) colin has-father james
    - (2) colin has-mother victoria
    - (1) & (2) => james has-wife victoria
  + Example 2:
    - (3) charlotte has-brother colin
    - (4) victoria has-brother arthur
    - (1), (2), (3), (4) => charlotte has-uncle arthur

<br>

**A Relational Learning Task**
  + A large set of <span style="color:blue;">triples</span> from some family trees => <span style="color:blue;">regularities</span>
    - Regularities in <span style="color:blue;">symbolic rules</span>:<br>
    (x has-mother y) & (y has-husband z) => (x has-father z)
  + Task: find symbolic rules via searching through a very large <span style="color:blue;">discrete space of possibilities</span>
  + Question: can a NN capture the same knowledge by searching through a <span style="color:blue;">continuous space of weights</span>?

<br>

**The Structure of the Neural Net**

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.2_nn-structure.png" alt="[Image] NN Structure" style="width: 600px; margin: auto;"/>
<p style="text-align: center">Figure 4-2: The Structure of the Neural Net</p>

<br>

**What the Network Learns**
  + The six hidden units in the bottleneck connected to the input representation of person 1 learn to represent features of people that are useful for predicting the answer.
    - Nationality, generation, branch of the family tree.
  + These features are only useful if the other bottlenecks use similar representations and the central layer learns how features predict other features. For example:
    - Input person is of generation 3 and
    - relationship requires answer to be one generation up
    - (implies) Output person is of generation 2

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.3_six-hidden-units.png" alt="[Image] Six Hidden Units" style="width: 600px; margin: auto;"/>
<p style="text-align: center">Figure 4-3: Six Hidden Units and Relational Map</p>

<br>

**Another Way to See that it Works**
  + Train the network on all but 4 of the triples that can be made using the 12 relationships
    - It needs to sweep through the training set many times adjusting the weights slightly each time.
  + Then test it on the 4 held-out cases.
    - It gets about 3/4 correct.
    - This is good for a 24-way choice.
    - On <span style="color:blue;">much bigger datasets</span> we can train on a <span style="color:blue;">much smaller fraction</span> of the data.

<br>

**A Large-Scale Example**
  + Suppose we have a database of millions of relational facts of the form <span style="color:blue;">(A R B)</span>.
    - We could train a net to discover feature vector representations of the terms that <span style="color:blue;">allow the third term to be predicted from the first two</span>.
    - Then we could use the trained net to find very unlikely triples. These are good candidates for errors in the database.
  + Instead of predicting the third term, we could use all three terms as input and predict the <span style="color:blue;">probability</span> that the fact is correct.
    - To train such a net we <span style="color:blue;">need a good source of false facts</span>.

<br>



### b. A Brief Diversion into Cognitive Science
---

**What the Family Trees Example Tells Us About Concepts**
  + A long debate in cognitive science between two rival theories of what it means to have a concept
    - **The Feature Theory**: A concept is a set of <span style="color:blue;">semantic features</span>.
      * This is good for <span style="color:blue;">explaining similarities between concepts</span>.
      * Its convenient: a concept is a vector of feature activities.

    - **The Structuralist Theory**: The meaning of a concept <span style="color:blue;">lies in its relationships to other concepts</span>.
      * So conceptual knowledge is best expressed as a <span style="color:blue;">relational graph</span>.
      * Minsky used the limitations of perceptrons as evidence against feature vectors and in favor of relational graph representations.

<br>

**Both Sides are Wrong**
  + These two theories need not be rivals. A neural net can use vectors of semantic features to implement a relational graph.
    - In the neural network that learns family trees, <span style="color:blue;">no explicit inference is required to arrive at the intuitively obvious consequences</span> of the facts that have been explicitly learned.
    - The net can “intuit” the answer in a forward pass.
  + We may use explicit rules for conscious, deliberate reasoning, but we do a lot of commonsense, analogical reasoning by just “seeing” the answer with no conscious intervening steps.
    - Even when we are using explicit rules, we need to just see which rules to apply.

<br>

**Localist and Distributed Representations of Concepts**
  + The obvious way to implement a relational graph in a neural net is to treat a neuron as a node in the graph and a connection as a binary relationship. But <span style="color:red;">this “localist” method will not work</span>:
    - We need many different types of relationship and the connections in a neural net do not have discrete labels.
    - We need ternary relationships as well as binary ones.<br>
    e.g. A is between B and C.
  + <span style="color:red;">The right way to implement relational knowledge in a neural net is still an open issue.</span>
    - But many neurons are probably used for each concept and each neuron is probably involved in many concepts. This is called a “**distributed representation**”.

<br>

### c. Another Diversion: The Softmax Output Function
---

**Problems with squared error**
  + The squared error measure has some drawbacks:
    - If the desired output is 1 and the actual output is 0.00000001 there is almost no gradient for a logistic unit to fix up the error.
    - If we are trying to assign probabilities to mutually exclusive class labels, we know that the outputs should sum to 1, but we are depriving the network of this knowledge.
  + Is there a different cost function that works better?
    - Yes: <span style="color:blue;">Force the outputs to represent a probability distribution across discrete alternatives.</span>

<br>

**<span style="color:blue;">Softmax</span>**

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.4_softmax.png" alt="[Image] Softmax" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 4-4: Softmax</p>

Formula:

$$
\boxed{
  \begin{align}
    y_{i} &= \frac{e^{z_{i}}}{\sum\limits_{j \in group} e^{z_{j}}} \\
    \frac{\partial y_{i}}{\partial z_{i}} &= y_{i}(1 - y_{i})
  \end{align}
}
$$

Derivation:

> $$
\begin{align}
  \frac{\partial y_{i}}{\partial z_{i}} &= \frac{e^{z_{i}} \cdot \sum\limits_{j \in group} e^{z_{j}} - e^{z_{i}} \cdot e^{z_{i}}}{\bigg( \sum\limits_{j \in group} e^{z_{j}} \bigg)^2} \\
  &= \frac{e^{z_{i}}}{\sum\limits_{j \in group} e^{z_{j}}} - \bigg( \frac{e^{z_{i}}}{\sum\limits_{j \in group} e^{z_{j}}} \bigg)^{2} \\
  &= y_{i} - (y_{i})^{2} \\
  &= y_{i}(1 - y_{i})
\end{align}
$$

<br>

**Cross-Entropy: the Right Cost Function to Use with Softmax**
  + The right cost function

$$
\boxed{
  \begin{align}
    C &= - \sum\limits_{j} t_{j} \log y_{j} \\
    \text{where} & \\
    t_{j} &= \text{target value}
  \end{align}
}
$$

  + C has a very big gradient when the target value is 1 and the output is almost 0.








<br>
### Reading
---
+ [Week 4 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/slides/Week4.pdf "Week 4 - Learning Feature Vectors for Words") <br>
+ Y. Bengio, R. Ducharme, P. Vincent, and C. Janvin. A neural probabilistic language model. _Journal of Machine Learning Research_, 3:1137–1155, 2003.
[[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/A Neural Probabilistic Language Model.pdf)]<br>

**More**
+ Activation Function
  - http://www.cs.toronto.edu/~guerzhoy/411/lec/W04/activationfn.pdf
  - https://www.youtube.com/watch?v=9vB5nzrL4hY
  - https://deeplearning.web.unc.edu/files/2016/11/DLJC_pres.pdf
