```python
import pandas as pd
counts = pd.Series([632, 1638, 456, 112])
print(counts)
```

    0     632
    1    1638
    2     456
    3     112
    dtype: int64
    


```python
counts.values
```




    array([ 632, 1638,  456,  112], dtype=int64)




```python
counts.index
```




    RangeIndex(start=0, stop=4, step=1)




```python
bacteria = pd.Series([632, 1638, 569, 115], index=['Firmicutes', 'Proteobacteria', 'Actinobacteria', 'Bacteroidetes'])
print(bacteria)
```

    Firmicutes         632
    Proteobacteria    1638
    Actinobacteria     569
    Bacteroidetes      115
    dtype: int64
    


```python
bacteria['Actinobacteria']
```




    569




```python
bacteria[bacteria.index.str.endswith('bacteria')]
```




    Proteobacteria    1638
    Actinobacteria     569
    dtype: int64




```python
'Bacteroidetes' in bacteria
```




    True




```python
bacteria[0]
```




    632




```python
bacteria.name = 'counts'
bacteria.index.name = 'phylum'
print(bacteria)
```

    phylum
    Firmicutes         632
    Proteobacteria    1638
    Actinobacteria     569
    Bacteroidetes      115
    Name: counts, dtype: int64
    


```python
import numpy as np
np.log(bacteria)
```




    phylum
    Firmicutes        6.448889
    Proteobacteria    7.401231
    Actinobacteria    6.343880
    Bacteroidetes     4.744932
    Name: counts, dtype: float64




```python
bacteria[bacteria > 1000]
```




    phylum
    Proteobacteria    1638
    Name: counts, dtype: int64




```python
bacteria_dict = {'Firmicutes': 632, 'Proteobacteria': 1632, 'Actinobacteria': 569, 'Bacteroidetes': 115}
```


```python
bact = pd.Series(bacteria_dict)
print(bact)
```

    Firmicutes         632
    Proteobacteria    1632
    Actinobacteria     569
    Bacteroidetes      115
    dtype: int64
    


```python
bacteria2 = pd.Series(bacteria_dict, index=['Cyanobacteria', 'Firmicutes', 'Proteobacteria', 'Actinobacteria'])
print(bacteria2)
```

    Cyanobacteria        NaN
    Firmicutes         632.0
    Proteobacteria    1632.0
    Actinobacteria     569.0
    dtype: float64
    


```python
bacteria2.isnull()
```




    Cyanobacteria      True
    Firmicutes        False
    Proteobacteria    False
    Actinobacteria    False
    dtype: bool




```python
bacteria + bacteria2
```




    Actinobacteria    1138.0
    Bacteroidetes        NaN
    Cyanobacteria        NaN
    Firmicutes        1264.0
    Proteobacteria    3270.0
    dtype: float64




