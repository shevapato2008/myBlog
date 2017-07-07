---
layout: post
title: 10 minutes to pandas
meta: An elementary tutorial on pandas library.
comments: true
mathjax: false
---

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

<br>

## Object Creation
---

See the [Data Structure Intro section](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dsintro).

### Create a Series

Create a **Series** by passing a list of values, letting pandas create a default integer index:


```python
s = pd.Series([1, 3, 5, np.nan, 6, 8])
```


```python
s
```




    0    1.0
    1    3.0
    2    5.0
    3    NaN
    4    6.0
    5    8.0
    dtype: float64



### Create a DataFrame

+ From a **numpy array**, with a datetime **index** and labeled **columns**:


```python
dates = pd.date_range('20130101', periods = 6)
```


```python
dates
```




    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')




```python
df = pd.DataFrame(np.random.randn(6, 4), index = dates, columns = list('ABCD'))
```


```python
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.151245</td>
      <td>2.135387</td>
      <td>0.315433</td>
      <td>1.244296</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>-0.060078</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>1.042195</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>1.058137</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.499296</td>
      <td>0.502565</td>
      <td>-1.101389</td>
      <td>-0.382417</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.737790</td>
      <td>-0.106322</td>
      <td>-0.726821</td>
      <td>1.511071</td>
    </tr>
  </tbody>
</table>
</div>



* From a **dict** of objects that can be converted to series-like.


```python
df2 = pd.DataFrame({ 'A' : 1.,
                     'B' : pd.Timestamp('20130102'),
                     'C' : pd.Series(1,index=list(range(4)),dtype='float32'),
                     'D' : np.array([3] * 4,dtype='int32'),
                     'E' : pd.Categorical(["test","train","test","train"]),
                     'F' : 'foo' })
```


```python
df2
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>



Having specific dtypes


```python
df2.dtypes
```




    A           float64
    B    datetime64[ns]
    C           float32
    D             int32
    E          category
    F            object
    dtype: object



If you’re using IPython, tab completion for column names (as well as public attributes) is automatically enabled. Here’s a subset of the attributes that will be completed:

`df2.<TAB>` helps look up the list of all available functions.

<br><br>

## Viewing Data
---
See the [Basics section](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics "Essential Basic Functionality")

See the top & bottom rows of the frame.


```python
df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.151245</td>
      <td>2.135387</td>
      <td>0.315433</td>
      <td>1.244296</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>-0.060078</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>1.042195</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>1.058137</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.499296</td>
      <td>0.502565</td>
      <td>-1.101389</td>
      <td>-0.382417</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail(3)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>1.058137</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.499296</td>
      <td>0.502565</td>
      <td>-1.101389</td>
      <td>-0.382417</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.737790</td>
      <td>-0.106322</td>
      <td>-0.726821</td>
      <td>1.511071</td>
    </tr>
  </tbody>
</table>
</div>



Display the index, colums, and the underlying numpy data.


```python
df.index
```




    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')




```python
df.columns
```




    Index([u'A', u'B', u'C', u'D'], dtype='object')




```python
df.values
```




    array([[-1.15124488,  2.1353869 ,  0.3154332 ,  1.24429637],
           [ 0.92097955, -0.00792084, -0.67835908, -0.06007828],
           [-1.71368096, -0.59253737,  0.59461783,  1.04219508],
           [ 0.29116065, -1.01113718, -0.7364927 ,  1.05813683],
           [-1.49929636,  0.50256457, -1.10138889, -0.38241723],
           [ 1.7377902 , -0.10632165, -0.72682066,  1.51107124]])



Describe shows a quick statistic summary of your data.


```python
df.describe()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-0.235715</td>
      <td>0.153339</td>
      <td>-0.388835</td>
      <td>0.735534</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.423340</td>
      <td>1.100567</td>
      <td>0.676732</td>
      <td>0.766971</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-1.713681</td>
      <td>-1.011137</td>
      <td>-1.101389</td>
      <td>-0.382417</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-1.412283</td>
      <td>-0.470983</td>
      <td>-0.734075</td>
      <td>0.215490</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-0.430042</td>
      <td>-0.057121</td>
      <td>-0.702590</td>
      <td>1.050166</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.763525</td>
      <td>0.374943</td>
      <td>0.066985</td>
      <td>1.197756</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.737790</td>
      <td>2.135387</td>
      <td>0.594618</td>
      <td>1.511071</td>
    </tr>
  </tbody>
</table>
</div>



Transposing your data.


```python
df.T
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2013-01-01 00:00:00</th>
      <th>2013-01-02 00:00:00</th>
      <th>2013-01-03 00:00:00</th>
      <th>2013-01-04 00:00:00</th>
      <th>2013-01-05 00:00:00</th>
      <th>2013-01-06 00:00:00</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>-1.151245</td>
      <td>0.920980</td>
      <td>-1.713681</td>
      <td>0.291161</td>
      <td>-1.499296</td>
      <td>1.737790</td>
    </tr>
    <tr>
      <th>B</th>
      <td>2.135387</td>
      <td>-0.007921</td>
      <td>-0.592537</td>
      <td>-1.011137</td>
      <td>0.502565</td>
      <td>-0.106322</td>
    </tr>
    <tr>
      <th>C</th>
      <td>0.315433</td>
      <td>-0.678359</td>
      <td>0.594618</td>
      <td>-0.736493</td>
      <td>-1.101389</td>
      <td>-0.726821</td>
    </tr>
    <tr>
      <th>D</th>
      <td>1.244296</td>
      <td>-0.060078</td>
      <td>1.042195</td>
      <td>1.058137</td>
      <td>-0.382417</td>
      <td>1.511071</td>
    </tr>
  </tbody>
</table>
</div>



Sorting by an axis.


```python
df.sort_index(axis = 1, ascending = False)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>D</th>
      <th>C</th>
      <th>B</th>
      <th>A</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>1.244296</td>
      <td>0.315433</td>
      <td>2.135387</td>
      <td>-1.151245</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.060078</td>
      <td>-0.678359</td>
      <td>-0.007921</td>
      <td>0.920980</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>1.042195</td>
      <td>0.594618</td>
      <td>-0.592537</td>
      <td>-1.713681</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>1.058137</td>
      <td>-0.736493</td>
      <td>-1.011137</td>
      <td>0.291161</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-0.382417</td>
      <td>-1.101389</td>
      <td>0.502565</td>
      <td>-1.499296</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.511071</td>
      <td>-0.726821</td>
      <td>-0.106322</td>
      <td>1.737790</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.sort_values(by = 'B', ascending = False)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.151245</td>
      <td>2.135387</td>
      <td>0.315433</td>
      <td>1.244296</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.499296</td>
      <td>0.502565</td>
      <td>-1.101389</td>
      <td>-0.382417</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>-0.060078</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.737790</td>
      <td>-0.106322</td>
      <td>-0.726821</td>
      <td>1.511071</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>1.042195</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>1.058137</td>
    </tr>
  </tbody>
