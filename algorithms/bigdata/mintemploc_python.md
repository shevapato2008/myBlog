---
layout: algorithm
comments: true
mathjax: true
---

# Minimum Temperature by Location

<br>

## Data
---
Download the `1800.csv` file from [here](https://raw.githubusercontent.com/shevapato2008/HadoopMapReduce_Python/master/3.%20Minimum%20Temperature%20By%20Location/1800.csv "1800.csv") and put it in the same folder as python code.

The data `1800.csv` looks something like below.
```
ITE00100554,18000101,TMAX,-75,,,E,
ITE00100554,18000101,TMIN,-148,,,E,
GM000010962,18000101,PRCP,0,,,E,
EZE00100082,18000101,TMAX,-86,,,E,
EZE00100082,18000101,TMIN,-135,,,E,
ITE00100554,18000102,TMAX,-60,,I,E,
ITE00100554,18000102,TMIN,-125,,,E,
GM000010962,18000102,PRCP,0,,,E,
EZE00100082,18000102,TMAX,-44,,,E,
EZE00100082,18000102,TMIN,-130,,,E,
... ...
```

<br>

## Code & Analysis
---
```python
from mrjob.job import MRJob

class MRMinTemperature(MRJob):

    def MakeFahrenheit(self, tenthsOfCelsius):
        celsius = float(tenthsOfCelsius) / 10.0
        fahrenheit = celsius * 1.8 + 32.0
        return fahrenheit

    def mapper(self, _, line):
        (location, date, type, data, x, y, z, w) = line.split(',')
        if (type == 'TMIN'):
            temperature = self.MakeFahrenheit(data)
            yield location, temperature

    def reducer(self, location, temps):
        yield location, min(temps)

if __name__ == '__main__':
    MRMinTemperature.run()
```

<br>

## Run the Code
---
Execute the following command in the Python Console.
```shell
import os
os.chdir("..")
cd 3. Minimum Temperature By Location
!python MRMinTemperature.py 1800.csv > mintemps.txt
```
The result looks like the following.
```
"EZE00100082"	7.699999999999999
"ITE00100554"	5.359999999999999
```

<br><br>
