---
layout: algorithm
comments: true
mathjax: true
---

# Friends by Age

<br>

## Data
---
Download the `fakefriends.csv` file from [here](https://raw.githubusercontent.com/shevapato2008/HadoopMapReduce_Python/master/2.%20Friends%20By%20Age/fakefriends.csv "fakefriends.csv") and put it in the same folder as python code.

The data `fakefriends.csv` looks something like below.
```
0,Will,33,385
1,Jean-Luc,26,2
2,Hugh,55,221
3,Deanna,40,465
4,Quark,68,21
5,Weyoun,59,318
6,Gowron,37,220
7,Will,54,307
8,Jadzia,38,380
9,Hugh,27,181
10,Odo,53,191
... ...
```

<br>

## Code & Analysis
---
```python
from mrjob.job import MRJob

class MRFriendsByAge(MRJob):
    def mapper(self, _, line):
        (ID, name, age, numFriends) = line.split(',')
        yield age, float(numFriends)
        # Cast numFriends as a float.
        # This tells python we can do arithmetic operations on it.

    def reducer(self, age, numFriends):
        total = 0
        numElements = 0
        for x in numFriends:
            total += x
            numElements += 1
        yield age, total / numElements

if __name__ == '__main__':
    MRFriendsByAge.run()
```

<br>

## Run the Code
---
Execute the following command in the Python Console.
```shell
import os
os.chdir("..")
cd 2. Friends By Age
!python FriendsByAge.py fakefriends.csv > friendsbyage.txt
```
The result looks like the following.
```
"18"	343.375
"19"	213.27272727272728
"20"	165.0
"21"	350.875
"22"	206.42857142857142
"23"	246.3
"24"	233.8
"25"	197.45454545454547
"26"	242.05882352941177
"27"	228.125
"28"	209.1
... ...
```

<br><br>
