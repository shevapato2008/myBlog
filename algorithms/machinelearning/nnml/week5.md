---
layout: algorithm
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Week 5 - Object Recognition with Neural Nets

### a. Things that Make it Hard to Recognize Objects
---
**Things that Make it Hard to Recognize Objects**
  + <span style="color:blue;">Segmentation</span>: Real scenes are cluttered with other objects:
    - It's hard to tell which pieces go together as parts of the same object.
    - Parts of an object can be hidden behind other objects.
  + <span style="color:blue;">Lighting</span>: The intensities of the pixels are determined as much by the lighting as by the objects.
  + <span style="color:blue;">Deformation</span>:
    - e.g. a hand-­‐wriHen 2 can have a large loop or just a cusp.
  + <span style="color:blue;">Affordances</span>: Object classes are often defined by how they are used.
    - e.g. Chairs are things designed for sitting on so they have a wide variety of physical shapes.
  + <span style="color:blue;">Viewpoint</span>: Changes in viewpoint cause changes in images that standard learning methods cannot cope with.
    - Information hops between input dimensions (i.e. pixels)

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.1_diff-viewpoint.png" alt="[Image] Changes in Viewpoint" style="width: 450px; margin: auto;"/>
<p style="text-align: center">Figure 5-1: Changes in Viewpoint</p>

<br>

### b. Ways to Achieve Viewpoint Invariance
---
**Some Ways to Achieve Viewpoint Invariance**
  + We are so good at viewpoint invariance that it is hard to appreciate how difficult it is.
    - one of the main difficulties in making computers perceive
    - we still don't have generally accepted solutions
  + There are several different approaches:
    - use redundant invariant features
    - put a box around the object and use normalized pixels
    - <span style="color:blue;">lecture 5c</span>: use replicated features with pooling. This is called "**Convolutional Neural Nets**"
    - use a hierarchy of parts that have explicit poses relative to the camera

<br>

**The Invariant Feature Approach**
  + Extract a large, redundant set of features that are invariant under transformations
    - e.g. pair of roughly parallel lines with a red dot between them.
    - This is what baby herring gulls use to know where to peck for food.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.2_red-dot.png" alt="[Image] Parallel lines and a red dot" style="width: 100px; margin: auto;"/>
<p style="text-align: center">Figure 5-2: Parallel Lines and a Red Dot</p>

  + Enough invariant features => assemble them into an object
    - do not need to represent the relationships between features, because they are captured by other features
  + For recognition, must <span style="color:blue;">avoid forming features from parts of different objects</span>.

<br>

**The Judicious Normalization Approach**
  + Put a box around the object and use it as a coordinate frame for a set of normalized pixels.
    - solves dimension-hopping problem
    - the box can provide <span style="color:blue;">invariance</span> to many degrees of freedom: <span style="color:blue;">translation, rotation, scale, shear, stretch ...</span>
  + But <span style="color:red;">choosing the box is difficult</span> because of:
    - segmentation erros
    - occlusions
    - unusual orientations
  + Need to recognize the shape to get the box right!

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.3_rotated-R.png" alt="[Image] Rotated Letter R" style="width: 100px; margin: auto;"/>
<p style="text-align: center">Figure 5-3: Rotated Letter R</p>

<br>

**The Brute Force Normalization Approach**
  + When training the recognizer, use well-segmented, upright images to fit the correct box.
  + At test time <span style="color:blue;">try all possible boxes in a range of positions and scales</span>.
    - widely used for detecting upright things like faces and house numbers in unsegmented images
    - much more efficient if the recognizer can cope with some variation in position and scale so that we can use a coarse grid when trying all possible boxes

<br>

### c. Convolutional Neural Networks for Hand-written Digit Recognition
---

**The Replicated Feature Approach (Currently the Dominant Approach for NNs)**
  + Use many different copies of the same feature detector with different positions.
    - Could also replicate across scale and orientation (tricky and expensive)
    - Replication greatly reduces the number of free parameters to be learned.
  + Use several different feature types, each with its own map of replicated detectors.
    - Allows each patch of image to be represented in several ways.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.4_replicated-features.png" alt="[Image] Replicated Features" style="width: 200px; margin: auto;"/>
<p style="text-align: center">Figure 5-4: Replicated Features</p>

<br>

**Backpropagation with weight constraints**
  + easy to modify Backpropagation algorithm to incorporate linear constraints between the weights
  + compute the gradients as usual => modify the gradients to satisfy the constraints

