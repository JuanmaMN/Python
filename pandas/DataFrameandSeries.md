
-- Note: This code has been run on Posit (previously known as R Studio).


#  Import  pandas numpy package    

```
import pandas as pd

import numpy as np

```


# Series
   

```
seriesobject = pd.Series([1,5,-2,-3])

seriesobject.values

seriesobject.index

```



##### Creatae a Series with an index identying each data point with a label

```
seriesobject2 = pd.Series([1,5,-2,-3], index=['a','b','c','d'])

seriesobject2.values

seriesobject2.index
```

#### Select a value 

```
seriesobject2[0]

seriesobject2['a']
```

#### Select several value 

```
seriesobject2[0:2]

seriesobject2[['c','b']]
```

#### Change a value

```
seriesobject2['a'] = 15
```

#### Boolean array 

```
seriesobject2[seriesobject2 > 5]
```

#### Multiplication

```
seriesobject2 * 2
```

#### Creatae a Series from a dictionary

```
data= {'col1': 20, 'col2': 25, 'col3': 56, 'col4': 96}

seriesobject3 = pd.Series(data)


```

#### Change the order of the index

```
columns = ['col1','col3', 'col4', 'col2']

seriesobject4 = pd.Series(data, index = columns)

```

# Data Frame


#### Create dataframe

```
data = {
  'team': ['ABC', 'DEF', 'GHI'],
  'year': [2000, 2010, 2020],
  'mark': ['Good', 'Average', 'Very good']
}

dataframe = pd.DataFrame(data)
```



#### The head method selects only the first five rows

```
dataframe.head()
```

##### Arrange columns

```
dataframe = pd.DataFrame(data, columns=['year', 'team','mark'])
```

#### Select one column

```
dataframe.team

dataframe['year']
```

#### Create a column

```
dataframe['newcolumn'] = 'AAA'

dataframe['newcolumnarange']= np.arange(3)

```

#### Delete a column

```
del dataframe['newcolumn']
```

#### Transpose the datafarme

```
dataframe.T
```



## Indexing, Selection, and Filtering


#### Bring the same dataframe

```

data = {
  'team': ['ABC', 'DEF', 'GHI'],
  'year': [2000, 2010, 2020],
  'mark': ['Good', 'Average', 'Very good']
}

data = pd.DataFrame(data, index=['Good', 'Average', 'Very good'])
```

#### Filter the data

```
data['year']                # Select year column
data[['year', 'mark']]      # Select year and mark columns
data[:2]                    # Select first two rows
data[data.mark=='Good']     # Select row when the mark is 'Good'
data[data['year'] == 2000]  # Select row when the year is 2000

```

#### Filter the data with loc and iloc

```
# Select 'Good' mark row and year and mark columns

data.loc[
  data.mark =='Good',
  ['year', 'mark']
]

# Select all rows and year and mark columns

data.loc[
  :,
  ['year','mark']
]

# Select 'Good' mark row and year and mark columns

data.iloc[0,[1,2]]

# Select 'Average' and 'Very good' marks row and all columns

data.iloc[[1,2],[2,0,1]]

```