</table>
</div>



<br><br>

## Selection
---

**Note:** While standard Python/Numpy expressions for selecting and setting are intuitive and come in handy for interactive work, for production code, we recommend the optimized pandas data access methods, .at; .iat, .loc, .iloc and .ix.

See the indexing documentation [Indexing and Selecting Data](https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing "Indexing and Selecting Data") and [MultiIndex / Advanced Indexing](https://pandas.pydata.org/pandas-docs/stable/advanced.html#advanced "MultiIndex / Advanced Indexing").

### Getting

Selecting a single column, which yields a *Series*.


```python
df['A']
```




    2013-01-01   -1.151245
    2013-01-02    0.920980
    2013-01-03   -1.713681
    2013-01-04    0.291161
    2013-01-05   -1.499296
    2013-01-06    1.737790
    Freq: D, Name: A, dtype: float64




```python
df.A
```




    2013-01-01   -1.151245
    2013-01-02    0.920980
    2013-01-03   -1.713681
    2013-01-04    0.291161
    2013-01-05   -1.499296
    2013-01-06    1.737790
    Freq: D, Name: A, dtype: float64



Selecting via `[]`, which slices the rows.


```python
df[0 : 3]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.151245</td>
      <td>2.135387</td>
      <td>0.315433</td>
      <td>1.244296</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>-0.060078</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>1.042195</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['20130102' : '20130104']
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>-0.060078</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>1.042195</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>1.058137</td>
    </tr>
  </tbody>
</table>
</div>



### Selection by Label

See more in [Selection by Label](https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-label "Selection By Label").

For getting a cross section using a Label.


```python
df.loc[dates[0]]
```




    A   -1.151245
    B    2.135387
    C    0.315433
    D    1.244296
    Name: 2013-01-01 00:00:00, dtype: float64



Selecting on a multi-axis by label.


```python
df.loc[:, ['A', 'B']]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.151245</td>
      <td>2.135387</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.499296</td>
      <td>0.502565</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.737790</td>
      <td>-0.106322</td>
    </tr>
  </tbody>
</table>
</div>



Showing label slicing, both endpoints are _included_.


```python
df.loc['20130102' : '20130104', ['A', 'B']]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
    </tr>
  </tbody>
</table>
</div>



Reduction in the dimensions of the returned object.


```python
df.loc['20130102', ['A', 'B']]
```




    A    0.920980
    B   -0.007921
    Name: 2013-01-02 00:00:00, dtype: float64



For getting a scalar value


```python
df.loc[dates[0], 'A']
```




    -1.1512448829323327



For getting fast access to a scalar (equiv to the prior method)


```python
df.at[dates[0], 'A']
```




    -1.1512448829323327



### Selection by Position
See more in [Selection by Position](https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-integer "Selection by Position")

Select via the position of the passed integers


```python
df.iloc[3]
```




    A    0.291161
    B   -1.011137
    C   -0.736493
    D    1.058137
    Name: 2013-01-04 00:00:00, dtype: float64



By integer slices, acting similar to nump/python


```python
df.iloc[3 : 5, 0 : 2]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.499296</td>
      <td>0.502565</td>
    </tr>
  </tbody>
</table>
</div>



By lists of integer position locations, similar to the numpy/python style.


```python
df.iloc[[1, 2, 4], [0, 2]]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.678359</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>0.594618</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.499296</td>
      <td>-1.101389</td>
    </tr>
  </tbody>
</table>
</div>



For slicing rows explicitly


```python
df.iloc[1 : 3, :]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>-0.060078</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>1.042195</td>
    </tr>
  </tbody>
</table>
</div>



For slicing columns explicitly


```python
df.iloc[:, 1 : 3]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>2.135387</td>
      <td>0.315433</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.007921</td>
      <td>-0.678359</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.592537</td>
      <td>0.594618</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-1.011137</td>
      <td>-0.736493</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.502565</td>
      <td>-1.101389</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.106322</td>
      <td>-0.726821</td>
    </tr>
  </tbody>
</table>
</div>



For getting a value explicitly


```python
df.iloc[1, 1]
```




    -0.0079208356499683181



For getting fast access to a scalar (equiv to the prior method)


```python
df.iat[1, 1]
```




    -0.0079208356499683181



### Boolean Indexing

Using a single column's values to select data.


```python
df[df.A > 0]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>-0.060078</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>1.058137</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.737790</td>
      <td>-0.106322</td>
      <td>-0.726821</td>
      <td>1.511071</td>
    </tr>
  </tbody>
</table>
</div>



Selecting values from a DataFrame where a boolean condition is met.


```python
df[df > 0]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>NaN</td>
      <td>2.135387</td>
      <td>0.315433</td>
      <td>1.244296</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.594618</td>
      <td>1.042195</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.058137</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>NaN</td>
      <td>0.502565</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.737790</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.511071</td>
    </tr>
  </tbody>
</table>
</div>



Using the `isin()` method for filtering:


```python
df2 = df.copy()
```


```python
df2['E'] = ['one', 'one', 'two', 'three', 'four', 'three']
```


```python
df2
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.151245</td>
      <td>2.135387</td>
      <td>0.315433</td>
      <td>1.244296</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>-0.060078</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>1.042195</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>1.058137</td>
      <td>three</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.499296</td>
      <td>0.502565</td>
      <td>-1.101389</td>
      <td>-0.382417</td>
      <td>four</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.737790</td>
      <td>-0.106322</td>
      <td>-0.726821</td>
      <td>1.511071</td>
      <td>three</td>
    </tr>
  </tbody>
</table>
</div>



### Setting

Setting a new column automatically aligns the data by the indexes.


```python
s1 = pd.Series([1, 2, 3, 4, 5, 6], index = pd.date_range('20130102', periods = 6))
s1
```




    2013-01-02    1
    2013-01-03    2
    2013-01-04    3
    2013-01-05    4
    2013-01-06    5
    2013-01-07    6
    Freq: D, dtype: int64



Setting values by label


```python
df.at[dates[0], 'A'] = 0
```

Setting values by position


```python
df.iat[0, 1] = 0
```

Setting by assigning with a numpy array


```python
df.loc[:, 'D'] = np.array([5] * len(df))
```


```python
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.315433</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.499296</td>
      <td>0.502565</td>
      <td>-1.101389</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>1.737790</td>
      <td>-0.106322</td>
      <td>-0.726821</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



A **`where`** operation with setting.


```python
df2 = df.copy()
```


```python
df2[df2 > 0] = - df2
```


```python
df2
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-0.315433</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>-0.594618</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.499296</td>
      <td>-0.502565</td>
      <td>-1.101389</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-1.737790</td>
      <td>-0.106322</td>
      <td>-0.726821</td>
      <td>-5</td>
    </tr>
  </tbody>
</table>
</div>



<br><br>

## Missing Data
---

pandas primarily uses the value `np.nan` to represent missing data. It is by default not included in computations. See the [Missing Data Section](https://pandas.pydata.org/pandas-docs/stable/missing_data.html#missing-data "Working with missing data")

Reindexing allows you to change/add/delete the index on a specified axis. This returns a copy of the data.


```python
df1 = df.reindex(index = dates[0 : 4], columns = list(df.columns) + ['E'])
```


```python
df1
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.315433</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.loc[dates[0]: dates[1], 'E'] = 1
```


```python
df1
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.315433</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



To drop any rows that have missing data.


```python
df1.dropna(how = 'any')
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.315433</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.92098</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



Filling missing data


```python
df1.fillna(value = 5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.315433</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.678359</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.713681</td>
      <td>-0.592537</td>
      <td>0.594618</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.291161</td>
      <td>-1.011137</td>
      <td>-0.736493</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



To get the boolean mask where values are `nan`


```python
pd.isnull(df1)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



<br><br>

## Operations
---
See the [Basic section on Binary Ops](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics-binop "Flexible binary operations")

### Stats

Operations in general _exclude_ missing data.

Performing a descriptive statistic.


```python
df.mean()
```




    A   -0.043841
    B   -0.202559
    C   -0.388835
    D    5.000000
    dtype: float64




```python
df.mean(0)    # same as above
```




    A   -0.043841
    B   -0.202559
    C   -0.388835
    D    5.000000
    dtype: float64



Same operation on the other axis.


```python
df.mean(1)
```




    2013-01-01    1.328858
    2013-01-02    1.308675
    2013-01-03    0.822100
    2013-01-04    0.885883
    2013-01-05    0.725470
    2013-01-06    1.476162
    Freq: D, dtype: float64



Operating with objects that have different dimensionality and need alignment. In addition, pandas automatically broadcasts along the specified dimension.


```python
s = pd.Series([1, 3, 5, np.nan, 6, 8], index = dates).shift(2)
```


```python
s
```




    2013-01-01    NaN
    2013-01-02    NaN
    2013-01-03    1.0
    2013-01-04    3.0
    2013-01-05    5.0
    2013-01-06    NaN
    Freq: D, dtype: float64




```python
df.sub(s, axis = 'index')
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-2.713681</td>
      <td>-1.592537</td>
      <td>-0.405382</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-2.708839</td>
      <td>-4.011137</td>
      <td>-3.736493</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-6.499296</td>
      <td>-4.497435</td>
      <td>-6.101389</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### Apply

Applying functions to the data.


```python
df.apply(np.cumsum)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.315433</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.920980</td>
      <td>-0.007921</td>
      <td>-0.362926</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.792701</td>
      <td>-0.600458</td>
      <td>0.231692</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.501541</td>
      <td>-1.611595</td>
      <td>-0.504801</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-2.000837</td>
      <td>-1.109031</td>
      <td>-1.606190</td>
      <td>25</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.263047</td>
      <td>-1.215352</td>
      <td>-2.333010</td>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.apply(lambda x: x.max() - x.min())
```




    A    3.451471
    B    1.513702
    C    1.696007
    D    0.000000
    dtype: float64



### Histogramming

See more at [Histogramming and Discretization](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics-discretization "Histogramming and Discretization").


```python
s = pd.Series(np.random.randint(0, 7, size = 10))
```


```python
s
```




    0    5
    1    2
    2    3
    3    2
    4    4
    5    3
    6    5
    7    5
    8    6
    9    6
    dtype: int64



### String Methods

Series is equipped with a set of string processing methods in the _str_ attribute that make it easy to operate on each element of the array, as in the code snippet below. Note that pattern-matching in _str_ generally uses [regular expressions](https://docs.python.org/2/library/re.html "Regular expression operations") by default (and in some cases always uses them). See more at [Vectorizing String Methods](https://pandas.pydata.org/pandas-docs/stable/text.html#text-string-methods "Working with Text Data").


```python
s = pd.Series(['A', 'B', 'C', 'Aaba', 'Baca', np.nan, 'CABA', 'dog', 'cat'])
```


```python
s.str.lower()
```




    0       a
    1       b
    2       c
    3    aaba
    4    baca
    5     NaN
    6    caba
    7     dog
    8     cat
    dtype: object



<br><br>

## Merge
---
### Concat

**`pd.concat()`** combines dataframes **vertically**.
See the [Merging section](https://pandas.pydata.org/pandas-docs/stable/merging.html#merging "Merge, join, and concatenate").

Concatenating pandas objects together with **`concat()`**:


```python
df = pd.DataFrame(np.random.randn(10, 4))
```


```python
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.207081</td>
      <td>0.471334</td>
      <td>-0.838968</td>
      <td>1.504522</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.859450</td>
      <td>-0.379802</td>
      <td>-0.640044</td>
      <td>-2.220086</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.215174</td>
      <td>0.218817</td>
      <td>-0.050697</td>
      <td>1.061165</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.201498</td>
      <td>0.387249</td>
      <td>-1.418478</td>
      <td>0.515991</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.529626</td>
      <td>-1.701973</td>
      <td>-0.919016</td>
      <td>-0.089885</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.184360</td>
      <td>1.762073</td>
      <td>1.638023</td>
      <td>1.908229</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1.053077</td>
      <td>0.284344</td>
      <td>0.794606</td>
      <td>-0.651995</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.935268</td>
      <td>1.092794</td>
      <td>-0.353333</td>
      <td>0.077360</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.753558</td>
      <td>-1.601098</td>
      <td>0.647484</td>
      <td>-0.491383</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1.394530</td>
      <td>-0.355425</td>
      <td>0.482833</td>
      <td>0.882305</td>
    </tr>
  </tbody>
</table>
</div>



Break it into pieces.


```python
pieces = [df[: 3], df[3 : 7], df[7 : ]]
```


```python
pieces
```




    [          0         1         2         3
     0  0.207081  0.471334 -0.838968  1.504522
     1  0.859450 -0.379802 -0.640044 -2.220086
     2 -0.215174  0.218817 -0.050697  1.061165,
               0         1         2         3
     3  0.201498  0.387249 -1.418478  0.515991
     4 -0.529626 -1.701973 -0.919016 -0.089885
     5 -0.184360  1.762073  1.638023  1.908229
     6  1.053077  0.284344  0.794606 -0.651995,
               0         1         2         3
     7  0.935268  1.092794 -0.353333  0.077360
     8  0.753558 -1.601098  0.647484 -0.491383
     9  1.394530 -0.355425  0.482833  0.882305]




```python
pd.concat(pieces)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.207081</td>
      <td>0.471334</td>
      <td>-0.838968</td>
      <td>1.504522</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.859450</td>
      <td>-0.379802</td>
      <td>-0.640044</td>
      <td>-2.220086</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.215174</td>
      <td>0.218817</td>
      <td>-0.050697</td>
      <td>1.061165</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.201498</td>
      <td>0.387249</td>
      <td>-1.418478</td>
      <td>0.515991</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.529626</td>
      <td>-1.701973</td>
      <td>-0.919016</td>
      <td>-0.089885</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.184360</td>
      <td>1.762073</td>
      <td>1.638023</td>
      <td>1.908229</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1.053077</td>
      <td>0.284344</td>
      <td>0.794606</td>
      <td>-0.651995</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.935268</td>
      <td>1.092794</td>
      <td>-0.353333</td>
      <td>0.077360</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.753558</td>
      <td>-1.601098</td>
      <td>0.647484</td>
      <td>-0.491383</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1.394530</td>
      <td>-0.355425</td>
      <td>0.482833</td>
      <td>0.882305</td>
    </tr>
  </tbody>
</table>
</div>



### Join

**`pd.merge()`** merges dataframes **horizontally**. Just like SQL style merges. See the [Database style joining](https://pandas.pydata.org/pandas-docs/stable/merging.html#merging-join "Database-style DataFrame joining/merging").

Example 1:


```python
left = pd.DataFrame({'key': ['foo', 'foo'], 'lval': [1, 2]})
```


```python
right = pd.DataFrame({'key': ['foo', 'foo'], 'rval': [4, 5]})
```


```python
left
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
right
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(left, right, on = 'key')
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>foo</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



Example 2:


```python
left = pd.DataFrame({'key': ['foo', 'bar'], 'lval': [1, 2]})
```


```python
right = pd.DataFrame({'key': ['foo', 'bar'], 'rval': [4, 5]})
```


```python
left
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
right
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(left, right, on = 'key')
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



### Append

Append rows to a dataframe. See the [Appending](https://pandas.pydata.org/pandas-docs/stable/merging.html#merging-concatenation "Concatenating using append").


```python
df = pd.DataFrame(np.random.randn(8, 4), columns = ['A', 'B', 'C', 'D'])
```


```python
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.303744</td>
      <td>-1.627896</td>
      <td>0.272797</td>
      <td>-0.007977</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.012547</td>
      <td>0.893648</td>
      <td>-1.324008</td>
      <td>0.982538</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.112323</td>
      <td>-0.598043</td>
      <td>0.428953</td>
      <td>0.755541</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.837114</td>
      <td>-1.330702</td>
      <td>-1.678282</td>
      <td>-0.472006</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.250183</td>
      <td>0.039900</td>
      <td>-0.390019</td>
      <td>1.679978</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.273232</td>
      <td>0.769950</td>
      <td>0.468201</td>
      <td>-0.619422</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.601851</td>
      <td>-0.637132</td>
      <td>0.201432</td>
      <td>-0.710817</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-1.140444</td>
      <td>0.403012</td>
      <td>0.576544</td>
      <td>-0.385594</td>
    </tr>
  </tbody>
</table>
</div>




```python
s = df.iloc[3]
```


```python
s
```




    A    1.837114
    B   -1.330702
    C   -1.678282
    D   -0.472006
    Name: 3, dtype: float64




```python
df.append(s, ignore_index = True)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.303744</td>
      <td>-1.627896</td>
      <td>0.272797</td>
      <td>-0.007977</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.012547</td>
      <td>0.893648</td>
      <td>-1.324008</td>
      <td>0.982538</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.112323</td>
      <td>-0.598043</td>
      <td>0.428953</td>
      <td>0.755541</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.837114</td>
      <td>-1.330702</td>
      <td>-1.678282</td>
      <td>-0.472006</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.250183</td>
      <td>0.039900</td>
      <td>-0.390019</td>
      <td>1.679978</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.273232</td>
      <td>0.769950</td>
      <td>0.468201</td>
      <td>-0.619422</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.601851</td>
      <td>-0.637132</td>
      <td>0.201432</td>
      <td>-0.710817</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-1.140444</td>
      <td>0.403012</td>
      <td>0.576544</td>
      <td>-0.385594</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.837114</td>
      <td>-1.330702</td>
      <td>-1.678282</td>
      <td>-0.472006</td>
    </tr>
  </tbody>
</table>
</div>



<br><br>

## Grouping
---
By "group by" we are referring to a process involving one or more of the following steps
- **Splitting** the data into groups based on some criteria
- **Applying** a function to each group independently
- **Combining** the results into a data structure

See the [Grouping Section](https://pandas.pydata.org/pandas-docs/stable/groupby.html#groupby "Group By: split-apply-combine")


```python
df = pd.DataFrame({'A' : ['foo', 'bar', 'foo', 'bar', 'foo', 'bar', 'foo', 'foo'],
                   'B' : ['one', 'one', 'two', 'three', 'two', 'two', 'one', 'three'],
                   'C' : np.random.randn(8),
                   'D' : np.random.randn(8)})
```


```python
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>one</td>
      <td>-0.246428</td>
      <td>0.641967</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>one</td>
      <td>-1.281053</td>
      <td>0.842393</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>two</td>
      <td>1.025707</td>
      <td>1.471538</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bar</td>
      <td>three</td>
      <td>-2.276049</td>
      <td>0.271163</td>
    </tr>
    <tr>
      <th>4</th>
      <td>foo</td>
      <td>two</td>
      <td>-0.324559</td>
      <td>-0.548972</td>
    </tr>
    <tr>
      <th>5</th>
      <td>bar</td>
      <td>two</td>
      <td>0.504407</td>
      <td>0.236265</td>
    </tr>
    <tr>
      <th>6</th>
      <td>foo</td>
      <td>one</td>
      <td>1.075662</td>
      <td>0.407394</td>
    </tr>
    <tr>
      <th>7</th>
      <td>foo</td>
      <td>three</td>
      <td>-0.369910</td>
      <td>-0.270197</td>
    </tr>
  </tbody>
</table>
</div>



Grouping and then applying a function **`sum`** to the resulting groups.


```python
df.groupby('A').sum()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>bar</th>
      <td>-3.052695</td>
      <td>1.349822</td>
    </tr>
    <tr>
      <th>foo</th>
      <td>1.160472</td>
      <td>1.701730</td>
    </tr>
  </tbody>
</table>
</div>



Grouping by multiple columns forms a hierarchical index, which we then apply the function.


```python
df.groupby(['A', 'B']).sum()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">bar</th>
      <th>one</th>
      <td>-1.281053</td>
      <td>0.842393</td>
    </tr>
    <tr>
      <th>three</th>
      <td>-2.276049</td>
      <td>0.271163</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.504407</td>
      <td>0.236265</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">foo</th>
      <th>one</th>
      <td>0.829234</td>
      <td>1.049362</td>
    </tr>
    <tr>
      <th>three</th>
      <td>-0.369910</td>
      <td>-0.270197</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.701148</td>
      <td>0.922566</td>
    </tr>
  </tbody>
</table>
</div>



<br><br>

## Reshaping
---
See the sections on [Hierarchical Indexing](https://pandas.pydata.org/pandas-docs/stable/advanced.html#advanced-hierarchical "Hierarchical indexing (MultiIndex)") and [Reshaping](https://pandas.pydata.org/pandas-docs/stable/reshaping.html#reshaping-stacking "Reshaping by stacking and unstacking").

### Stack


```python
tuples = list(zip(*[['bar', 'bar', 'baz', 'baz',
                     'foo', 'foo', 'qux', 'qux'],
                    ['one', 'two', 'one', 'two',
                     'one', 'two', 'one', 'two']]))
```


```python
tuples
```




    [('bar', 'one'),
     ('bar', 'two'),
     ('baz', 'one'),
     ('baz', 'two'),
     ('foo', 'one'),
     ('foo', 'two'),
     ('qux', 'one'),
     ('qux', 'two')]




```python
index = pd.MultiIndex.from_tuples(tuples, names = ['first', 'second'])
```


```python
index
```




    MultiIndex(levels=[[u'bar', u'baz', u'foo', u'qux'], [u'one', u'two']],
               labels=[[0, 0, 1, 1, 2, 2, 3, 3], [0, 1, 0, 1, 0, 1, 0, 1]],
               names=[u'first', u'second'])




```python
df = pd.DataFrame(np.random.randn(8, 2), index = index, columns = ['A', 'B'])
```


```python
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>1.179286</td>
      <td>-0.524009</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.365006</td>
      <td>1.421423</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>-1.435253</td>
      <td>-1.157835</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.387341</td>
      <td>-1.714900</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">foo</th>
      <th>one</th>
      <td>-0.049550</td>
      <td>1.018840</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-0.433423</td>
      <td>0.896300</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">qux</th>
      <th>one</th>
      <td>-0.653060</td>
      <td>1.509228</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-1.720006</td>
      <td>1.315937</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = df[: 4]
```


```python
df2
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>1.179286</td>
      <td>-0.524009</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.365006</td>
      <td>1.421423</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>-1.435253</td>
      <td>-1.157835</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.387341</td>
      <td>-1.714900</td>
    </tr>
  </tbody>
</table>
</div>



The **`stack`** method "compresses" a level in the the DataFrame's columns.


```python
stacked = df2.stack()
```


```python
stacked
```




    first  second   
    bar    one     A    1.179286
                   B   -0.524009
           two     A    0.365006
                   B    1.421423
    baz    one     A   -1.435253
                   B   -1.157835
           two     A    0.387341
                   B   -1.714900
    dtype: float64



With a "stacked" DataFrame or Series (having a `MultiIndex` as the `index`), the inverse operation of **`stack()`** is **`unstack()`**, which by default unstacks the **last level**:


```python
stacked.unstack()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>1.179286</td>
      <td>-0.524009</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.365006</td>
      <td>1.421423</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>-1.435253</td>
      <td>-1.157835</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.387341</td>
      <td>-1.714900</td>
    </tr>
  </tbody>
</table>
</div>




```python
stacked.unstack(2)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>1.179286</td>
      <td>-0.524009</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.365006</td>
      <td>1.421423</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>-1.435253</td>
      <td>-1.157835</td>
    </tr>
    <tr>
      <th>two</th>
      <td>0.387341</td>
      <td>-1.714900</td>
    </tr>
  </tbody>
</table>
</div>




```python
stacked.unstack(1)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>second</th>
      <th>one</th>
      <th>two</th>
    </tr>
    <tr>
      <th>first</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>A</th>
      <td>1.179286</td>
      <td>0.365006</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.524009</td>
      <td>1.421423</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>A</th>
      <td>-1.435253</td>
      <td>0.387341</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-1.157835</td>
      <td>-1.714900</td>
    </tr>
  </tbody>
</table>
</div>




```python
stacked.unstack(0)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>first</th>
      <th>bar</th>
      <th>baz</th>
    </tr>
    <tr>
      <th>second</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">one</th>
      <th>A</th>
      <td>1.179286</td>
      <td>-1.435253</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.524009</td>
      <td>-1.157835</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">two</th>
      <th>A</th>
      <td>0.365006</td>
      <td>0.387341</td>
    </tr>
    <tr>
      <th>B</th>
      <td>1.421423</td>
      <td>-1.714900</td>
    </tr>
  </tbody>
</table>
</div>



### Pivot Tables

See the section on [Pivot Tables](https://pandas.pydata.org/pandas-docs/stable/reshaping.html#reshaping-pivot "Pivot tables").


```python
df = pd.DataFrame({'A' : ['one', 'one', 'two', 'three'] * 3,
                   'B' : ['A', 'B', 'C'] * 4,
                   'C' : ['foo', 'foo', 'foo', 'bar', 'bar', 'bar'] * 2,
                   'D' : np.random.randn(12),
                   'E' : np.random.randn(12)})
```


```python
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>one</td>
      <td>A</td>
      <td>foo</td>
      <td>0.420749</td>
      <td>0.268579</td>
    </tr>
    <tr>
      <th>1</th>
      <td>one</td>
      <td>B</td>
      <td>foo</td>
      <td>-0.357331</td>
      <td>-1.005766</td>
    </tr>
    <tr>
      <th>2</th>
      <td>two</td>
      <td>C</td>
      <td>foo</td>
      <td>1.465894</td>
      <td>-0.106632</td>
    </tr>
    <tr>
      <th>3</th>
      <td>three</td>
      <td>A</td>
      <td>bar</td>
      <td>-0.252910</td>
      <td>-0.985129</td>
    </tr>
    <tr>
      <th>4</th>
      <td>one</td>
      <td>B</td>
      <td>bar</td>
      <td>1.505958</td>
      <td>0.927334</td>
    </tr>
    <tr>
      <th>5</th>
      <td>one</td>
      <td>C</td>
      <td>bar</td>
      <td>0.326996</td>
      <td>0.759087</td>
    </tr>
    <tr>
      <th>6</th>
      <td>two</td>
      <td>A</td>
      <td>foo</td>
      <td>-0.929285</td>
      <td>-0.123798</td>
    </tr>
    <tr>
      <th>7</th>
      <td>three</td>
      <td>B</td>
      <td>foo</td>
      <td>-0.139210</td>
      <td>-0.097484</td>
    </tr>
    <tr>
      <th>8</th>
      <td>one</td>
      <td>C</td>
      <td>foo</td>
      <td>-0.414775</td>
      <td>0.324731</td>
    </tr>
    <tr>
      <th>9</th>
      <td>one</td>
      <td>A</td>
      <td>bar</td>
      <td>-0.326252</td>
      <td>-1.870384</td>
    </tr>
    <tr>
      <th>10</th>
      <td>two</td>
      <td>B</td>
      <td>bar</td>
      <td>1.517495</td>
      <td>-0.134392</td>
    </tr>
    <tr>
      <th>11</th>
      <td>three</td>
      <td>C</td>
      <td>bar</td>
      <td>-2.068089</td>
      <td>-0.505142</td>
    </tr>
  </tbody>
</table>
</div>



We can produce pivot tables from this data very easily:


```python
pd.pivot_table(df, values = 'D', index = ['A', 'B'], columns = ['C'])
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
      <th>bar</th>
      <th>foo</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">one</th>
      <th>A</th>
      <td>-0.326252</td>
      <td>0.420749</td>
    </tr>
    <tr>
      <th>B</th>
      <td>1.505958</td>
      <td>-0.357331</td>
    </tr>
    <tr>
      <th>C</th>
      <td>0.326996</td>
      <td>-0.414775</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">three</th>
      <th>A</th>
      <td>-0.252910</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>B</th>
      <td>NaN</td>
      <td>-0.139210</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-2.068089</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">two</th>
      <th>A</th>
      <td>NaN</td>
      <td>-0.929285</td>
    </tr>
    <tr>
      <th>B</th>
      <td>1.517495</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>C</th>
      <td>NaN</td>
      <td>1.465894</td>
    </tr>
  </tbody>
</table>
</div>



<br><br>

## Time Series
---

pandas has simple, powerful, and efficient functionality for performing resampling operations during frequency conversion (e.g., converting secondly data into 5-minutely data). This is extremely common in, but not limited to, financial applications. See the [Time Series section](https://pandas.pydata.org/pandas-docs/stable/timeseries.html#timeseries "Time Series / Date functionality").


```python
rng = pd.date_range('1/1/2012', periods = 100, freq = 'S')
```


```python
ts = pd.Series(np.random.randint(0, 500, len(rng)), index = rng)
```


```python
ts.resample('5Min').sum()
```




    2012-01-01    28003
    Freq: 5T, dtype: int64



Time zone representation


```python
rng = pd.date_range('3/6/2012 00:00', periods = 5, freq = 'D')
```


```python
rng
```




    DatetimeIndex(['2012-03-06', '2012-03-07', '2012-03-08', '2012-03-09',
                   '2012-03-10'],
                  dtype='datetime64[ns]', freq='D')




```python
ts = pd.Series(np.random.randn(len(rng)), rng)
```


```python
ts
```




    2012-03-06    0.196634
    2012-03-07   -0.170732
    2012-03-08   -0.914972
    2012-03-09   -0.652561
    2012-03-10   -0.713764
    Freq: D, dtype: float64




```python
ts_utc = ts.tz_localize('UTC')
```


```python
ts_utc
```




    2012-03-06 00:00:00+00:00    0.196634
    2012-03-07 00:00:00+00:00   -0.170732
    2012-03-08 00:00:00+00:00   -0.914972
    2012-03-09 00:00:00+00:00   -0.652561
    2012-03-10 00:00:00+00:00   -0.713764
    Freq: D, dtype: float64



Convert to another time zone.


```python
ts_utc.tz_convert('US/Eastern')
```




    2012-03-05 19:00:00-05:00    0.196634
    2012-03-06 19:00:00-05:00   -0.170732
    2012-03-07 19:00:00-05:00   -0.914972
    2012-03-08 19:00:00-05:00   -0.652561
    2012-03-09 19:00:00-05:00   -0.713764
    Freq: D, dtype: float64



Converting between time span representations.


```python
rng = pd.date_range('1/1/2012', periods = 5, freq = 'M')
```


```python
rng
```




    DatetimeIndex(['2012-01-31', '2012-02-29', '2012-03-31', '2012-04-30',
                   '2012-05-31'],
                  dtype='datetime64[ns]', freq='M')




```python
ts = pd.Series(np.random.randn(len(rng)), index = rng)
```


```python
ts
```




    2012-01-31   -0.480761
    2012-02-29   -0.423017
    2012-03-31   -1.993730
    2012-04-30    0.142594
    2012-05-31    1.304180
    Freq: M, dtype: float64




```python
ps = ts.to_period()
```


```python
ps
```




    2012-01   -0.480761
    2012-02   -0.423017
    2012-03   -1.993730
    2012-04    0.142594
    2012-05    1.304180
    Freq: M, dtype: float64




```python
ps.to_timestamp()
```




    2012-01-01   -0.480761
    2012-02-01   -0.423017
    2012-03-01   -1.993730
    2012-04-01    0.142594
    2012-05-01    1.304180
    Freq: MS, dtype: float64



Converting between period and timestamp enables some convenient arithmetic functions to be used.<br>
In the following example, we convert a quarterly frequency with year ending in November to 9am of the end of the month following the quarter end:


```python
prng = pd.period_range('1990Q1', '2000Q4', freq='Q-NOV')
```


```python
prng
```




    PeriodIndex(['1990Q1', '1990Q2', '1990Q3', '1990Q4', '1991Q1', '1991Q2',
                 '1991Q3', '1991Q4', '1992Q1', '1992Q2', '1992Q3', '1992Q4',
                 '1993Q1', '1993Q2', '1993Q3', '1993Q4', '1994Q1', '1994Q2',
                 '1994Q3', '1994Q4', '1995Q1', '1995Q2', '1995Q3', '1995Q4',
                 '1996Q1', '1996Q2', '1996Q3', '1996Q4', '1997Q1', '1997Q2',
                 '1997Q3', '1997Q4', '1998Q1', '1998Q2', '1998Q3', '1998Q4',
                 '1999Q1', '1999Q2', '1999Q3', '1999Q4', '2000Q1', '2000Q2',
                 '2000Q3', '2000Q4'],
                dtype='period[Q-NOV]', freq='Q-NOV')




```python
ts = pd.Series(np.random.randn(len(prng)), prng)
```


```python
ts.head(3)
```




    1990Q1   -1.145494
    1990Q2   -0.776468
    1990Q3   -0.598847
    Freq: Q-NOV, dtype: float64




```python
ts.index = (prng.asfreq('M', 'e') + 1).asfreq('H', 's') + 9
```


```python
ts.head()
```




    1990-03-01 09:00   -1.145494
    1990-06-01 09:00   -0.776468
    1990-09-01 09:00   -0.598847
    1990-12-01 09:00    0.005923
    1991-03-01 09:00   -1.044754
    Freq: H, dtype: float64



<br><br>

## Categoricals

Since version 0.15, pandas can include categorical data in a `DataFrame`. For full docs, see the [categorical introduction](https://pandas.pydata.org/pandas-docs/stable/categorical.html#categorical "Categorical Data") and the [API documentation](https://pandas.pydata.org/pandas-docs/stable/api.html#api-categorical "Categorical API").


```python
df = pd.DataFrame({"id":[1, 2, 3, 4, 5, 6], "raw_grade":['a', 'b', 'b', 'a', 'a', 'e']})
```

Convert the raw grades to a categorical data type using **`.astype()`**.


```python
df["grade"] = df["raw_grade"].astype("category")
```


```python
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>raw_grade</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>a</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>b</td>
      <td>b</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
      <td>a</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>a</td>
      <td>a</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
      <td>e</td>
    </tr>
  </tbody>
</table>
</div>




```python
df["raw_grade"]
```




    0    a
    1    b
    2    b
    3    a
    4    a
    5    e
    Name: raw_grade, dtype: object




```python
df["grade"]
```




    0    a
    1    b
    2    b
    3    a
    4    a
    5    e
    Name: grade, dtype: category
    Categories (3, object): [a, b, e]



Rename the categories to more meaningful names (assigning to **`Series.cat.categories`** is **inplace**!)


```python
df["grade"].cat.categories = ["very good", "good", "very bad"]
```


```python
df["grade"]
```




    0    very good
    1         good
    2         good
    3    very good
    4    very good
    5     very bad
    Name: grade, dtype: category
    Categories (3, object): [very good, good, very bad]



Reorder the categories and simultaneously add the missing categories (methods under **`Series .cat`** return a new `Series` per default).


```python
df["grade"] = df["grade"].cat.set_categories(["very bad", "bad", "medium", "good", "very good"])
```


```python
df["grade"]
```




    0    very good
    1         good
    2         good
    3    very good
    4    very good
    5     very bad
    Name: grade, dtype: category
    Categories (5, object): [very bad, bad, medium, good, very good]



**Sorting is per order in the categories, not lexical order.**


```python
df.sort_values(by = "grade")
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>raw_grade</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
      <td>very bad</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>b</td>
      <td>good</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
      <td>very good</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>a</td>
      <td>very good</td>
    </tr>
  </tbody>
</table>
</div>



Grouping by a categorical column shows also empty categories.


```python
df.groupby("grade").size()
```




    grade
    very bad     1
    bad          0
    medium       0
    good         2
    very good    3
    dtype: int64



<br><br>

## Plotting
---
See the [Plotting docs](https://pandas.pydata.org/pandas-docs/stable/visualization.html#visualization "Visualization").


```python
ts = pd.Series(np.random.randn(1000), index = pd.date_range('1/1/2000', periods = 1000))
```


```python
ts = ts.cumsum()
```


```python
ts.plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7fa138994e10>



![image](https://pandas.pydata.org/pandas-docs/stable/_images/series_plot_basic.png)

On DataFrame, **`plot()`** is a convenience to plot all of the columns with labels:


```python
df = pd.DataFrame(np.random.randn(1000, 4), index = ts.index, columns = ['A', 'B', 'C', 'D'])
```


```python
df = df.cumsum()
```


```python
plt.figure();
df.plot();
plt.legend(loc = 'best')
```




    <matplotlib.legend.Legend at 0x7fa13552ead0>



![image](https://pandas.pydata.org/pandas-docs/stable/_images/frame_plot_basic.png)

<br><br>

## Getting Data In/Out
---
### CSV
[Writing to a csv file](https://pandas.pydata.org/pandas-docs/stable/io.html#io-store-in-csv "Writing to CSV format")


```python
df.to_csv('foo.csv')
```

[Reading from a csv file](https://pandas.pydata.org/pandas-docs/stable/io.html#io-read-csv-table "Reading from a csv file")


```python
pd.read_csv('foo.csv').head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000-01-01</td>
      <td>-0.128407</td>
      <td>1.053644</td>
      <td>0.762004</td>
      <td>-0.838496</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000-01-02</td>
      <td>-0.694843</td>
      <td>-1.405031</td>
      <td>2.776359</td>
      <td>0.947008</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000-01-03</td>
      <td>1.864596</td>
      <td>-0.520070</td>
      <td>3.235581</td>
      <td>1.903378</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000-01-04</td>
      <td>2.625047</td>
      <td>-0.232371</td>
      <td>2.332271</td>
      <td>1.067805</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000-01-05</td>
      <td>3.835167</td>
      <td>0.466320</td>
      <td>1.088676</td>
      <td>2.083621</td>
    </tr>
  </tbody>
</table>
</div>



### HDF5
Reading and writing to [HDFStores](https://pandas.pydata.org/pandas-docs/stable/io.html#io-hdf5 "HDF5 (PyTables)").

Writing to a HDF5 Store.


```python
df.to_hdf('foo.h5', 'df')
```

Reading from a HDF5 Store.


```python
pd.read_hdf('foo.h5','df').head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-01</th>
      <td>-0.128407</td>
      <td>1.053644</td>
      <td>0.762004</td>
      <td>-0.838496</td>
    </tr>
    <tr>
      <th>2000-01-02</th>
      <td>-0.694843</td>
      <td>-1.405031</td>
      <td>2.776359</td>
      <td>0.947008</td>
    </tr>
    <tr>
      <th>2000-01-03</th>
      <td>1.864596</td>
      <td>-0.520070</td>
      <td>3.235581</td>
      <td>1.903378</td>
    </tr>
    <tr>
      <th>2000-01-04</th>
      <td>2.625047</td>
      <td>-0.232371</td>
      <td>2.332271</td>
      <td>1.067805</td>
    </tr>
    <tr>
      <th>2000-01-05</th>
      <td>3.835167</td>
      <td>0.466320</td>
      <td>1.088676</td>
      <td>2.083621</td>
    </tr>
  </tbody>
</table>
</div>



### Excel
Reading and writing to [MS Excel](https://pandas.pydata.org/pandas-docs/stable/io.html#io-excel "Excel files").

Writing to an excel file.


```python
df.to_excel('foo.xlsx', sheet_name='Sheet1')
```

Reading from an excel file.


```python
pd.read_excel('foo.xlsx', 'Sheet1', index_col=None, na_values=['NA']).head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-01</th>
      <td>-0.128407</td>
      <td>1.053644</td>
      <td>0.762004</td>
      <td>-0.838496</td>
    </tr>
    <tr>
      <th>2000-01-02</th>
      <td>-0.694843</td>
      <td>-1.405031</td>
      <td>2.776359</td>
      <td>0.947008</td>
    </tr>
    <tr>
      <th>2000-01-03</th>
      <td>1.864596</td>
      <td>-0.520070</td>
      <td>3.235581</td>
      <td>1.903378</td>
    </tr>
    <tr>
      <th>2000-01-04</th>
      <td>2.625047</td>
      <td>-0.232371</td>
      <td>2.332271</td>
      <td>1.067805</td>
    </tr>
    <tr>
      <th>2000-01-05</th>
      <td>3.835167</td>
      <td>0.466320</td>
      <td>1.088676</td>
      <td>2.083621</td>
    </tr>
  </tbody>
</table>
</div>



<br><br>

## Gotchas
---
If you are trying an operation and you see an exception like:


```python
if pd.Series([False, True, False]):
    print("I was true")
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-156-9cae3ab0f79f> in <module>()
    ----> 1 if pd.Series([False, True, False]):
          2     print("I was true")


    /home/frank/anaconda3/envs/py2/lib/python2.7/site-packages/pandas/core/generic.pyc in __nonzero__(self)
        951         raise ValueError("The truth value of a {0} is ambiguous. "
        952                          "Use a.empty, a.bool(), a.item(), a.any() or a.all()."
    --> 953                          .format(self.__class__.__name__))
        954
        955     __bool__ = __nonzero__


    ValueError: The truth value of a Series is ambiguous. Use a.empty, a.bool(), a.item(), a.any() or a.all().


See [Comparisons](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics-compare "Flexible Comparisons") for an explanation and what to do.

See [Gotchas](https://pandas.pydata.org/pandas-docs/stable/gotchas.html#gotchas "Frequently Asked Questions (FAQ)") as well.
