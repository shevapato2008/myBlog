---
layout: algorithm
title: Bootstrap Aggregating (Bagging)
comments: true
mathjax: true
---

## {{page.title}}

In ensemble algorithms, `B`ootstrap `Agg`regat`ing` (bagging) methods form a class of algorithms which build several instances of a black-box estimator on random subsets of the original training set and then aggregate their individual predictions to form a final prediction. These methods are used as a way to <span style="background-color:yellow;">reduce the variance</span> of a base estimator (e.g., a decision tree), by introducing randomization into its construction procedure and then making an ensemble out of it. In many cases, bagging methods constitute a very simple way to improve with respect to a single model, without making it necessary to adapt the underlying base algorithm. As they provide a way to <span style="background-color:yellow;">reduce overfitting</span>, bagging methods work best with strong and complex models (e.g., fully developed decision trees), in contrast with boosting methods which usually work best with weak models (e.g., shallow decision trees).

<br>

### History
---
Bagging (Bootstrap aggregating) was proposed by Leo Breiman in 1994 to improve classification by combining classifications of randomly generated training sets. See Breiman, 1994. Technical Report No. 421.

<br>

### Algorithms
---
#### Bagging algorithm in general
1. Bootstrap (自助抽样法)<br>
Given a standard training set $D$ of size $n$, bagging generates $m$ new training sets $D_{i}$, each of size $n′$, by sampling from $D$ uniformly and with replacement.
2. Aggregating<br>
The $m$ models are fitted using the above $m$ bootstrap samples and combined by averaging the output (for regression) or voting (for classification).

<br>

#### Random Forest
1. Bootstrap as above
2. Special tree learning algorithm<br>
  + Feature Bagging: selects, at each candidate split in the learning process, a random subset of the features.

== Note ==<br>
The reason for feature bagging this is the correlation of the trees in an ordinary bootstrap sample: if one or a few features are very strong predictors for the response variable (target output), these features will be selected in many of the B trees, causing them to become correlated. An analysis of how bagging and random subspace projection contribute to accuracy gains under different conditions is given by Ho.

Reference:<br>
Ho, Tin Kam (2002). "[A Data Complexity Analysis of Comparative Advantages of Decision Forest Constructors](http://ect.bell-labs.com/who/tkh/publications/papers/compare.pdf)". Pattern Analysis and Applications: 102–112.


<br><br>
