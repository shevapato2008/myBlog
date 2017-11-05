---
layout: algorithm
title: Decision Tree
comments: true
mathjax: true
---

## {{page.title}}

Decision Trees (DTs) are a non-parametric supervised learning method used for classification and regression. The goal is to create a model that predicts the value of a target variable by learning simple decision rules inferred from the data features.

<br>

### Algorithms
---
#### 1. ID3
[ID3](https://en.wikipedia.org/wiki/ID3_algorithm "Wikipedia") (Iterative Dichotomiser 3) was developed in 1986 by Ross Quinlan. The algorithm creates a multiway tree, finding for each node (i.e. in a greedy manner) the categorical feature that will yield the largest information gain for categorical targets. Trees are grown to their maximum size and then a pruning step is usually applied to improve the ability of the tree to generalise to unseen data.

<br>

**1.1 Summary**

1. Calculate the entropy of every attribute using the data set $S$<br>
2. Split the set $S$ into subsets using the attribute for which the resulting entropy (after splitting) is minimum (or, equivalently, information gain is maximum)<br>
3. Make a decision tree node containing that attribute<br>
4. Recurse on subsets using remaining attributes.

<br>

**1.2 Pseudocode**
```
ID3 (Examples, Target_Attribute, Attributes)
    Create a root node for the tree
    If all examples are positive, Return the single-node tree Root with label = +.
    If all examples are negative, Return the single-node tree Root with label = -.
    If number of predicting attributes is empty, then Return the single node tree Root, with label = most common value of the target attribute in the examples.
    Otherwise Begin
        A ← The Attribute that best classifies examples.
        Decision Tree attribute for Root = A.
        For each possible value, vi, of A,
            Add a new tree branch below Root, corresponding to the test A = vi.
            Let Examples(vi) be the subset of examples that have the value vi for A
            If Examples(vi) is empty
                Then below this new branch add a leaf node with label = most common target value in the examples
            Else below this new branch add the subtree ID3 (Examples(vi), Target_Attribute, Attributes – {A})
    End
    Return Root
```

<br>

**1.3 Properties**

1. ID3 does not guarantee an optimal solution.<br>
It can get stuck in local optima. It uses a greedy approach by selecting the best attribute to split the dataset on each iteration. One improvement that can be made on the algorithm can be to use [backtracking](https://en.wikipedia.org/wiki/Backtracking "Wikipedia") during the search for the optimal decision tree.

2. ID3 can overfit to the training data.<br>
To avoid overfitting, smaller decision trees should be preferred over larger ones. This algorithm usually produces small trees, but it does not always produce the smallest possible tree.

3. ID3 is harder to use on continuous data.<br>
If the values of any given attribute is continuous, then there are many more places to split the data on this attribute, and searching for the best value to split by can be time consuming.

<br>

**1.4 ID3 Metrics**

(1) Entropy<br>
Entropy $H(S)$ is a measure of the amount of uncertainty in the (data) set $S$ (i.e. entropy characterizes the (data) set $S$.

$$H(S) = - \sum\limits_{x \in X} p(x) \log_{2} p(x)$$

where,
+ $S$ = The current (data) set for which entropy is being calculated (changes every iteration of the ID3 algorithm)
+ $X$ = Set of classes in $S$
+ $p(x)$ = The proportion of the number of elements in class $x$ to the number of elements in set $S$

When $H(S) = 0$, the set $S$ is perfectly classified (i.e. all elements in $S$ are of the same class).

(2) Information Gain<br>
Information gain $IG(A)$ is the measure of the difference in entropy from before to after the set $S$ is split on an attribute $A$. In other words, how much uncertainty in $S$ was reduced after splitting set $S$ on attribute $A$.

$$IG(A, S) = H(S) - \sum\limits_{t \in T} p(t)H(t)$$

where,
+ $H(S)$ = Entropy of set $S$
+ $T$ = The subsets created from splitting set $S$ by attribute $A$ such that $S = \bigcup\limits_{t \in T} t$
+ $p(t)$ = The proportion of the number of elements in $t$ to the number of elements in set $S$
+ $H(t)$ = Entropy of subset $t$

In ID3, information gain can be calculated (instead of entropy) for each remaining attribute. The attribute with the largest information gain is used to split the set $S$ on this iteration.

<br>

#### 2. C4.5 & C5.0
[C4.5](https://en.wikipedia.org/wiki/C4.5_algorithm) is the successor to ID3 and removed the restriction that features must be categorical by dynamically defining a discrete attribute (based on numerical variables) that partitions the continuous attribute value into a discrete set of intervals. C4.5 converts the trained trees (i.e. the output of the ID3 algorithm) into sets of if-then rules. These accuracy of each rule is then evaluated to determine the order in which they should be applied. Pruning is done by removing a rule’s precondition if the accuracy of the rule improves without it.

C5.0 is Quinlan’s latest version release under a proprietary license. It uses less memory and builds smaller rulesets than C4.5 while being more accurate.

Authors of the Weka machine learning software described the C4.5 algorithm as "a landmark decision tree program that is probably the machine learning workhorse most widely used in practice to date".

It became quite popular after ranking #1 in the Top 10 Algorithms in Data Mining pre-eminent paper published by Springer LNCS in 2008.

This algorithm has a few base cases.
1. All the samples in the list belong to the same class. When this happens, it simply creates a leaf node for the decision tree saying to choose that class.
2. None of the features provide any information gain. In this case, C4.5 creates a decision node higher up the tree using the expected value of the class.
3. Instance of previously-unseen class encountered. Again, C4.5 creates a decision node higher up the tree using the expected value.

<br>

**2.1 Pseudocode**
```
(1) Check for the above base cases.
(2) For each attribute a, find the normalized information gain ratio from splitting on a.
(3) Let a_best be the attribute with the highest normalized information gain.
(4) Create a decision node that splits on a_best.
(5) Recur on the sublists obtained by splitting on a_best, and add those nodes as children of node.
```
<br>

**2.2 Improvements in C4.5 from ID.3 algorithm**

1. Handling both continuous and discrete attributes<br>
In order to handle continuous attributes, C4.5 creates a threshold and then splits the list into those whose attribute value is above the threshold and those that are less than or equal to it.<br>
2. Handling training data with missing attribute values<br>
C4.5 allows attribute values to be marked as ? for missing. Missing attribute values are simply not used in gain and entropy calculations.<br>
3. Handling attributes with differing costs.<br>
4. Pruning trees after creation<br>
C4.5 goes back through the tree once it's been created and attempts to remove branches that do not help by replacing them with leaf nodes.

<br>

**2.3 Improvements in C5.0 from C4.5 algorithm [Questionable]**

1. Speed<br>
C5.0 is significantly faster than C4.5 (several orders of magnitude)
2. Memory usage<br>
C5.0 is more memory efficient than C4.5
3. Smaller decision trees<br>
C5.0 gets similar results to C4.5 with considerably smaller decision trees.
4. Support for boosting<br>
Boosting improves the trees and gives them more accuracy.
5. Weighting<br>
C5.0 allows you to weight different cases and misclassification types.
6. Winnowing<br>
A C5.0 option automatically winnows the attributes to remove those that may be unhelpful.

<br>

#### 3. CART (分类回归树)
[CART](https://en.wikipedia.org/wiki/Predictive_analytics#Classification_and_regression_trees_.28CART.29 "Wikipedia") (Classification and Regression Trees) is very similar to C4.5, but it differs in that it supports numerical target variables (regression) and does not compute rule sets. CART constructs binary trees using the feature and threshold that yield the largest information gain at each node. scikit-learn uses an optimized version of the CART algorithm.

<br>

**3.1 Decision Tree Types**

Decision trees used in data mining are of two main types:
1. **Classification tree** analysis is when the predicted outcome is the class to which the data belongs.
2. **Regression tree** analysis is when the predicted outcome can be considered a real number (e.g. the price of a house, or a patient's length of stay in a hospital).

The term **Classification And Regression Tree (CART)** analysis is an umbrella term used to refer to both of the above procedures, first introduced by Breiman et al. Trees used for regression and trees used for classification have some similarities - but also some differences, such as the procedure used to determine where to split.

Some techniques, often called **ensemble methods**, construct more than one decision tree:
1. [**Boosted trees**](https://en.wikipedia.org/wiki/Gradient_boosting#Gradient_tree_boosting "Wikipedia") Incrementally building an ensemble by training each new instance to emphasize the training instances previously mis-modeled. A typical example is [**AdaBoost**](https://en.wikipedia.org/wiki/AdaBoost "Wikipedia"). These can be used for regression-type and classification-type problems.
2. [**Bootstrap aggregated**](https://en.wikipedia.org/wiki/Bootstrap_aggregating "Wikipedia") (or bagged) decision trees, an early ensemble method, builds multiple decision trees by repeatedly resampling training data with replacement, and voting the trees for a consensus prediction.
  + A [**random forest**](https://en.wikipedia.org/wiki/Random_forest "Wikipedia") classifier is a specific type of bootstrap aggregating
3. Rotation forest - in which every decision tree is trained by first applying principal component analysis (PCA) on a random subset of the input features.

A special case of a decision tree is a [**decision list**](https://en.wikipedia.org/wiki/Decision_list "Wikipedia"), which is a one-sided decision tree, so that every internal node has exactly 1 leaf node and exactly 1 internal node as a child (except for the bottommost node, whose only child is a single leaf node). While less expressive, decision lists are arguably easier to understand than general decision trees due to their added sparsity, permit non-greedy learning methods and monotonic constraints to be imposed.

<br>

**3.2 Metrics**

(1) Gini Impurity (基尼不纯度)

Used by the CART (classification and regression tree) algorithm, Gini impurity is a measure of how often a randomly chosen element from the set would be incorrectly labeled if it was randomly labeled according to the distribution of labels in the subset. Gini impurity can be computed by summing the probability $p_{i}$ of an item with label $i$ being chosen times the probability $1 - p_{i}$ of a mistake in categorizing that item. It reaches its minimum (zero) when all cases in the node fall into a single target category.

To compute Gini impurity for a set of items with $J$ classes, suppose $$i \in \big\{ 1,2,...,J \big\}$$, and let $p_{i}$ be the fraction of items labeled with class $i$ in the set.

$$
\begin{equation}
\begin{split}
I_{G} (p) & = \sum\limits_{i = 1}^{J} p_{i}(1 - p_{i})
            = \sum\limits_{i = 1}^{J} (p_{i} - p_{i}^2)\\
          & = \sum\limits_{i = 1}^{J} p_{i} - \sum\limits_{i = 1}^{J} p_{i}^2
            = 1 - \sum\limits_{i = 1}^{J} p_{i}^2\\
          & = \sum\limits_{i \neq k} p_{i}p_{k}
\end{split}
\end{equation}
$$

(2) Information Gain (信息增益)

Used by the ID3, C4.5 and C5.0 tree-generation algorithms. Information gain is based on the concept of entropy from information theory.

Entropy is defined as below

$$
\begin{equation}
\begin{split}
H(T) = I_{E}(p_{1}, p_{2}, ..., p_{J}) = - \sum\limits_{i = 1}^{J} p_{i} \log_{2} p_{i}
\end{split}
\end{equation}
$$

where $p_{1}$, $p_{2}$,... are fractions that add up to 1 and represent the percentage of each class present in the child node that results from a split in the tree.

$$
\begin{equation}
\begin{split}
\text{Information Gain} &= \text{Entropy (parent)} - \text{Weighted Sum of Entropy (children)}\\
IG(T, a) &= H(T) - H(T|a)
\end{split}
\end{equation}
$$

(3) Variance Reduction (方差衰减/方差降低)

Introduced in CART, variance reduction is often employed in cases where the target variable is continuous (regression tree), meaning that use of many other metrics would first require discretization before being applied. The variance reduction of a node $N$ is defined as the total reduction of the variance of the target variable $x$ due to the split at this node:

$$
\begin{equation}
\begin{split}
I_{V}(N) =
&\frac{1}{|S|^{2}} \sum\limits_{i \in S} \sum\limits_{j \in S} \frac{1}{2} (x_{i} - x_{j})^2\\
& - \Bigg(
  \frac{1}{|S_{t}|^{2}} \sum\limits_{i \in S_{t}} \sum\limits_{j \in S_{t}} \frac{1}{2} (x_{i} - x_{j})^2
+ \frac{1}{|S_{f}|^{2}} \sum\limits_{i \in S_{f}} \sum\limits_{j \in S_{f}} \frac{1}{2} (x_{i} - x_{j})^2
  \Bigg)
\end{split}
\end{equation}
$$

where $S$, $S_{t}$, and $S_{f}$ are the set of presplit sample indices, set of sample indices for which the split test is true, and set of sample indices for which the split test is false, respectively. Each of the above summands are indeed variance estimates, though, written in a form without directly referring to the mean.

<br>

### Pros & Cons
---
#### 1. Pros
+ **Simple to understand and interpret (white box model)**<br>
Trees can also be displayed graphically in a way that is easy for non-experts to interpret. It uses a white box model. By contrast, in a black box model, the explanation for the results is typically difficult to understand, for example with an artificial neural network.
+ **Handle both numerical and categorical data**<br>
Other techniques are usually specialized in analyzing datasets that have only one type of variable.
+ **Requires little data preparation**<br>
Other techniques often require data normalization. Since trees can handle qualitative predictors, there is no need to create dummy variables.
+ **Non-statistical approach that makes no assumptions of the training data or prediction residuals**<br>
e.g., no distributional, independence, or constant variance assumptions
+ **Performs well with large datasets**<br>
Large amounts of data can be analysed using standard computing resources in reasonable time.
+ Possible to validate a model using statistical tests<br>
That makes it possible to account for the reliability of the model.

<br>

#### 2. Cons
+ **Non-robustness**<br>
A small change in the training data can result in a big change in the tree, and thus a big change in final predictions.
+ **Learning an optimal decision tree is know to be NP-complete**<br>
Consequently, practical decision-tree learning algorithms are based on heuristics such as the greedy algorithm where locally-optimal decisions are made at each node. Such algorithms cannot guarantee to return the globally-optimal decision tree. To reduce the greedy effect of local-optimality some methods such as the dual information distance (DID) tree were proposed.
+ **Overfitting**<br>
Decision-tree learners can create over-complex trees that do not generalize well from the training data. Mechanisms such as pruning are necessary to avoid this problem.
+ **For data including categorical variables with different numbers of levels, information gain in decision trees is biased in favor of those attributes with more levels.**<br>
However, the issue of biased predictor selection is avoided by the Conditional Inference approach.

<br>

### Interview Questions
---
#### 1. [[stackoverflow] Different decision tree algorithms with comparison of complexity or performance](https://stackoverflow.com/questions/9979461/different-decision-tree-algorithms-with-comparison-of-complexity-or-performance)
+ **ID3**<br>
ID3, or Iternative Dichotomizer, was the first of three Decision Tree implementations developed by Ross Quinlan (Quinlan, J. R. 1986. Induction of Decision Trees. Mach. Learn. 1, 1 (Mar. 1986), 81-106.)

+ **C4.5**<br>
C4.5, Quinlan's next iteration. The new features (versus ID3) are:
  1. accepts both continuous and discrete features;
  2. handles incomplete data points;
  3. solves over-fitting problem by (very clever) bottom-up technique usually known as "pruning";
  4. different weights can be applied to the features that comprise the training data. Of these, the first three are very important--and i would suggest that any DT implementation you choose have all three. The fourth (differential weighting) is much less important.

+ **C5.0**<br>
C5.0, the most recent Quinlan iteration. This implementation is covered by patent and probably as a result, is rarely implemented (outside of commercial software packages). I have never coded a C5.0 implementation myself (I have never even seen the source code) so i can't offer an informed comparison of C5.0 versus C4.5. I have always been skeptical about the improvements claimed by its inventor (Ross Quinlan)--for instance, he claims it is "several orders of magnitude" faster than C4.5. Other claims are similarly broad ("significantly more memory efficient") and so forth. I'll just point you to studies which report the result of comparison of the two techniques and you can decide for yourself.

+ **CART**<br>
CART, or Classification And Regression Trees is often used as a generic acronym for the term Decision Tree, though it apparently has a more specific meaning. In sum, the CART implementation is very similar to C4.5; the one notable difference is that CART constructs the tree based on a numerical splitting criterion recursively applied to the data, whereas C4.5 includes the intermediate step of constructing `rule sets`.



<br><br>
