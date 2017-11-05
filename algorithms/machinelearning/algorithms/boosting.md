---
layout: algorithm
title: Boosting
comments: true
mathjax: true
---

## {{page.title}}

Boosting is a machine learning ensemble meta-algorithm for primarily reducing bias, and also variance in supervised learning, and a family of machine learning algorithms which convert weak learners to strong ones.

<br>

### History
---
There are many boosting algorithms. The original ones, proposed by Robert Schapire (a recursive majority gate formulation) and Yoav Freund (boost by majority), were not adaptive and could not take full advantage of the weak learners. However, Schapire and Freund then developed AdaBoost, an adaptive boosting algorithm that won the prestigious Gödel Prize.

<br>

### Algorithms
---
#### 1. Boosting algorithm in general
While boosting is not algorithmically constrained, most boosting algorithms consist of iteratively learning weak classifiers with respect to a distribution and adding them to a final strong classifier. When they are added, they are typically weighted in some way that is usually related to the weak learners' accuracy. After a weak learner is added, the data are reweighted: examples that are misclassified gain weight and examples that are classified correctly lose weight (some boosting algorithms actually decrease the weight of repeatedly misclassified examples, e.g., boost by majority and BrownBoost). Thus, future weak learners focus more on the examples that previous weak learners misclassified.

<br>

#### 2. AdaBoost
**2.1 Description of Steps**

The core principle of AdaBoost is to fit a sequence of weak learners (i.e., models that are only slightly better than random guessing, such as small decision trees) on repeatedly modified versions of the data. The predictions from all of them are then combined through a weighted majority vote (or sum) to produce the final prediction. The data modifications at each so-called boosting iteration consist of applying weights $w_1, w_2, …, w_N$ to each of the training samples. Initially, those weights are all set to $w_i = 1/N$, so that the first step simply trains a weak learner on the original data. For each successive iteration, the sample weights are individually modified and the learning algorithm is reapplied to the reweighted data. At a given step, those training examples that were incorrectly predicted by the boosted model induced at the previous step have their weights increased, whereas the weights are decreased for those that were predicted correctly. As iterations proceed, examples that are difficult to predict receive ever-increasing influence. Each subsequent weak learner is thereby forced to concentrate on the examples that are missed by the previous ones in the sequence.

Reference:<br>
[http://scikit-learn.org/stable/modules/ensemble.html#adaboost](http://scikit-learn.org/stable/modules/ensemble.html#adaboost)

**2.2 Pseudocode**

Given training data $(x_{1}, y_{1}), ..., (x_{m}, y_{m})$<br>
$$y_{i} \in \{ -1, +1 \}$$, $x_{i} \in X$ is the object or instance, $y_{i}$ is the classification.

for $t = 1, ..., T$<br>
&nbsp;&nbsp;&nbsp;&nbsp;
create distribution $D_{t}$ on ${1, ..., m}$<br>
&nbsp;&nbsp;&nbsp;&nbsp;
select weak classifier with smallest error $\epsilon_{t}$ on $D_{t}$<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
$\epsilon_{t} = Pr_{D_{t}} \big[ h_{t}(x_{i}) \neq y_{i}\big]$<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
$$h_{t}: X \rightarrow \{ -1, +1 \}$$<br>
output single classifier $H_{final}(x)$

Reference:<br>
[http://math.mit.edu/~rothvoss/18.304.3PM/Presentations/1-Eric-Boosting304FinalRpdf.pdf](http://math.mit.edu/~rothvoss/18.304.3PM/Presentations/1-Eric-Boosting304FinalRpdf.pdf)

<br>

### Pros & Cons
---
#### 1. AdaBoost
**Pros**<br>
+ Fast
+ Simple and easy to program
+ No parameters to tune (except T)
+ No prior knowledge needed about weak learner
+ Provably effective given weak learning assumption
+ Versatile

**Cons**<br>
+ Weak classifiers too complex $\rightarrow$ overfitting
+ Weak classifiers too weak $\rightarrow$ low margins, also overfitting
+ From empirical evidence, AdaBoost is particularly vulnerable to uniform noise.

Reference:<br>
[http://math.mit.edu/~rothvoss/18.304.3PM/Presentations/1-Eric-Boosting304FinalRpdf.pdf](http://math.mit.edu/~rothvoss/18.304.3PM/Presentations/1-Eric-Boosting304FinalRpdf.pdf)



<br><br>