<div style="background-color: #ffffc8;">
$$
\begin{align}
  &\text{To constrain:} \qquad && \ \ \ w_{1} = w_{2} \\
  &\text{We need:} \qquad && \Delta w_{1} = \Delta w_{2} \\
  &\text{Compute:} \qquad && \frac{\partial E}{\partial w_{1}} \ \text{and} \ \frac{\partial E}{\partial w_{2}} \\
  &\text{Use} \ \frac{\partial E}{\partial w_{1}} + \frac{\partial E}{\partial w_{2}} \ \text{for} \ w_{1} \ \text{and} \ w_{2}
\end{align}
$$
</div>

<br>

**What does Replicating the Feature Detectors Achieve?**
  + <span style="color:blue;">Equivariant Activities</span>: Replicated features do <span style="color:red;">NOT</span> make the neural activities invariant to translation. The activities are equivariant.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.5_translated-representation.png" alt="[Image] Translated Representation" style="width: 600px; margin: auto;"/>
<p style="text-align: center">Figure 5-5: Translated Representation</p>

  + <span style="color:blue;">Invariant knowledge</span>: If a feature is useful in SOME locations during TRAINING, detectors for that feature will be available in ALL locations during TESTING.

<br>

**Pooling the Outputs of Replicated Feature Detectors**
  + Get a small amount of translational invariance at each level by averaging four neighboring replicated detectors to give a single output to the next level.
    - This <span style="color:blue;">reduces the number of inputs to the next layer of feature extraction</span>, thus allowing us to have many more different feature maps.
    - Taking the maximum of the four works slightly better.
  + <span style="color:red;">Problem</span>: After several levels of pooling, we have <span style="color:red;">lost information about the precise positions</span> of things.
    - This makes it impossible to use the precise spatial relationships between high-level parts for recognition.

<br>

