---
layout: algorithm
comments: true
mathjax: true
---

# Most Popular Movie

<br>

## Data
---
Download the `ml-100k` file from [here](https://github.com/shevapato2008/HadoopMapReduce_Python/tree/master/8.%20Most%20Popular%20Movie/ml-100k "ml-100k") and put it in the same folder as python code.

<br>

## Code & Analysis
---
The basic version:
```python
from mrjob.job import MRJob
from mrjob.step import MRStep

class MostPopularMovie(MRJob):
    def steps(self):
        return [
            MRStep(mapper = self.mapper_get_ratings,
                   reducer = self.reducer_count_ratings),
            MRStep(mapper = self.mapper_passthrough,
                   reducer = self.reducer_find_max)
        ]

    def mapper_get_ratings(self, _, line):
        (userID, movieID, rating, timestamp) = line.split('\t')
        yield movieID, 1

    # The following mapper does nothing; it's just here to avoid a bug in
    # some versions of mrjob related to "non-script steps." Normally this
    # wouldn't be needed.
    def mapper_passthrough(self, key, value):
        yield key, value

    def reducer_count_ratings(self, key, values):
        yield None, (sum(values), key)

    def reducer_find_max(self, key, values):
        yield max(values)

if __name__ == '__main__':
    MostPopularMovie.run()
```
An improved version:
```python
from mrjob.job import MRJob
from mrjob.step import MRStep

class MostPopularMovie(MRJob):

    def configure_options(self):
        super(MostPopularMovie, self).configure_options()
        self.add_file_option('--items', help = 'Path to u.item')

    def steps(self):
        return [
            MRStep(mapper = self.mapper_get_ratings,
                   reducer_init = self.reducer_init,
                   reducer = self.reducer_count_ratings),
            MRStep(mapper = self.mapper_passthrough,
                   reducer = self.reducer_find_max)
        ]

    def mapper_get_ratings(self, _, line):
        (userID, movieID, rating, timestamp) = line.split('\t')
        yield movieID, 1

    def reducer_init(self):
        self.movieNames = {}            # opens up a dictionary
        with open("u.ITEM") as f:
            for line in f:
                fields = line.split('|')
                self.movieNames[fields[0]] = fields[1].decode('utf-8', 'ignore')

    def reducer_count_ratings(self, key, values):
        yield None, (sum(values), self.movieNames[key])

    # The following mapper does nothing; it's just here to avoid a bug in
    # some versions of mrjob related to "non-script steps." Normally this
    # wouldn't be needed.
    def mapper_passthrough(self, key, value):
        yield key, value

    def reducer_find_max(self, key, values):
        yield max(values)

if __name__ == '__main__':
    MostPopularMovie.run()
```


<br>

## Run the Code
---
The basic version:

Execute the following command in the Python Console.
```shell
import os
os.chdir("..")
cd 8. Most Popular Movie
!python MostPopularMovie.py ml-100k/u.data > MostPopularMovie.txt
```
The result looks like the following.
```
583	"50"
```

The improved version:

Execute the following command in the Python Console.
```shell
!python MostPopularMovieNicer.py --items=ml-100k/u.item ml-100k/u.data > MostPopularMovieNicer.txt
```
The result looks like the following.
```
583	"Star Wars (1977)"
```

<br><br>
