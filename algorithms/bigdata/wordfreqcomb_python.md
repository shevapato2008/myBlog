---
layout: algorithm
comments: true
mathjax: true
---

# Word Frequency with Combiners

<br>

## Data
---
Download the `Book.txt` file from [here](https://raw.githubusercontent.com/shevapato2008/HadoopMapReduce_Python/master/7.%20Word%20Frequency%20With%20Combiners/Book.txt "Book.txt") and put it in the same folder as python code.

The data `Book.txt` looks something like below.
```
Self-Employment: Building an Internet Business of One
Achieving Financial and Personal Freedom through a Lifestyle Technology Business
... ...
```

<br>

## Code & Analysis
---
```python
from mrjob.job import MRJob
from mrjob.step import MRStep

class MRWordFrequencyCount(MRJob):

    def mapper(self, _, line):
        words = line.split()
        for word in words:
            word = unicode(word, "utf-8", errors = "ignore")      # avoids issues in mrjob 5.0
            yield word.lower(), 1

    def combiner(self, key, values):    # combiner and reducer are only allowed to differ in the output
        yield key, sum(values)

    def reducer(self, key, values):
        yield key, sum(values)

if __name__ == '__main__':
    MRWordFrequencyCount.run()
```

<br>

## Run the Code
---
The basic version:

Execute the following command in the Python Console.
```shell
import os
os.chdir("..")
cd 7. Word Frequency With Combiners
!python WordFrequencyWithCombiner.py Book.txt > wccombiner.txt
```
The result looks like the following.
```
"------------------------------------------------------------"	2
"---------------"	2
"--"	2
"#1"	1
"$1,000"	2
"$1,800"	1
"$10"	1
"$10,000"	8
"$100" 1
... ...
```

<br><br>
