---
layout: algorithm
title: Logistic Regression
comments: true
mathjax: true
---

## {{page.title}}

In statistics, logistic regression, or logit regression, or logit model is a regression model where the dependent variable (DV) is categorical. This article covers the case of a binary dependent variable—that is, where the output can take only two values, "0" and "1", which represent outcomes such as pass/fail, win/lose, alive/dead or healthy/sick. Cases where the dependent variable has more than two outcome categories may be analyzed in multinomial logistic regression, or, if the multiple categories are ordered, in ordinal logistic regression.

<br>

### History
---
Logistic regression was developed by statistician David Cox in 1958. The binary logistic model is used to estimate the probability of a binary response based on one or more predictor (or independent) variables (features). It allows one to say that the presence of a risk factor increases the odds of a given outcome by a specific factor.

<br>

### Algorithms
---
#### Binary Classification

<br>

#### Multiple Classification

Reference:<br>
[[CSDN] 分类问题之逻辑回归](http://blog.csdn.net/xiu_star/article/details/52563619)

<br>

### Pros & Cons
---
#### Pros
+ Input variables can be any form: numerical or categorical
+ Easy to compute<br>
linear combination of parameters $\beta$ and input X, i.e. $X^{T}\beta$, has low computational complexity
+ Easy to interpret<br>
from a probability point of view

#### Cons
+ Fit for binary prediction
+ It is a generalized linear model. Cannot solve non-linear problems.


Reference:<br>
[[Quora] What are the pros and cons of using logistic regression with one binary outcome and several binary predictors?](https://www.quora.com/What-are-the-pros-and-cons-of-using-logistic-regression-with-one-binary-outcome-and-several-binary-predictors)

<br><br>
