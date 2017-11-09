---
layout: algorithm
comments: true
mathjax: true
---

# Total Spent by Customer

<br>

## Data
---
Download the `customer-orders.csv` file from [here](https://raw.githubusercontent.com/shevapato2008/HadoopMapReduce_Python/master/6.%20Total%20Spent%20by%20Customer/customer-orders.csv "customer-orders.csv") and put it in the same folder as python code.

The data `customer-orders.csv` looks something like below.
```
44,8602,37.19
35,5368,65.89
2,3391,40.64
47,6694,14.98
29,680,13.08
91,8900,24.59
70,3959,68.68
... ...
```

<br>

## Code & Analysis
---
The basic version:
```python
from mrjob.job import MRJob

class MRCustomerSpent(MRJob):

    def mapper(self, _, line):
        (customerID, itemID, spent) = line.split(',')
        yield customerID, float(spent)

    def reducer(self, customerID, spent):
        yield customerID, sum(spent)

if __name__ == '__main__':
    MRCustomerSpent.run();
```

The sorted version:
```python
from mrjob.job import MRJob
from mrjob.step import MRStep

class SpendByCustomerSorted(MRJob):

    def steps(self):
        return [
            MRStep(mapper = self.mapper_getSpent,
                   reducer = self.reducer_totalSpent),
            MRStep(mapper = self.mapper_makeSpentKey,
                   reducer = self.reducer_outputTopSpent)
        ]

    def mapper_getSpent(self, _, line):
        (customerID, itemID, order) = line.split(',')
        yield customerID, float(order)

    def reducer_totalSpent(self, customerID, orders):
        yield customerID, sum(orders)

    def mapper_makeSpentKey(self, customerID, totalSpent):
        yield '%04.02f'%float(totalSpent), customerID

    def reducer_outputTopSpent(self, spent, customerIDList):
        for customerID in customerIDList:
            yield customerID, spent

if __name__ == '__main__':
    SpendByCustomerSorted.run();
```

<br>

## Run the Code
---
The basic version:

Execute the following command in the Python Console.
```shell
import os
os.chdir("..")
cd 6. Total Spent by Customer
!python CustomerSpent.py customer-orders.csv > customerspent.txt
```
The result looks like the following.
```
"0"	5524.950000000002
"1"	4958.600000000001
"10"	4819.7
"11"	5152.29
"12"	4664.589999999999
"13"	4367.619999999999
"14"	4735.030000000001
"15"	5413.510000000001
"16"	4979.060000000001
"17"	5032.680000000001
... ...
```

The sorted version:

Execute the following command in the Python Console.
```shell
!python CustomerSpentSorted.py customer-orders.csv > customerspentsorted.txt
```
The result looks like the following.
```
"45"	"3309.38"
"79"	"3790.57"
"96"	"3924.23"
"23"	"4042.65"
"99"	"4172.29"
"75"	"4178.50"
"36"	"4278.05"
"98"	"4297.26"
"47"	"4316.30"
"77"	"4327.73"
"13"	"4367.62"
"48"	"4384.33"
... ...
```

<br><br>
