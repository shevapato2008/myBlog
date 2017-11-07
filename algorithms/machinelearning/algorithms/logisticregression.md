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
The goal of logistic regression is to model the probability of a random variable $Y$ being 0 or 1 given experimental data.

Consider a generalized linear model function (logistic function) parameterized by $\theta$,

$$
\begin{equation}
\begin{split}
h_{\theta}(x) = \frac{1}{1 + e^{- \theta^{T} x}}
\end{split}
\end{equation}
$$

This can be considered as a probability of $y = 1$ given $x$ and $\theta$, i.e.

$$
\begin{equation}
\begin{split}
h_{\theta}(x) = Pr(y = 1 | x; \theta)
\end{split}
\end{equation}
$$

In this line, we can model the probability that $y$ is $0$ or $1$ with Bernoulli distribution.

$$
\begin{equation}
\begin{split}
Pr(y | x; \theta) = h_{\theta}(x)^{y}(1 - h_{\theta}(x))^{(1-y)}
\end{split}
\end{equation}
$$


<br>

#### Multiple Classification

Reference:<br>
[[CSDN] 分类问题之逻辑回归](http://blog.csdn.net/xiu_star/article/details/52563619)

<br>

### Pros & Cons
---
#### Pros
+ Input variables can be of any form: numerical or categorical
+ Easy to compute<br>
linear combination of parameters $\theta$ and input $x$, i.e. $\theta^{T} x$, has low computational complexity
+ Easy to interpret<br>
from a probability point of view

#### Cons
+ Fit for binary prediction
+ It is a generalized linear model. Cannot solve non-linear problems.


Reference:<br>
[[Quora] What are the pros and cons of using logistic regression with one binary outcome and several binary predictors?](https://www.quora.com/What-are-the-pros-and-cons-of-using-logistic-regression-with-one-binary-outcome-and-several-binary-predictors)

<br><br>
