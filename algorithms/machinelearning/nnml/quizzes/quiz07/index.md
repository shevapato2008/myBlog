---
layout: algorithm
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Quiz 07

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/3.1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/3.2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>

**Code**<br>
```python
import numpy as np

Wxh = 0.5
Whh = -1.0
Why = -0.7
h_bias = -1.0
y_bias = 0.0

x0 = 9
x1 = 4
x2 = -2

def logit(z):
    return 1 / (1 + np.exp(-z))

z0 = Wxh * x0 + h_bias                  # z0 = 3.5
h0 = logit(z0)                          # h0 = 0.97068776924864364
z1 = Wxh * x1 + Whh * h0 + h_bias       # z1 = 0.02931223075135625
h1 = logit(z1)                          # h1 = 0.50732753303979039
y1 = Why * h1 + y_bias                  # y1 = -0.35512927312785325
```

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/4.1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/4.2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/4.3.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>


**Code**<br>
```python
import numpy as np

# initialize values
Wxh = -0.1
Whh = 0.5
Why = 0.25
h_bias = 0.4
y_bias = 0.0

x0 = 18
x1 = 9
x2 = -8

h0 = 0.2
h1 = 0.4
h2 = 0.8

y0 = 0.05
y1 = 0.1
y2 = 0.2

t0 = 0.1
t1 = -0.1
t2 = -0.2

-(t1 - y1) * Why * h1 * (1 - h1) - (t2 - y2) * Why * h2 * (1 - h2) * Whh * h1 * (1 - h1)
# 0.01392
```

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/5.1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/5.2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/6.1.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/6.2.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/quizzes/quiz07/6.3.png" alt="[Image] quiz image" style="width: 800px; margin: auto;"/>

<br><br>
