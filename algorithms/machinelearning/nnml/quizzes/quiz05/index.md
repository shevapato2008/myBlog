---
layout: nnml
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## In-Class Questions

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/in-class-q1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/in-class-q2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>

<br>

## Quiz 05

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/1.1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/1.2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/2.1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/2.2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/2.3.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/2.4.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>

`python`

```python
import numpy as np

X = np.array([(0, 1, 1, 1, 0),
              (0, 0, 0, 1, 0),
              (0, 1, 1, 1, 0),
              (0, 0, 0, 1, 0),
              (0, 1, 1, 1, 0)])

h = np.array([(1, 1, 1, 0),
              (0, 0, 1, 0),
              (1, 1, 1, 0),
              (0, 0, 1, 0)])

def logit(z):
    return 1 / (1 + np.exp(-z))

y1 = logit(np.sum(np.multiply(X[0:4, 0:4], h)))
y2 = logit(np.sum(np.multiply(X[0:4, 1:5], h)))
y3 = logit(np.sum(np.multiply(X[1:5, 0:4], h)))
y4 = logit(np.sum(np.multiply(X[1:5, 1:5], h)))
```

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/3.1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/3.2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/3.3.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/4.1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/4.2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/4.3.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/5.1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/5.2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/5.3.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/6.1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/6.2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/6.3.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz05/6.4.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>

<br><br>
