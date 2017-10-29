---
layout: algorithm
comments: true
mathjax: true
---

# Word Count

<br>

## Data
---
Download the `Book.txt` file from [here](https://raw.githubusercontent.com/shevapato2008/HadoopMapReduce_Python/master/5.%20Word%20Count/Book.txt") and put it in the same folder as python code.

The data `Book.txt` looks something like below.
```
Self-Employment: Building an Internet Business of One
Achieving Financial and Personal Freedom through a Lifestyle Technology Business
By Frank Kane
... ...
```

<br>

## Code & Analysis
---
The basic version:
```python
from mrjob.job import MRJob

class MRWordFrequencyCount(MRJob):

    def mapper(self, _, line):
        words = line.split()
        for word in words:
            word = unicode(word, "utf-8", errors = "ignore")
                # avoids issues in mrjob 5.0
            yield word.lower(), 1

    def reducer(self, key, values):
        yield key, sum(values)

if __name__ == '__main__':
    MRWordFrequencyCount.run()
```
The better version:
```python
from mrjob.job import MRJob
import re

WORD_REGEXP = re.compile(r"[\w']+")

class MRWordFrequencyCount(MRJob):

    def mapper(self, _, line):
        words = WORD_REGEXP.findall(line)
        for word in words:
            word = unicode(word, "utf-8", errors = "ignore")
                # avoids issues in mrjob 5.0
            yield word.lower(), 1

    def reducer(self, key, values):
        yield key, sum(values)

if __name__ == '__main__':
    MRWordFrequencyCount.run()
```
The sorted version:
```python
from mrjob.job import MRJob
# introduce step package to deal with chaining of mappers and reducers
from mrjob.step import MRStep
import re

WORD_REGEXP = re.compile(r"[\w']+")

class MRWordFrequencyCount(MRJob):

    def steps(self):
        return [
            MRStep(mapper = self.mapper_get_words,
                   reducer = self.reducer_count_words),
            MRStep(mapper = self.mapper_make_counts_key,
                   reducer = self.reducer_output_words)
        ]

    def mapper_get_words(self, _, line):
        words = WORD_REGEXP.findall(line)
        for word in words:
            word = unicode(word, "utf-8", errors="ignore")
                # avoids issues in mrjob 5.0
            yield word.lower(), 1

    def reducer_count_words(self, word, values):
        yield word, sum(values)

    def mapper_make_counts_key(self, word, count):
        yield '%04d'%int(count), word
            # group words by count and sort count

    def reducer_output_words(self, count, words):
        for word in words:
            # output one word for each line
            yield count, word

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
cd 5. Word Count
!python WordFrequency.py Book.txt > wordcount.txt
```
The result looks like the following.
```
"------------------------------------------------------------"	2
"---------------"	2
"--"	2
""	174
"#1"	1
"$1,000"	2
"$1,800"	1
"$10"	1
"$10,000"	8
"$100"	1
"$100,"	1
"$100,000"	3
"$1000"	1
... ...
```

The better version:

Execute the following command in the Python Console.
```shell
!python WordFrequencyBetter.py Book.txt > wcbetter.txt
```
The result looks like the following.
```
"___"	28
"0"	1
"000"	24
"05"	1
"07"	1
"1"	13
"10"	23
"100"	10
"1000"	1
... ...
```

The sorted version:

Execute the following command in the Python Console.
```shell
!python WordFrequencySorted.py Book.txt > wcsorted.txt
```
The result looks like the following.
```
"0001"	"0"
"0001"	"05"
"0001"	"07"
"0001"	"1000"
"0001"	"104"
"0001"	"1099"
"0001"	"1124"
"0001"	"12"
"0001"	"125"
"0001"	"13"
"0001"	"14"
"0001"	"15"
... ...
```

<br><br>