```python
bacteria_data = pd.DataFrame({'value': [632, 1638, 569, 115, 433, 1130, 754, 555],
                             'patient': [1, 1, 1, 1, 2, 2, 2, 2],
                             'phylum': ['Firmicutes', 'Proteobacteria', 'Actinobacteria', 'Bacteroidetes', 'Firmicutes', 'Proteobacteria', 'Actinobacteria', 'Bacteroidetes']})
bacteria_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>value</th>
      <th>patient</th>
      <th>phylum</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>632</td>
      <td>1</td>
      <td>Firmicutes</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1638</td>
      <td>1</td>
      <td>Proteobacteria</td>
    </tr>
    <tr>
      <th>2</th>
      <td>569</td>
      <td>1</td>
      <td>Actinobacteria</td>
    </tr>
    <tr>
      <th>3</th>
      <td>115</td>
      <td>1</td>
      <td>Bacteroidetes</td>
    </tr>
    <tr>
      <th>4</th>
      <td>433</td>
      <td>2</td>
      <td>Firmicutes</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1130</td>
      <td>2</td>
      <td>Proteobacteria</td>
    </tr>
    <tr>
      <th>6</th>
      <td>754</td>
      <td>2</td>
      <td>Actinobacteria</td>
    </tr>
    <tr>
      <th>7</th>
      <td>555</td>
      <td>2</td>
      <td>Bacteroidetes</td>
    </tr>
  </tbody>
</table>
</div>




```python
bacteria_data[['phylum', 'value', 'patient']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>phylum</th>
      <th>value</th>
      <th>patient</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Firmicutes</td>
      <td>632</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Proteobacteria</td>
      <td>1638</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Actinobacteria</td>
      <td>569</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bacteroidetes</td>
      <td>115</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Firmicutes</td>
      <td>433</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Proteobacteria</td>
      <td>1130</td>
      <td>2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Actinobacteria</td>
      <td>754</td>
      <td>2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bacteroidetes</td>
      <td>555</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
bacteria_data.columns
```




    Index(['value', 'patient', 'phylum'], dtype='object')




```python
bacteria_data['value']
```




    0     632
    1    1638
    2     569
    3     115
    4     433
    5    1130
    6     754
    7     555
    Name: value, dtype: int64




```python
type(bacteria_data['value'])
```




    pandas.core.series.Series




```python
bacteria_data[['value']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>632</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1638</td>
    </tr>
    <tr>
      <th>2</th>
      <td>569</td>
    </tr>
    <tr>
      <th>3</th>
      <td>115</td>
    </tr>
    <tr>
      <th>4</th>
      <td>433</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1130</td>
    </tr>
    <tr>
      <th>6</th>
      <td>754</td>
    </tr>
    <tr>
      <th>7</th>
      <td>555</td>
    </tr>
  </tbody>
</table>
</div>




```python
bacteria_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>value</th>
      <th>patient</th>
      <th>phylum</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>632</td>
      <td>1</td>
      <td>Firmicutes</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1638</td>
      <td>1</td>
      <td>Proteobacteria</td>
    </tr>
    <tr>
      <th>2</th>
      <td>569</td>
      <td>1</td>
      <td>Actinobacteria</td>
    </tr>
    <tr>
      <th>3</th>
      <td>115</td>
      <td>1</td>
      <td>Bacteroidetes</td>
    </tr>
    <tr>
      <th>4</th>
      <td>433</td>
      <td>2</td>
      <td>Firmicutes</td>
    </tr>
  </tbody>
</table>
</div>




```python
bacteria_data.tail(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>value</th>
      <th>patient</th>
      <th>phylum</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <td>1130</td>
      <td>2</td>
      <td>Proteobacteria</td>
    </tr>
    <tr>
      <th>6</th>
      <td>754</td>
      <td>2</td>
      <td>Actinobacteria</td>
    </tr>
    <tr>
      <th>7</th>
      <td>555</td>
      <td>2</td>
      <td>Bacteroidetes</td>
    </tr>
  </tbody>
</table>
</div>




```python
bacteria_data.shape
```




    (8, 3)




```python
bacteria_data = pd.DataFrame([{'patient': 1, 'phylum': 'Firmicutes', 'value': 632},
{'patient': 1, 'phylum': 'Proteobacteria', 'value': 1638},
{'patient': 1, 'phylum': 'Actinobacteria', 'value': 569},
{'patient': 1, 'phylum': 'Bacteroidetes', 'value': 115},
{'patient': 2, 'phylum': 'Firmicutes', 'value': 6433},
{'patient': 2, 'phylum': 'Proteobacteria', 'value': 1130},
{'patient': 2, 'phylum': 'Actinobacteria', 'value': 754},
{'patient': 2, 'phylum': 'Bacteroidetes', 'value': 555}])
bacteria_data


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>patient</th>
      <th>phylum</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Firmicutes</td>
      <td>632</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Proteobacteria</td>
      <td>1638</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Actinobacteria</td>
      <td>569</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Bacteroidetes</td>
      <td>115</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>Firmicutes</td>
      <td>6433</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>Proteobacteria</td>
      <td>1130</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>Actinobacteria</td>
      <td>754</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>Bacteroidetes</td>
      <td>555</td>
    </tr>
  </tbody>
</table>
</div>




```python
vals = bacteria_data.value
vals
```




    0     632
    1    1638
    2     569
    3     115
    4    6433
    5    1130
    6     754
    7     555
    Name: value, dtype: int64




```python
vals[5] = 0
```

    C:\Users\JON\AppData\Local\Temp/ipykernel_10164/2794464284.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      vals[5] = 0
    


```python
bacteria_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>patient</th>
      <th>phylum</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Firmicutes</td>
      <td>632</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Proteobacteria</td>
      <td>1638</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Actinobacteria</td>
      <td>569</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Bacteroidetes</td>
      <td>115</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>Firmicutes</td>
      <td>6433</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>Proteobacteria</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>Actinobacteria</td>
      <td>754</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>Bacteroidetes</td>
      <td>555</td>
    </tr>
  </tbody>
</table>
</div>




```python
bacteria_data.value[5] = 1130
```

    C:\Users\JON\AppData\Local\Temp/ipykernel_10164/2034502601.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      bacteria_data.value[5] = 1130
    


```python
bacteria_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>patient</th>
      <th>phylum</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Firmicutes</td>
      <td>632</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Proteobacteria</td>
      <td>1638</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Actinobacteria</td>
      <td>569</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Bacteroidetes</td>
      <td>115</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>Firmicutes</td>
      <td>6433</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>Proteobacteria</td>
      <td>1130</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>Actinobacteria</td>
      <td>754</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>Bacteroidetes</td>
      <td>555</td>
    </tr>
  </tbody>
</table>
</div>




```python
bacteria_data['year'] = 2013
bacteria_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>patient</th>
      <th>phylum</th>
      <th>value</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Firmicutes</td>
      <td>632</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Proteobacteria</td>
      <td>1638</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Actinobacteria</td>
      <td>569</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Bacteroidetes</td>
      <td>115</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>Firmicutes</td>
      <td>6433</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>Proteobacteria</td>
      <td>1130</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>Actinobacteria</td>
      <td>754</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>Bacteroidetes</td>
      <td>555</td>
      <td>2013</td>
    </tr>
  </tbody>
</table>
</div>




```python
bacteria_data.phylum
```




    0        Firmicutes
    1    Proteobacteria
    2    Actinobacteria
    3     Bacteroidetes
    4        Firmicutes
    5    Proteobacteria
    6    Actinobacteria
    7     Bacteroidetes
    Name: phylum, dtype: object




```python
treatment = pd.Series([0]*4 + [1] * 2)
treatment
```




    0    0
    1    0
    2    0
    3    0
    4    1
    5    1
    dtype: int64




```python
bacteria_data['treatment'] = treatment
bacteria_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>patient</th>
      <th>phylum</th>
      <th>value</th>
      <th>year</th>
      <th>treatment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Firmicutes</td>
      <td>632</td>
      <td>2013</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Proteobacteria</td>
      <td>1638</td>
      <td>2013</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Actinobacteria</td>
      <td>569</td>
      <td>2013</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Bacteroidetes</td>
      <td>115</td>
      <td>2013</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>Firmicutes</td>
      <td>6433</td>
      <td>2013</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>Proteobacteria</td>
      <td>1130</td>
      <td>2013</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>Actinobacteria</td>
      <td>754</td>
      <td>2013</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>Bacteroidetes</td>
      <td>555</td>
      <td>2013</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
bacteria_data.values
```




    array([[1, 'Firmicutes', 632, 2013, 0.0],
           [1, 'Proteobacteria', 1638, 2013, 0.0],
           [1, 'Actinobacteria', 569, 2013, 0.0],
           [1, 'Bacteroidetes', 115, 2013, 0.0],
           [2, 'Firmicutes', 6433, 2013, 1.0],
           [2, 'Proteobacteria', 1130, 2013, 1.0],
           [2, 'Actinobacteria', 754, 2013, nan],
           [2, 'Bacteroidetes', 555, 2013, nan]], dtype=object)




```python
df = pd.DataFrame({'foo': [1,2,3], 'bar': [0.4, -1.0, 4.5]})
df.values, df.values.dtype
```




    (array([[ 1. ,  0.4],
            [ 2. , -1. ],
            [ 3. ,  4.5]]),
     dtype('float64'))




```python
bacteria_data.index[0] = 15
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_10164/950673072.py in <module>
    ----> 1 bacteria_data.index[0] = 15
    

    D:\Programs\Anaconda3\lib\site-packages\pandas\core\indexes\base.py in __setitem__(self, key, value)
       4583     @final
       4584     def __setitem__(self, key, value):
    -> 4585         raise TypeError("Index does not support mutable operations")
       4586 
       4587     def __getitem__(self, key):
    

    TypeError: Index does not support mutable operations



```python
bacteria2.index = bacteria.index
bacteria2
```




    phylum
    Firmicutes           NaN
    Proteobacteria     632.0
    Actinobacteria    1632.0
    Bacteroidetes      569.0
    dtype: float64




```python
medals = pd.read_table('olympics.2018.txt', sep='\t', index_col=0, header=None, names=['country', 'medals', 'population'])
medals.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>medals</th>
      <th>population</th>
    </tr>
    <tr>
      <th>country</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Tonga</th>
      <td>1</td>
      <td>96165</td>
    </tr>
    <tr>
      <th>Bahamas</th>
      <td>1</td>
      <td>281584</td>
    </tr>
    <tr>
      <th>Jamaica</th>
      <td>6</td>
      <td>2589043</td>
    </tr>
    <tr>
      <th>Cuba</th>
      <td>25</td>
      <td>10952046</td>
    </tr>
    <tr>
      <th>Australia</th>
      <td>41</td>
      <td>18348078</td>
    </tr>
  </tbody>
</table>
</div>




```python
oecd_site = 'https://www.oecd.org/about/budget/member-countries-budget-contributions.htm'
```


```python
pd.read_html(oecd_site)
```




    [                                                    0               1
     0   Member Countries' percentage shares of Part I ...             NaN
     1                                    Member Countries  % Contribution
     2                                           AUSTRALIA             3.1
     3                                             AUSTRIA             1.5
     4                                             BELGIUM             1.7
     5                                              CANADA             3.5
     6                                               CHILE             1.2
     7                                      CZECH REPUBLIC             1.1
     8                                             DENMARK             1.4
     9                                             ESTONIA             0.9
     10                                            FINLAND             1.3
     11                                             FRANCE             5.2
     12                                            GERMANY             7.2
     13                                             GREECE             1.1
     14                                            HUNGARY             1.0
     15                                            ICELAND             0.6
     16                                            IRELAND             1.3
     17                                             ISRAEL             1.4
     18                                              ITALY             4.0
     19                                              JAPAN             9.4
     20                                              KOREA             3.3
     21                                             LATVIA             0.9
     22                                          LITHUANIA             0.9
     23                                         LUXEMBOURG             0.8
     24                                             MEXICO             2.7
     25                                        NETHERLANDS             2.2
     26                                        NEW ZEALAND             1.1
     27                                             NORWAY             1.6
     28                                             POLAND             1.6
     29                                           PORTUGAL             1.2
     30                                    SLOVAK REPUBLIC             1.0
     31                                           SLOVENIA             0.9
     32                                              SPAIN             3.0
     33                                             SWEDEN             1.6
     34                                        SWITZERLAND             2.2
     35                                             TURKEY             2.2
     36                                     UNITED KINGDOM             5.4
     37                                      UNITED STATES            20.5
     38                             Total of contributions           100.0]




```python
mb = pd.read_csv('microbiome.csv')
```


```python
pd.read_csv('microbiome.csv', skiprows=[3,4,6]).head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Taxon</th>
      <th>Patient</th>
      <th>Tissue</th>
      <th>Stool</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Firmicutes</td>
      <td>1</td>
      <td>632</td>
      <td>305</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Firmicutes</td>
      <td>2</td>
      <td>136</td>
      <td>4182</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Firmicutes</td>
      <td>5</td>
      <td>831</td>
      <td>8605</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Firmicutes</td>
      <td>7</td>
      <td>718</td>
      <td>717</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Firmicutes</td>
      <td>8</td>
      <td>173</td>
      <td>33</td>
    </tr>
  </tbody>
</table>
</div>




```python
few_recs = pd.read_csv('microbiome.csv', nrows=4)
few_recs
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Taxon</th>
      <th>Patient</th>
      <th>Tissue</th>
      <th>Stool</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Firmicutes</td>
      <td>1</td>
      <td>632</td>
      <td>305</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Firmicutes</td>
      <td>2</td>
      <td>136</td>
      <td>4182</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Firmicutes</td>
      <td>3</td>
      <td>1174</td>
      <td>703</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Firmicutes</td>
      <td>4</td>
      <td>408</td>
      <td>3946</td>
    </tr>
  </tbody>
</table>
</div>




```python
data_chunks = pd.read_csv('microbiome.csv', chunksize=5)
data_chunks
```




    <pandas.io.parsers.readers.TextFileReader at 0x21d12f5f580>




```python
next(data_chunks)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Taxon</th>
      <th>Patient</th>
      <th>Tissue</th>
      <th>Stool</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Firmicutes</td>
      <td>1</td>
      <td>632</td>
      <td>305</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Firmicutes</td>
      <td>2</td>
      <td>136</td>
      <td>4182</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Firmicutes</td>
      <td>3</td>
      <td>1174</td>
      <td>703</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Firmicutes</td>
      <td>4</td>
      <td>408</td>
      <td>3946</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Firmicutes</td>
      <td>5</td>
      <td>831</td>
      <td>8605</td>
    </tr>
  </tbody>
</table>
</div>




```python
mb = pd.read_csv('microbiome.csv', index_col=['Taxon', 'Patient'])
mb.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Tissue</th>
      <th>Stool</th>
    </tr>
    <tr>
      <th>Taxon</th>
      <th>Patient</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Firmicutes</th>
      <th>1</th>
      <td>632</td>
      <td>305</td>
    </tr>
    <tr>
      <th>2</th>
      <td>136</td>
      <td>4182</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1174</td>
      <td>703</td>
    </tr>
    <tr>
      <th>4</th>
      <td>408</td>
      <td>3946</td>
    </tr>
    <tr>
      <th>5</th>
      <td>831</td>
      <td>8605</td>
    </tr>
  </tbody>
</table>
</div>




```python
mb.index
```




    MultiIndex([('Firmicutes',  1),
                ('Firmicutes',  2),
                ('Firmicutes',  3),
                ('Firmicutes',  4),
                ('Firmicutes',  5),
                ('Firmicutes',  6),
                ('Firmicutes',  7),
                ('Firmicutes',  8),
                ('Firmicutes',  9),
                ('Firmicutes', 10)],
               names=['Taxon', 'Patient'])




```python
mb.loc[('Firmicutes', 2)]
```




    Tissue     136
    Stool     4182
    Name: (Firmicutes, 2), dtype: int64




```python
mb.xs(1, level='Patient')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Tissue</th>
      <th>Stool</th>
    </tr>
    <tr>
      <th>Taxon</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Firmicutes</th>
      <td>632</td>
      <td>305</td>
    </tr>
  </tbody>
</table>
</div>




```python
mb.swaplevel('Patient', 'Taxon').head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Tissue</th>
      <th>Stool</th>
    </tr>
    <tr>
      <th>Patient</th>
      <th>Taxon</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <th>Firmicutes</th>
      <td>632</td>
      <td>305</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Firmicutes</th>
      <td>136</td>
      <td>4182</td>
    </tr>
    <tr>
      <th>3</th>
      <th>Firmicutes</th>
      <td>1174</td>
      <td>703</td>
    </tr>
    <tr>
      <th>4</th>
      <th>Firmicutes</th>
      <td>408</td>
      <td>3946</td>
    </tr>
    <tr>
      <th>5</th>
      <th>Firmicutes</th>
      <td>831</td>
      <td>8605</td>
    </tr>
  </tbody>
</table>
</div>



## Jonathan Doolittle


```python

```
