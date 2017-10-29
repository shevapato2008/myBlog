---
layout: algorithm
comments: true
mathjax: true
---

# Rating Counter

<br>

## Data
---
Download the `ml-100k.zip` file from [http://grouplens.org/datasets/movielens/](http://grouplens.org/datasets/movielens/).<br>
Unzip it and put it in the same folder as python code.

The data `u.data` under `ml-100k/` folder looks something like below.
```
196	242	3	881250949
186	302	3	891717742
22	377	1	878887116
244	51	2	880606923
166	346	1	886397596
298	474	4	884182806
115	265	2	881171488
253	465	5	891628467
... ...
```

<br>

## Code & Analysis
---
```python
from mrjob.job import MRJob

class MRRatingCounter(MRJob):
    def mapper(self, key, line):
        (userID, movieID, rating, timestamp) = line.split('\t')
        yield rating, 1
        # key/value pair created by mapper
        # mapper will also sort and group the key/value pair

    def reducer(self, rating, occurences):
        yield rating, sum(occurences)

if __name__ == '__main__':
    MRRatingCounter.run()
```

<br>

## Run the Code
---
Execute the following command in the Python Console.
```shell
!python RatingCounter.py ml-100k/u.data
```

<br><br>
