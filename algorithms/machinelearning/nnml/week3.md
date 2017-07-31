---
layout: nnml
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Week 3 - The Backpropagation Learning Procedure

### a. Learning the Weights of A Linear Neuron
---
**Why the Perceptron Learning Procedure Cannot Be Generalised to Hidden Layers**
  + Perceptron convergence: weights --> every “generously feasible” set of weights
    - cannot be extended to more complex networks in which the average of two good solutions may be a bad solution
  + "multi-layer" NN do not use the perceptron learning procedure
    - no "multi-layer perceptrons"

**A Different Way to Show that A Learning Procedure Makes Progress**
  + Instead of showing the weights get closer to a good set of weights, <span style="color:red">show that the actual output values get closer the target values.</span>
    - This can be true even for non-convex problems in which there are many quite different sets of weights that work well and averaging two good sets of weights may give a bad set of weights.
    - not true for perceptron learning
  + Simplest example: a linear neuron with a squared error measure

**Linear Neurons (Also Called Linear Filters)**
  + The neuron has a real-valued output which is a weighted sum of its inputs.
  + The aim of learning is to minimize the error summed over all training cases.
    - The error is the squared difference between the desired output and the actual output.

$$
\begin{align}
y &= \sum_{i} w_{i} x_{i} = \boldsymbol{w}^{T} \boldsymbol{x} \\
\text{where} \quad & \\
y &= \text{neuron's estimate of the desired output} \\
\boldsymbol{w} &= \text{weight vector} \\
\boldsymbol{x} &= \text{input vector}
\end{align}
$$

**Why Don’t We Solve It Analytically?**
  + It is straight-forward to write down a set of equations, one per training case, and to solve for the best set of weights.
    - This is the standard engineering approach so why don’t we use it?
  + <span style="color:red;">Scientific answer</span>: We want a method that real neurons could use.
  + <span style="color:red;">Engineering answer</span>: We want a method that can be generalized to multi-layer, non-linear neural networks.
    - The analytic solution relies on it being linear and having a squared error measure.
    - <span style="color:red;">Iterative methods are usually less efficient but they are much easier to generalize.</span>

**A Toy Example to Illustrate the Iterative Method**

  Setting:<br>
  + Each day you get lunch at the cafeteria.
    - Your diet consists of fish, chips, and ketchup.
    - You get several portions of each.
  + The cashier only tells you the total price of the meal
    - After several days, you should be able to figure out the price of each portion.
  + The iterative approach: Start with random guesses for the prices and then adjust them to get a better fit to the observed prices of whole meals.

  Solving the equations iteratively:<br>
  + Each meal price gives a linear constraint on the prices of the portions:

$$
price = x_{fish} w_{fish} + x_{chips} w_{chips} + x_{ketchup} w_{ketchup}
$$

  + The prices of the portions are like the weights in of a linear neuron.

$$
\boldsymbol{w} = (w_{fish}, w_{chips}, w_{ketchup})
$$

  + We will start with guesses for the weights and then adjust the guesses slightly to give a better fit to the prices given by the cashier.

  The <span style="color:red;">true weights</span> used by the cashier<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/3.1_true-weights.png" alt="[Image] True Weights" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 3-1: True Weights Used by the Cashier</p>

  A model of the cashier with arbitrary initial weights<br>
  + Initial weights $w_{1} = w_{2} = w_{3} = 50$

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/3.2_model-arbitrary-initial-weights.png" alt="[Image] Model with Arbitrary Initial Weights" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 3-2: Model with Arbitrary Initial Weights</p>

  + Residual error = 350
  + The "**delta rule**" for learning is:

$$
\Delta w_{i} = \epsilon x_{i} (t - y)
$$

  + With a learning rate $\epsilon = 1/35$, the weight changes are:
    - $\Delta w_{1} = +20$
    - $\Delta w_{2} = +50$
    - $\Delta w_{3} = +30$

  + This gives new weights of 70, <span style="color:red;">100</span>, 80.
    - <span style="color:red;">Notice that weights for chips got worse!</span>

**Deriving the Delta Rule**
  + Define the error as the squared residuals summed over all training cases:

$$
E = \frac{1}{2} \sum_{n \in training} (t^{n} - y^{n})^2
$$

  + Differentiate to get error derivatives for weights

$$
\begin{align}
\frac{\partial E}{\partial w_{i}} &= \frac{1}{2} \sum_{n} \frac{\partial y^{n}}{\partial w_{i}} \frac{d E^{n}}{d y^{n}} \\
&= - \sum_{n} x_{i}^{n}(t^{n}-y^{n})
\end{align}
$$

  + The **<span style="color:red;">batch</span> delta rule** changes the weights in proportion to their error derivatives summed over all training cases

$$
\Delta w_{i} = - \epsilon \cdot \frac{\partial E}{\partial w_{i}} = \sum_{n} \epsilon \cdot x_{i}^{n} \cdot (t^{n} - y^{n})
$$

Derivation: <br>
Assuming that there are<br>
``-`` $m$ data points in the training set;<br>
``-`` $p$ dimensions for each data point;
> $$
\begin{align}
  E &= \frac{1}{2} \sum_{i=1}^{m} E^{(i)} = \frac{1}{2} \sum_{i=1}^{m} (t^{(i)} - y^{(i)})^{2} \\
  \frac{\partial E}{\partial w_{j}} &= \frac{1}{2} \sum_{i=1}^{m} \frac{\partial E^{(i)}}{\partial w_{j}} \qquad &&\text{for} \ j = 1, 2, ..., p \\
  &= \frac{1}{2} \sum_{i=1}^{m} \frac{\partial E^{(i)}}{\partial y^{(i)}} \cdot \frac{\partial y^{(i)}}{\partial w_{j}} &&\text{(chain rule)}\\
  &= \frac{1}{2} \sum_{i=1}^{m} 2 (t^{(i)} - y^{(i)}) (-1) \cdot x_{j}^{(i)} &&(\text{since} \ \frac{\partial y^{(i)}}{\partial w_{j}} = \frac{\partial \sum_{j=1}^{p} w_{j} x_{j}^{(i)}}{\partial w_{j}}) \\
  &= - \sum_{i=1}^{m} x_{j}^{(i)} \cdot (t^{(i)} - y^{(i)}) \\
  \Delta w_{j} &= - \epsilon \cdot \frac{\partial E}{\partial w_{j}} = \sum_{i=1}^{m} \epsilon \cdot x_{j}^{(i)} \cdot (t^{(i)} - y^{(i)}) &&\text{for} \ j = 1, 2, ..., p \\
\end{align}
$$

**Behavior of the Iterative Learning Procedure**
  + Does the learning procedure eventually get the right answer?
    - There may be no perfect answer.
    - By making the learning rate small enough we can get as close as we desire to the best answer.
  + How quickly do the weights converge to their correct values?
    - <span style="color:red;">It can be very slow if two input dimensions are highly correlated</span>.
    - Example: If you almost always have the same number of portions of ketchup and chips, it is hard to decide how to divide the price between ketchup and chips.

**The Relationship between the Online Delta-Rule and the Learning Rule for Perceptrons**
  + Perceptron: we increment or decrement the weight vector by the input vector <span style="color:blue;">$x^{(i)}$</span>.
    - But we <span style="color:red;">only change the weights when we make an error</span>.
  + Online Delta-Rule: we increment or decrement the weight vector by the input vector <span style="color:blue;">$x^{(i)}$</span> <span style="color:red;">scaled by</span> the residual error <span style="color:red;">$(t^{(i)} - y^{(i)})$</span> and the learning rate <span style="color:red;">$\epsilon$</span>.
    - So we have to choose a learning rate. This is annoying.

<div style="background-color: #ffffc8; padding: 2px;">
$$
\Delta w_{j} = \sum_{i=1}^{m} \epsilon \cdot x_{j}^{(i)} \cdot (t^{(i)} - y^{(i)}) \qquad \text{for} \ j = 1, 2, ..., p
$$
</div>

<br>



### b. The Error Surface for a Linear Neuron
---

**The Error Surface in Extended Weight Space**
  + The error surface lies in a space with a horizontal axis for each weight and one vertical axis for the error.
  + For a **linear** neuron with a **squared error**, it is a _quadratic bowl_.
    - Vertical cross-sections are parabolas.
    - Horizontal cross-sections are ellipses.
  + For **multi-layer, non-linear** nets the error surface is much more complicated.

**Online vs. Batch Learning**
  + The simplest kind of **batch learning** does steepest descent on the error surface.
    - travels perpendicular to the contour lines
  + The simplest kind of **online learning** zig-zags around the direction of steepest descent

<div style="text-align:center;">
  <div style="display: inline-block;">
    <img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/3.3_batch-learning.png" alt="[Image] Batch Learning" style="width: 200px; margin: auto;"/>
    <p style="text-align: center">Figure 3-3: Batch Learning</p>
  </div>
  <div style="display: inline-block;">
    <img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/3.4_online-learning.png" alt="[Image] Online Learning" style="width: 300px; margin: auto;"/>
    <p style="text-align: center">Figure 3-4: Online Learning</p>
  </div>
</div>

**Why Learning Can be Slow**
  + <span style="color:red">If the ellipse is very elongated</span>, the direction of steepest descent is almost <span style="color:red">perpendicular</span> to the direction towards the minimum!
    - The red gradient vector has a large component along the short axis of the ellipse and a small component along the long axis of the ellipse.
    - This is just the opposite of what we want.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/3.5_elongated-eclipse.png" alt="[Image] Elongated Eclipse" style="height: 250px; width: 250px; margin: auto;"/>
<p style="text-align: center">Figure 3-5: Elongated Eclipse => Slow Learning</p>

<br>



### c. Learning the Weights of a Logistic Output Neuron

**Logistic Neurons**
  + These give a _real-valued output_ that is a _smooth_ and _bounded_ function of their total input.
  + nice derivatives --> make learning easy

$$
\begin{align}
z &= b + \sum_{i} x_{i} w_{i} \\
y &= \frac{1}{1 + e^{-z}}
\end{align}
$$

**The Derivatives of a Logistic Neuron**
  + The derivatives of the logit, $z$, with respect to the inputs and the weights are very simple:

$$
  \frac{\partial z}{\partial w_{i}} = x_{i} \qquad
  \frac{\partial z}{\partial x_{i}} = w_{i}
$$

  + The derivative of the output with respect to the logit is simple if you express it in terms of the output:

$$
\begin{align}
  y &= \frac{1}{1 + e^{-z}} \\
  \frac{dy}{dz} &= y(1 - y)
\end{align}
$$

Derivation:
> <img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/3.101_logistic-neuron-derivative.png" alt="[Image] Derivation" style="width: 500px; margin: auto;"/>

**The Weights of a Logistic Unit**

Assuming that we have<br>
`-` $m$ data points<br>
`-` $p$ weights

<div style="background-color: #ffffc8; padding: 2px;">
$$
\frac{\partial E}{\partial w_{j}} = - \sum_{i=1}^{m} x_{j}^{(i)} y^{(i)} (1 - y^{(i)}) (t^{i} - y^{(i)}) \qquad \text{for} \ j = 1, 2, ..., p
$$
</div>

<br>

Derivation:<br>
> $$
\begin{align}
  \frac{\partial y}{\partial w_{j}} &= \frac{\partial z}{\partial w_{j}} \cdot \frac{dy}{dz} = x_{j} \cdot y(1 - y) \\
  \frac{\partial E}{\partial w_{j}} &= \sum_{i=1}^{m} \frac{\partial E^{(i)}}{\partial w_{j}} \\
  &= \sum_{i=1}^{m} \frac{\partial E^{(i)}}{\partial y^{(i)}} \cdot \frac{\partial y^{(i)}}{\partial w_{j}} \qquad \text{(Chain Rule)} \\
  &= \sum_{i=1}^{m} - (t^{(i)} - y^{(i)}) \cdot x_{j}^{(i)} y^{(i)}(1 - y^{(i)}) \\
  &= - \sum_{i=1}^{m} x_{j}^{(i)} y^{(i)} (1 - y^{(i)}) (t^{(i)} - y^{(i)})
\end{align}
$$

<br>

### d. The Backpropagation Algorithm
---

**Learning with Hidden Units (Again)**
  + NN without hidden units:
    - very limited in the input-output mappings they can model.
  + NN with a layer of hand-coded features (as in a perceptron):
    - pro: much more powerful
    - con: hard bit is designing the features
  + Goal: _automate the loop of designing features_ for a particular task and seeing how well they work.

**Learning by Perturbing Weights**
  + Randomly <span style="color:red;">perturb one weight</span> and see if it improves performance. If so, save the change.
    - a form of reinforcement learning
    - Pros:
      * an intuitive method
    - Cons:
      * very inefficient: We need to do multiple forward passes on a representative set of training cases just to change one weight. Backpropagation is much better.
      * Towards the end of learning, large weight perturbations will nearly always make things worse, because the weights need to have the right relative values.

  + Randomly <span style="color:red;">perturb all the weights in parallel</span> and correlate the performance gain with the weight changes
    - Not any better because we need lots of trials on each training case to “see” the effect of changing one weight through the noise created by all the changes to other weights.

  + A better idea: Randomly perturb the activities of the hidden units.
    - Once we know how we want a hidden activity to change on a given training case, we can compute how to change the weights.
    - There are fewer activities than weights, but backpropagation still wins by a factor of the number of neurons.

**The Idea Behind Backpropagation**
  + We don’t know what the hidden units ought to do, but we can compute how fast the error changes as we change a hidden activity.
    -  Instead of using desired activities to train the hidden units, use <span style="color:red;">error derivatives w.r.t. hidden activities</span>.
    - Each hidden activity can affect many output units and can therefore have many separate effects on the error. These effects must be combined.
  + We can compute error derivatives for all the hidden units efficiently at the same time.
    - Once we have the error derivatives for the hidden activities, its easy to get the error derivatives for the weights going into a hidden unit.

**Sketch of the Backpropagation Algorithm on a Single Case**
  + First convert the discrepancy between each output and its target value into an error derivative $\frac{\partial E}{\partial y_j}$.

$$
\begin{align}
  E &= \frac{1}{2} \sum_{j \in output} (t_{j} - y_{j})^{2} \\
  \frac{\partial E}{\partial y_j} &= - (t_j - y_j)
\end{align}
$$

  + Then compute error derivatives in each hidden layer $\frac{\partial E}{\partial y_j}$ from error derivatives in the layer above $\frac{\partial E}{\partial y_i}$.

  + Then use error derivatives w.r.t. activities to get error derivatives w.r.t. the incoming weights.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/3.6_backpropagation-single-case.png" alt="[Image] Backpropagation on a Single Case" style="width: 300px; margin: auto;"/>
<p style="text-align: center">Figure 3-6: Backpropagation on a Single Case</p>

**Backpropagating dE/dy**

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/3.7_backpropagating-dEdy.png" alt="[Image] Backpropagating dE/dy" style="width: 250px; margin: auto;"/>
<p style="text-align: center">Figure 3-7: Backpropagating dE/dy</p>

Assume<br>
`-` logistic neurons, we therefore have

$$
\frac{dy}{dz} = y(1 - y)
$$

`-` $y_{j}$ = output of neuron $j$ <br>
`-` $y_{i}$ = output of neuron $i$ <br>
`-` $z_{j}$ = sum of all the input to node $j$ <br>
`-` $w_{ij}$ = weight between node $i$ and node $j$

<div style="background-color: #ffffc8; padding: 2px;">
$$
\begin{align}
  \frac{\partial E}{\partial z_{j}} &= y_{j}(1 - y_{j}) \frac{\partial E}{\partial y_{j}} \\
  \frac{\partial E}{\partial y_{i}} &= \sum_{j} w_{ij} \frac{\partial E}{\partial z_{j}} \\
  \frac{\partial E}{\partial w_{ij}} &= y_{i} \frac{\partial E}{\partial z_{j}}
\end{align}
$$
</div>

<br>

Derivation: <br>
> $$
\begin{align}
  \frac{\partial E}{\partial z_{j}} &= \frac{d y_{j}}{d z_{j}} \cdot \frac{\partial E}{\partial y_j} \qquad &&\text{(chain rule)} \\
  &= y_{j} (1 - y_{j}) \cdot \frac{\partial E}{\partial y_j} &&\text{(node } j \text{ is a logistic neuron)} \\
  \frac{\partial E}{\partial y_{i}} &= \sum_{j} \frac{d z_{j}}{d y_{i}} \cdot \frac{\partial E}{\partial z_{j}} &&\text{(sum over all nodes on node } j \text{'s layer)} \\
  &= \sum_{j} w_{ij} \cdot \frac{\partial E}{\partial z_{j}} &&\text{(since } z_{j} = \sum_{k} w_{kj} y_{k} \text{)} \\
  \frac{\partial E}{\partial w_{ij}} &= \frac{\partial z_{j}}{\partial{w_{ij}}} \cdot \frac{\partial{E}}{\partial{z_{j}}} \\
  &= y_{i} \cdot \frac{\partial E}{\partial z_{j}} &&\text{(since } z_{j} = \sum_{k} w_{kj} y_{k} \text{)}
\end{align}
$$

<br>

### e. How to Use the Derivatives Computed by the Backpropagation Algorithm
---

**Converting Error Derivatives into a Learning Procedure**
  + The backpropagation algorithm is an <span style="color:red;">efficient</span> way of computing the error derivative dE/dw for every weight on a single training case.
  + To get a fully specified learning procedure, we still need to make a lot of other decisions about how to use these error derivatives:
    - <span style="color:blue;">Optimization issues</span>: How do we use the error derivatives on individual cases to discover a good set of weights? <span style="color:blue;">(lecture 6)</span>
    - <span style="color:blue;">Generalization issues</span>: How do we ensure that the learned weights work well for cases we did not see during training? <span style="color:blue;">(lecture 7)</span>
  + We now have a very brief overview of these two sets of issues.

**Optimization Issues in Using the Weight Derivatives**
  + How often to update the weights
    - **Online**: after each training case.
    - **Full batch**: after a full sweep through the training data.
    - **Mini-batch**: after a small sample of training cases.
  + How much to update (discussed further in lecture 6)
    - Use a fixed learning rate?
    - Adapt the global learning rate?
    - Adapt the learning rate on each connection separately?
    - Don’t use steepest descent?

**Overfitting: The Downside of Using Powerful Models**
  + The training data contains information about the regularities in the mapping from input to output. But it also contains two types of noise.
    - The target values may be unreliable (usually only a minor worry).
    - There is **sampling error**. There will be accidental regularities just because of the particular training cases that were chosen.
  + When we fit the model, it cannot tell which regularities are real and which are caused by sampling error.
    - So it fits both kinds of regularity.
    - If the model is very flexible it can model the sampling error really well. <span style="color:red;">This is a disaster</span>.

**A Simple Example of Overfitting**<br>
Skipped.

**Ways to Reduce Overfitting**
  + A large number of different methods have been developed.
    - Weight-decay
    - Weight-sharing
    - Early stopping
    - Model averaging
    - Bayesian fitting of neural nets
    - Dropout
    - Generative pre-training
  + Many of these methods will be described in <span style="color:blue;">lecture 7</span>.

<br>

### Reading
---
+ [Week 3 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/slides/Week3.pdf "Week 3 - The Perceptron learning procedure") <br>
+ Rumelhart, D. E., Hinton, G. E. & Williams, R. J. in _Parallel Distributed Processing: Explorations in the Microstructure of Cognition._ Vol. 1: _Foundations_ (eds Rumelhart, D. E. & McClelland, J. L.) 318−362 (MIT, Cambridge, 1986). [[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/Chap8_PDP86.pdf)]<br>

**More**
+ Demos on backpropagation algorithm:<br>
[http://home.agh.edu.pl/~vlsi/AI/backp_t_en/backprop.html](http://home.agh.edu.pl/~vlsi/AI/backp_t_en/backprop.html) <br>
[https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/](https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/)<br>

<br>
