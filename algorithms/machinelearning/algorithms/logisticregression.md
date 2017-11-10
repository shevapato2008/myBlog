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
The goal of logistic regression is to model the probability of a random variable $Y$ being $0$ or $1$ given experimental data.

Consider a generalized linear model function (logistic function) parameterized by $\theta$.

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
Pr(y | x; \theta)
&=
\left\{ \begin{array}{rcl}
h_{\theta} (x) & \mbox{if} & y = 1\\
1 - h_{\theta} (x) & \mbox{if} & y = 0
\end{array}\right.\\
&= h_{\theta}(x)^{y} \Big( 1 - h_{\theta}(x) \Big)^{(1 - y)}
\end{split}
\end{equation}
$$

We take our likelihood function assuming that all the samples are independent.

$$
\begin{equation}
\begin{split}
L(\theta|X, Y)
&= Pr(Y|X; \theta)\\
&= \prod\limits_{i} Pr(y_{i}|x_{i}; \theta)\\
&= \prod\limits_{i} h_{\theta}(x_{i})^{y_{i}} \Big( 1 - h_{\theta}(x_{i}) \Big)^{(1 - y_{i})}
\end{split}
\end{equation}
$$

The goal is to maximize the likelihood function to get the optimal parameter vector $\theta$. It is equivalent to minimizing the negative log of the likelihood function show as below.

$$
\begin{equation}
\begin{split}
& \max\limits_{\theta} \quad L(\theta|X, Y)\\
\Leftrightarrow \quad & \max\limits_{\theta} \quad \log L(\theta|X, Y)\\
\Leftrightarrow \quad & \min\limits_{\theta} \quad - \log L(\theta|X, Y)
\end{split}
\end{equation}
$$

We can set it as the cost of a single $(x, y)$ pair.

$$
\begin{equation}
\begin{split}
Cost(h_{\theta} (x), y)
&= \left\{ \begin{array}{rcl}
   - \log (h_{\theta} (x)) & \mbox{if} & y = 1\\
   - \log (1 - h_{\theta} (x)) & \mbox{if} & y = 0
   \end{array}\right.\\
&= - \Big[ y \log (h_{\theta} (x)) + (1 - y) \log (1 - h_{\theta} (x)) \Big]
\end{split}
\end{equation}
$$

Note:<br>
(1) Convexity:<br>
For both $y = 0$ and $y = 1$ cases, the cost function is convex.

(2) Intuitive understanding:<br>
Take the $y = 1$ case as an example.<br>
+ $Cost = 0$ if $h_{\theta} (x) = 1$.<br>
This means prediction is correct. The penalty is $0$.
+ $Cost \rightarrow \infty$ as $h_{\theta} (x) \rightarrow 0$.<br>
This means that if $h_{\theta} (x) = 0$, we predict $Pr(y = 1|x; \theta) = 0$). But $y = 1$. We will penalize the learning algorithm by a very large cost.

<br>

The cost function $J(\theta)$ of logistic regression for all input output pairs $(x_{1}, y_{1}), ..., (x_{m}, y_{m})$ is:

$$
\begin{equation}
\begin{split}
J(\theta)
&= \frac{1}{m} \sum\limits_{i = 1}^{m} Cost(h_{\theta}(x_{i}), y_{i})\\
&= - \frac{1}{m} \sum\limits_{i = 1}^{m} \Big[ y_{i} \log (h_{\theta} (x_{i})) + (1 - y_{i}) \log (1 - h_{\theta} (x_{i})) \Big]
\end{split}
\end{equation}
$$

To fit parameters $\theta$:

$$
\begin{equation}
\begin{split}
\min\limits_{\theta} J(\theta)
\end{split}
\end{equation}
$$

However, there's no closed form solution for $\theta$. We need to use some optimization method like gradient descent or Newton's method to get $\theta$.

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

<br>

### Reference
---
+ [Logistic Regression (Wikipedia)](https://en.wikipedia.org/wiki/Logistic_regression)
+ [Logistic Regression (SciKit-Learn)](http://scikit-learn.org/stable/modules/linear_model.html#logistic-regression)
+ [Lecture Notes on Logistic Regression (Machine Learning by Andrew Ng)]({{site.baseurl}}/algorithms/machinelearning/course/ml_andrewng/slides/6.pdf)

<br><br>
