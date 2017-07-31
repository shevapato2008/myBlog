---
layout: nnml
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Week 4 - Learning Feature Vectors for Words

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

+ Definition: <br>
In mathematics, the **softmax function**, or **normalized exponential function**, is <span style="color:blue">a generalization of the logistic function</span> that "squashes" a $K$-dimensional vector $\boldsymbol{z}$ of arbitrary real values to a $K$-dimensional vector $\sigma (\boldsymbol{z})$ of real values in the range $[0, 1]$ that add up to $1$. [[Wikipedia](https://en.wikipedia.org/wiki/Softmax_function "Softmax function")]

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.4_softmax.png" alt="[Image] Softmax" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 4-4: Softmax</p>

+ Softmax function

$$
y_{i} = \frac{e^{z_{i}}}{\sum\limits_{j \in group} e^{z_{j}}}
$$

+ Derivatives of softmax function:

$$
\boxed{
  \begin{align}
    \text{if } i = j: \qquad \frac{\partial y_{i}}{\partial z_{i}} &= y_{i}(1 - y_{i}) \\
    \text{if } i \neq j: \qquad \frac{\partial y_{i}}{\partial z_{j}} &= - y_{i}y_{j}
  \end{align}
}
$$

Derivation

> $$
\begin{align}
  \text{if } i = j: \qquad \frac{\partial y_{i}}{\partial z_{i}}
  &= \frac{e^{z_{i}} \cdot \sum\limits_{j \in group} e^{z_{j}} - e^{z_{i}} \cdot e^{z_{i}}}{\bigg( \sum\limits_{j \in group} e^{z_{j}} \bigg)^2} \\
  &= y_{i}(1 - y_{i}) \\
  \text{if } i \neq j: \qquad \frac{\partial y_{i}}{\partial z_{j}}
  &= \frac{0 - e^{z_{i}} \cdot e^{z_{j}}}{\bigg( \sum\limits_{j \in group} e^{z_{j}} \bigg)^2} \\
  &= - y_{i}y_{j}
\end{align}
$$

<br>

+ **Cross-Entropy**: the Right Cost Function to Use with Softmax

$$
\boxed{
  \begin{align}
    C &= - \sum\limits_{j} t_{j} \log y_{j} \\
    \text{where} & \\
    t_{j} &= \text{target value}
  \end{align}
}
$$

+ Derivatives of cross-entropy cost function for softmax function
  - C has a very big gradient when the target value is $1$ and the output is almost $0$.
  - The steepness of $\frac{dC}{dy}$ exactly balances the flatness of $\frac{dy}{dz}$.

$$
\boxed{
  \frac{\partial C}{\partial z_{i}} = y_{i} - t_{i}
}
$$

Derivation

> $$
\begin{align}
  \frac{\partial C}{\partial z_{i}} &= \frac{\partial}{\partial z_{i}} \bigg( - t_{i} \log y_{i} - \sum\limits_{j \neq i} t_{j} \log y_{j} \bigg) \\
  &= - t_{i} \cdot \frac{1}{y_{i}} \cdot \frac{\partial y_{i}}{\partial z_{i}} - \sum\limits_{j \neq i} t_{j} \cdot \frac{1}{y_j} \cdot \frac{\partial y_{j}}{\partial z_{i}} \\
  &= - t_{i} (1 - y_{i}) + \sum\limits_{j \neq i} t_{j} y_{i} \\
  &= - t_{i} + y_{i} \sum\limits_{j} t_{j} \\
  &= y_{i} - t_{i}  \qquad (\text{since} \ \sum\limits_{j} t_{j} = 1)
\end{align}
$$

<br>

### d. Neuro-Probabilistic Language Model
---

**A Basic Problem in Speech Recognition**
  + We cannot identify phonemes perfectly in noisy speech
    - The acoustic input is often ambiguous: there are several different words that fit the acoustic signal equally well.
  + People use their understanding of the meaning of the utterance to hear the right words.
  + This means <span style="color:blue;">speech recognizers have to know which words are likely to come next and which are not</span>.
    - Fortunately, words can be predicted quite well without full understanding.

<br>

**The Standard “Trigram” Method**
  + Take a huge amount of text and count the frequencies of all triples of words.
  + Use these frequencies to make bets on the relative probabilities of words given the previous two words:

$$
\frac{p(w_{3} = c | w_{2} = b, w_{1} = a)}{p(w_{3} = d | w_{2} = b, w_{1} = a)} = \frac{count(abc)}{count(abd)}
$$

  + Until very recently this was the state-of-the-art. <span style="color:red;">Drawbacks of trigram method:</span>
    - <span style="color:red;">We cannot use a much bigger context</span> because there are too many possibilities to store and the counts would mostly be zero.
    - <span style="color:red;">The probability is not zero</span> just because the count is zero!

<br>

**Information that the Trigram Model Fails to Use**
  + Suppose we have seen the sentence
    - "the cat got squashed in the garden on friday"
  + This should help us predict words in the sentence
    - "the dog got flattened in the yard on monday"
  + <span style="color:red;">A trigram model does not understand the similarities</span> between
    - cat/dog squashed/flattened garden/yard friday/monday
  + To overcome this limitation, we need to <span style="color:blue;">use the semantic and syntactic features of previous words to predict the features of the next word</span>.
    - Using a feature representation also allows a context that contains many more previous words (e.g. 10).

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.5_bengio-nn.png" alt="[Image] Relational Information" style="width: 600px; margin: auto;"/>
<p style="text-align: center">Figure 4-5: Bengio’s Neural Net for Predicting the Next Word</p>

<br>

**A Problem with Having $\boldsymbol{100,000}$ Output Words**
  + Each unit in the last hidden layer has $100,000$ outgoing weights.
    - So <span style="color:red;">we cannot afford to have many hidden units</span>, unless we have a huge number of training cases.
    - <span style="color:red;">If last hidden layer small, then it's hard to get the $100,000$ probabilities right.</span> The small probabilities are often relevant.
  + Is there a better way to deal with such a large number of outputs?

<br>

### e. Ways to Deal with the Large Number of Possible Outputs in Neuro-Probabilistic Language Models
---

**A Serial Architecture**
  + Try all candidates next words one at a time.
  + This allows the learned feature vector representation to be used for the candidate word.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.6_serial-architecture.png" alt="[Image] Serial Architecture" style="width: 600px; margin: auto;"/>
<p style="text-align: center">Figure 4-6: A Serial Architecture</p>

<br>

**Learning in the Serial Architecture**
  + After computing the <span style="color: blue;">logit score</span> for each candidate word, use all of the logits in a <span style="color: blue;">softmax</span> to get <span style="color: blue;">word probabilities</span>.
  + The difference between the word probabilities and their target probabilities ($y_{i} - t_{i}$) gives cross-entropy error derivatives ($\frac{\partial C}{\partial z_{i}}$).
    - The derivatives try to raise the score of the correct candidate and lower the scores of its high-scoring rivals.
  + We can save a lot of time if we only use a small set of candidates suggested by some other kind of predictor.
    - For example, we could <span style="color: blue;">use the neural net to revise the probabilities of the words that the trigram model thinks are likely</span>.

<br>

**Learning to Predict the Next Word by Predicting a Path Through a Tree (Minih and Hinton, 2009)**
  + Arrange all the words in a binary tree with words as the leaves.
  + Use the previous context to generate a “**prediction vector**”, $\boldsymbol{v}$.
    - Compare $\boldsymbol{v}$ with a learned vector, $\boldsymbol{u}$, at each node of the tree.
    - Apply the logistic function to the scalar product of $\boldsymbol{u}$ and $\boldsymbol{v}$ to predict the probabilities of taking the two branches of the tree.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.7_minih-hinton-tree-1.png" alt="[Image] Minih and Hinton's Binary Tree" style="width: 400px; margin: auto;"/>
<p style="text-align: center">Figure 4-7: Minih and Hinton's Binary Tree</p>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.8_minih-hinton-tree-2.png" alt="[Image] A Picture of the Learning" style="width: 800px; margin: auto;"/>
<p style="text-align: center">Figure 4-8: A Picture of the Learning</p>

<br>

**A Convenient Decomposition**
  + Maximizing the log probability of picking the target word is equivalent to maximizing the sum of the log probabilities of taking all the branches on the path that leads to the target word.
    - So during learning, we only need to consider the nodes on the correct path. This is an exponential win: <span style="color:blue;">$\log N$ instead of $N$</span>.
    - For each of these nodes, we know the correct branch and we know the current probability of taking it so we can get derivatives for learning both the prediction vector $\boldsymbol{v}$ and that node vector $\boldsymbol{u}$.
  + <span style="color:red;">Unfortunately, it is still slow at test time</span>.

<br>

**A Simpler Way to Learn Feature Vectors for Words (Collobert and Weston, 2008)**
  + Learn to judge if a word fits the 5 word context on either side of it.
  + Train on ~600 million examples. Use for many different NLP tasks.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.9_collobert-weston-model.png" alt="[Image] Collobert and Weston Model" style="width: 800px; margin: auto;"/>
<p style="text-align: center">Figure 4-9: Collobert and Weston Model</p>

<br>

**Displaying the Learned Feature Vectors in a 2-D Map**
  + We can get an idea of the quality of the learned feature vectors by displaying them in a 2-D map.
    - <span style="color:blue;">Display very similar vectors very close to each other.</span>
    - Use a multi-scale method called "**t-sne**" that also <span style="color:blue;">displays similar clusters near each other</span>.
  + The learned feature vectors capture lots of subtle semantic distinctions, just by looking at strings of words.
    - No extra supervision is required.
    - The information is all in the contexts that the word is used in.
    - Consider "<span style="color:blue;">She scrommed him with the frying pan.</span>"

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.10_2D-map-1.png" alt="[Image] 2D Map 1" style="width: 400px; margin: auto;"/>
<p style="text-align: center">Figure 4-10: 2D Map 1</p>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.11_2D-map-2.png" alt="[Image] 2D Map 2" style="width: 500px; margin: auto;"/>
<p style="text-align: center">Figure 4-11: 2D Map 2</p>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/4.12_2D-map-3.png" alt="[Image] Collobert and Weston Model" style="width: 600px; margin: auto;"/>
<p style="text-align: center">Figure 4-12: 2D Map 3</p>

<br>

### Reading
---
+ [Week 4 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/slides/Week4.pdf "Week 4 - Learning Feature Vectors for Words") <br>
+ Y. Bengio, R. Ducharme, P. Vincent, and C. Janvin. A neural probabilistic language model. _Journal of Machine Learning Research_, 3:1137–1155, 2003.
[[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/A Neural Probabilistic Language Model.pdf)]<br>

**More**
+ Softmax Function
  - [Softmax Function (Wikipedia)](https://en.wikipedia.org/wiki/Softmax_function "Softmax function")
  - [Softmax classification function - Peter's Notes](http://peterroelants.github.io/posts/neural_network_implementation_intermezzo02/ "Peter's Notes")
+ Activation Function
  - [Activation Function (Wikipedia)](https://en.wikipedia.org/wiki/Activation_function "Activation function")
  - [http://www.cs.toronto.edu/~guerzhoy/411/lec/W04/activationfn.pdf](http://www.cs.toronto.edu/~guerzhoy/411/lec/W04/activationfn.pdf)
  - [https://www.youtube.com/watch?v=9vB5nzrL4hY](https://www.youtube.com/watch?v=9vB5nzrL4hY)
  - [https://deeplearning.web.unc.edu/files/2016/11/DLJC_pres.pdf](https://deeplearning.web.unc.edu/files/2016/11/DLJC_pres.pdf)