**Le Net**
  + Yann LeCun and his collaborators developed a really good recognizer for handwritten digits by using backpropagation in a feed-forward net with:
    - many hidden layers
    - many maps of replicated units in each layer
    - pooling of the outputs of nearby replicated units
    - a wide net that can cope with several characters at once even if they overlap
    - a clever way of training a complete system, not just a recognizer
  + This net was used for reading ~10% of the checks in North America.
  + Look the impressive demos of LENET at [http://yann.lecun.com](http://yann.lecun.com).

<br>

**The	Architecture of LeNet5**

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.6_LeNet5-architecture.png" alt="[Image] The Architecture of LeNet5" style="width: 800px; margin: auto;"/>
<p style="text-align: center">Figure 5-6: The Architecture of LeNet5</p>

<br>

**The 82 Errors Made by LeNet5**
  + Notice that most of the errors are cases that people find quite easy.
  + The human error rate is probably 20 to 30 errors but nobody has had the patience to measure it.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.7_82-errors-lenet5.png" alt="[Image] 82 Errors Made by LeNet5" style="width: 800px; margin: auto;"/>
<p style="text-align: center">Figure 5-7: 82 Errors Made by LeNet5</p>

<br>

**Priors and Prejudice**
  + put <span style="color:blue;">prior knowledge</span> about the task into the network by designing appropriate:
    - connectivity
    - weight constraints
    - neuron activation functions
  + less intuitive than hand-designing the features
  + alternatively, use our prior knowledge to create a lot more training data
    - may require a lot of work (Hofman & Tresp, 1993)
    - make learning take much longer
  + allows optimization to discover clever ways of using the multi-layer network
    - we may never fully understand how it does it

<br>

**The Brute Force Approach**
  + LeNet uses knowledge about the invariances to design:
    - local connectivity
    - weight-sharing
    - pooling
  + achieves about 80 errors
    - this can be reduced to ~40 errors using many different transformations of the input and other tricks (Ranzato 2008)
  + Ciresan et. al. (2010) inject knowledge of invariances by creating a huge amount of carefully designed extra training data to achieve ~35 errors:
    - for each training image => produce <span style="color:blue;">new training examples</span> by applying different <span style="color:blue;">transformations</span> => <span style="color:blue;">a large, deep, dumb net</span> on a GPU without much overfitting

    - top printed digit: the right answer
    - bottom two printed: network's best two guesses
    - right answer is <span style="color:blue;">almost always in the top 2 guesses</span>
    - with model averaging => ~25 errors

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.8_ciresan.png" alt="[Image] Errors Made by the Ciresan et. al. Net" style="width: 400px; margin: auto;"/>
<p style="text-align: center">Figure 5-8: Errors Made by the Ciresan et. al. Net</p>

<br>

**How to Detect a Significant Drop in the Error Rate**
  + Is 30 errors 10,000	test cases significantly better than 40 errors?
    - <span style="color:blue;">all depends on the particular errors</span>
    - <span style="color:blue;">McNemar test</span> uses the particular errors and can be much more powerful than a test that just uses the number of errors

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.9_mcnemar-test.png" alt="[Image] McNemar Test" style="width: 600px; margin: auto;"/>
<p style="text-align: center">Figure 5-9: McNemar Test</p>

<br>

### d. Convolutional Neural Networks for Object Recognition
---

**From Hand-Written Digits to 3-D Objects**
  + Recognizing real objects in <span style="color:red;">color photographs</span> downloaded from the web is much <span style="color:red;">more complicated</span> than recognizing hand-written digits:
    - hundred times as many classes ($1000$ vs. $10$)
    - hundred times as many pixels ($256 \times 256$ color vs. $28 \times 28$ gray)
    - $2$-dim image of $3$-dim scene
    - cluttered scenes requiring segmentation
    - multiple objects in each image
  + will the same type of convolutional nn work?

<br>

**The ILSVRC-2012 Competition on ImageNet**
  + $1.2$ million high resolution training images
  + <span style="color:blue;">classification task</span>:
    - get the "correct" class in your top 5 bets
  + <span style="color:blue;">localization task</span>:
    - for each bet, put a box around the object
    - box must have $>=50 \%$ overlap with the correct box

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.10_examples-from-test-set.png" alt="[Image] Examples from the Test Set (with Network's Guesses)" style="width: 600px; margin: auto;"/>
<p style="text-align: center">Figure 5-10: Examples from the Test Set (with Network's Guesses)</p>

<br>

**A Neural Network for ImageNet**
  + Alex Krizhevsky (NIPS 2012) developed a very deep convolutional neural net of the type pioneered by Yann LeCun. Its architecture is:
    - 7 hidden layers (not counting some max pooling layers)
    - early layers were convolutional
    - last 2 layers were globally connected
  + activation functions:
    - <span style="color:blue;">rectified linear units</span> in every hidden layer. <span style="color:blue;">faster and more expressive than logistic units</span>.
    - competitive normalization to suppress hidden activities when nearby units have stronger activities

<br>

**Tricks that Significantly Improve Generalization**
  + train on random $224 \times 224$ patches from the $256 \times 256$ images to get more data. Also use left-right reflections of the images.
  + at test time, combine the opinions from $10$ different patches:  
    - $4$ &nbsp; $224 \times 224$ corner patches
    - $1$ &nbsp; central $224 \times 224$ patch
    - $5$ &nbsp; reflections
  + use "**dropout**" to regularize the weights in the globally connected layers (which contain most of the parameters)
    - <span style="color:blue;">**dropout** means that half of the hidden units in a layer are randomly removed for each training example.</span>
    - this stops hidden units from relying too much on other hidden units.

<br>

**Find Roads in High-Resolution Images**
  + Vlad Mnih (ICML 2012) used a <span style="color:blue;">non-convolutional net with local fields</span> and multiple layers of rectified linear units to find roads in cluttered aerial images.
    - it takes a large image patch and predicts a binary road label for the central $16 \times 16$ pixels.
    - there is lots of labeled training data available for this task.
  + The task is <span style="color:red;">hard</span> because:
    - occlusion by buildings, trees, and cars
    - shadows, lighting changes
    - minor viewpoint changes
  + The <span style="color:red;">worst</span> problems are <span style="color:red;">incorrect labels</span>:
    - badly registered maps
    - arbitrary decisions about what counts as a road
  + <span style="color:blue;">Big NNs trained on big image patches</span> with <span style="color:blue;">millions of examples</span> are the only hope.

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/image/5.11_Vlad-Mnih.png" alt="[Image] Vlad Mnih's (ICML 2012) Non-Convolutional Net with Local Fields on Finding Roads" style="width: 800px; margin: auto;"/>
<p style="text-align: center">Figure 5-11: Vlad Mnih's (ICML 2012) Non-Convolutional Net with Local Fields on Finding Roads</p>

<br>

### Reading
---
+ [Week 5 Slides]({{site.baseurl}}/algorithms/machinelearning/nnml/slides/Week5.pdf "Week 5 - Object Recognition with Neural Nets") <br>

**More**
+ Alex Krizhevsky, Ilya Sutskever, Geoffrey E. Hinton: ImageNet Classification with Deep Convolutional Neural Networks. _NIPS_ 2012: 1106-1114 [[pdf]({{site.baseurl}}/algorithms/machinelearning/nnml/supplement/ImageNet Classification with Deep Convolutional Neural Networks.pdf)]<br>

<br><br>
