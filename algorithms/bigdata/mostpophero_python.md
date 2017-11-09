---
layout: algorithm
comments: true
mathjax: true
---

# Most Popular Superhero

<br>

## Data
---
Download `Marvel-Graph.txt` file from [here](https://raw.githubusercontent.com/shevapato2008/HadoopMapReduce_Python/master/9.%20Most%20Popular%20Superhero/Marvel-Graph.txt "Marvel-Graph.txt") and `Marvel-Names.txt` from [here](https://raw.githubusercontent.com/shevapato2008/HadoopMapReduce_Python/master/9.%20Most%20Popular%20Superhero/Marvel-Names.txt "Marvel-Names.txt"). Then put them in the same folder as python code.

The `Marvel-Graph.txt` file looks like below.
```
5988 748 1722 3752 4655 5743 1872 3413 5527 6368 6085 4319 4728 1636 2397 3364 4001 1614 1819 1585 732 2660 3952 2507 3891 2070 2239 2602 612 1352 5447 4548 1596 5488 1605 5517 11 479 2554 2043 17 865 4292 6312 473 534 1479 6375 4456
5989 4080 4264 4446 3779 2430 2297 6169 3530 3272 4282 6432 2548 4140 185 105 3878 2429 1334 4595 2767 3956 3877 4776 4946 3407 128 269 5775 5121 481 5516 4758 4053 1044 1602 3889 1535 6038 533 3986
... ...
```
The `Marvel-Names.txt` file looks like below.
```
1 "24-HOUR MAN/EMMANUEL"
2 "3-D MAN/CHARLES CHAN"
3 "4-D MAN/MERCURIO"
4 "8-BALL/"
5 "A"
6 "A'YIN"
7 "ABBOTT, JACK"
8 "ABCISSA"
9 "ABEL"
10 "ABOMINATION/EMIL BLO"
... ...
```

<br>

## Code & Analysis
---
```python
from mrjob.job import MRJob
from mrjob.step import MRStep

class MostPopularSuperHero(MRJob):

    def configure_options(self):
        super(MostPopularSuperHero, self).configure_options()
        self.add_file_option('--names', help = 'Path to Marvel-names.txt')
            # This will send Marvel-names.txt to all the nodes running this job.

    def steps(self):
        return [
            MRStep(mapper = self.mapper_count_friends_per_line,
                   reducer = self.reducer_combine_friends),
            MRStep(mapper = self.mapper_prep_for_sort,
                   mapper_init = self.load_name_dictionary,
                   reducer = self.reducer_find_max_friends)
        ]

    def mapper_count_friends_per_line(self, _, line):
        fields = line.split()
        heroID = fields[0]
        numFriends = len(fields) - 1
        yield int(heroID), int(numFriends)
            # count number of friends for each line

    def reducer_combine_friends(self, heroID, friendCounts):
        yield heroID, sum(friendCounts)
            # sum of number of friends for each superhero

    def mapper_prep_for_sort(self, heroID, friendCounts):
        heroName = self.heroNames[heroID]
            # convert hero ID to hero name
        yield None, (friendCounts, heroName)
            # by a dictionary defined below

    def reducer_find_max_friends(self, key, value):
        yield max(value)

    def load_name_dictionary(self):
        self.heroNames = {}
            # use self.heroNames makes heroNames
        with open("Marvel-names.txt") as f:
            # dictionary usable everywhere in this class.
            for line in f:
                fields = line.split('"')
                    # split based on quotes
                heroID = int(fields[0])
                self.heroNames[heroID] = unicode(fields[1], errors = 'ignore')

if __name__ == '__main__':
    MostPopularSuperHero.run()
```

<br>

## Run the Code
---
Execute the following command in the Python Console.
```shell
import os
os.chdir("..")
cd 9. Most Popular Superhero
!python MostPopularSuperhero.py --names=Marvel-names.txt Marvel-Graph.txt > MostPopularSuperhero.txt
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
1933	"CAPTAIN AMERICA"
```

<br><br>
