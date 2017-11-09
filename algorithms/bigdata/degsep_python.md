---
layout: algorithm
comments: true
mathjax: true
---

# Degrees of Separation (Breath First Search)

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
# Call this with one argument: the character ID you are starting from.
# For example, Spider Man is 5306, The Hulk is 2548. Refer to Marvel-names.txt
# for others.

import sys

print 'Creating BFS starting input for character ' + sys.argv[1]
    # sys.argv[1] is command line argument

with open("BFS-iteration-0.txt", 'w') as out:
    # output file

    with open("Marvel-graph.txt") as f:
        # input file

        for line in f:
            fields = line.split()
            heroID = fields[0]
            numConnections = len(fields) - 1
                # number of neighbors for each node
            connections = fields[-numConnections:]
                # use a list "connections" to store all the neighbors

            color = 'WHITE'
                # the node initially is marked unvisited (white)
            distance = 9999
                # all nodes (except starting node) has a starting distance 9999

            if (heroID == sys.argv[1]):
                # starting node has color gray and distance 0
                color = 'GRAY'
                distance = 0

            if (heroID != ''):
                edges = ','.join(connections)                                   # join all neighbors with ','
                outStr = '|'.join((heroID, edges, str(distance), color))
                    # join the new fields with '|'
                out.write(outStr)
                out.write("\n")

    f.close()

out.close()
```

<br>

## Run the Code
---
Execute the following command in the Python Console.
```shell
!python ProcessMarvel.py 2548
```
The result looks like the following.
```
5988|748,1722,3752,4655,5743,1872,3413,5527,6368,6085,4319,4728,1636,2397,3364,4001,1614,1819,1585,732,2660,3952,2507,3891,2070,2239,2602,612,1352,5447,4548,1596,5488,1605,5517,11,479,2554,2043,17,865,4292,6312,473,534,1479,6375,4456|9999|WHITE
5989|4080,4264,4446,3779,2430,2297,6169,3530,3272,4282,6432,2548,4140,185,105,3878,2429,1334,4595,2767,3956,3877,4776,4946,3407,128,269,5775,5121,481,5516,4758,4053,1044,1602,3889,1535,6038,533,3986|9999|WHITE
5982|217,595,1194,3308,2940,1815,794,1503,5197,859,5096,6039,2664,651,2244,528,284,1449,1097,1172,1092,108,3405,5204,387,4607,4545,3705,4930,1805,4712,4404,247,4754,4427,1845,536,5795,5978,533,3984,6056|9999|WHITE
5983|1165,3836,4361,1282,716,4289,4646,6300,5084,2397,4454,1913,5861,5485|9999|WHITE
5980|2731,3712,1587,6084,2472,2546,6313,875,859,323,2664,1469,522,2506,2919,2423,3624,5736,5046,1787,5776,3245,3840,2399|9999|WHITE
... ...
```

<br><br>
