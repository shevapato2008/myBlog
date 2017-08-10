---
layout: nnml
title: Neural Networks for Machine Learning (Geoffrey Hinton, University of Toronto)
comments: true
mathjax: true
---

## Assignment 2

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/1.1.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/1.2.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/2.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>

Solution for Question $2$ & $3$:

After $10$ Epochs

|Learning Rate|Cross Entropies|
|:---:|---:|
|$0.0001$|Training Set = $4.384$<br>Validation Set = $4.385$<br>Test Set = $4.392$|
|$0.1$|Training Set = $2.536$<br>Validation Set = $2.609$<br>Test Set = $2.618$|

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/3.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/4.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/5.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>

Solution:

After $1$ Epoch

|Learning Rate|Training Set Cross Entropy|
|:---:|:---:|
|$0.001$|$4.432$|
|$0.1$|$3.956$|
|$10$|$4.705$|

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/6.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>

Solution:

After $10$ Epochs

|Learning Rate|Training Set Cross Entropy|
|:---:|:---:|
|$0.001$|$4.378$|
|$0.1$|$2.535$|
|$10$|$4.668$|

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/7.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>

Solution for Question $7$ & $8$:

After $10$ Epochs

|Model|# dim embedding|# dim hidden|Cross Entropies|
|:---:|:---:|:---:|---:|
|A|$5$|$100$|Training Set = $2.807$<br>Validation Set = $2.8275$<br>Test Set = $2.833$|
|B|$50$|$10$|Training Set = $3.013$<br>Validation Set = $3.029$<br>Test Set = $3.024$|
|C|$50$|$200$|Training Set = $2.537$<br>Validation Set = $2.601$<br>Test Set = $2.615$|
|D|$100$|$5$|Training Set = $3.223$<br>Validation Set = $3.233$<br>Test Set = $3.229$|

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/8.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/9.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>

Solution:

After $5$ Epochs

|Model|Momentum|Training Set Cross Entropy|
|:---:|:---:|:---:|
|A|$0.0$|$4.002$|
|B|$0.5$|$3.324$|
|C|$0.9$|$2.715$|

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/10.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>

Solution:

```matlab
>> model = train(10)
>> display_nearest_words('day', model, 10)
```

<br>

<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/11.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/12.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>
<img src="{{site.baseurl}}/algorithms/machinelearning/nnml/assignments/Assignment2/questions/13.png" alt="[Image] assignment image" style="width: 800px; margin: auto;"/>

<br><br>
