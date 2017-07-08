---
layout: algorithm
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

My own derivation:

Assuming that there are<br>
(1) $m$ data points in the training set;<br>
(2) $p$ dimensions for each data point;
> $$
> \begin{align}
> E &= \frac{1}{2} \sum_{i=1}^{m} E^{(i)} = \frac{1}{2} \sum_{i=1}^{m} (t^{(i)} - y^{(i)})^{2} \\
> \frac{\partial E}{\partial w_{j}} &= \frac{1}{2} \sum_{i=1}^{m} \frac{\partial E^{(i)}}{\partial w_{j}} \qquad &&\text{for} \ j = 1, 2, ..., p \\
> &= \frac{1}{2} \sum_{i=1}^{m} \frac{\partial E^{(i)}}{\partial y^{(i)}} \cdot \frac{\partial y^{(i)}}{\partial w_{j}} &&\text{(chain rule)}\\
> &= \frac{1}{2} \sum_{i=1}^{m} 2 (t^{(i)} - y^{(i)}) (-1) \cdot x_{j}^{(i)} &&(\text{since} \ \frac{\partial y^{(i)}}{\partial w_{j}} = \frac{\partial \sum_{j=1}^{p} w_{j} x_{j}^{(i)}}{\partial w_{j}}) \\
> &= - \sum_{i=1}^{m} x_{j}^{(i)} \cdot (t^{(i)} - y^{(i)}) \\
> \Delta w_{j} &= - \epsilon \cdot \frac{\partial E}{\partial w_{j}} = \sum_{i=1}^{m} \epsilon \cdot x_{j}^{(i)} \cdot (t^{(i)} - y^{(i)}) &&\text{for} \ j = 1, 2, ..., p \\
> \end{align}
> $$

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

$$
\Delta w_{j} = \sum_{i=1}^{m} \epsilon \cdot x_{j}^{(i)} \cdot (t^{(i)} - y^{(i)}) \qquad \text{for} \ j = 1, 2, ..., p
$$

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



<br>

### Reading
---
+ [Week 3 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/Week3.pdf "Week 3 - The Perceptron learning procedure") <br>
+ Rumelhart, D. E., Hinton, G. E. & Williams, R. J. in _Parallel Distributed Processing: Explorations in the Microstructure of Cognition._ Vol. 1: _Foundations_ (eds Rumelhart, D. E. & McClelland, J. L.) 318−362 (MIT, Cambridge, 1986). [[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/Chap8_PDP86.pdf)]

<br>
