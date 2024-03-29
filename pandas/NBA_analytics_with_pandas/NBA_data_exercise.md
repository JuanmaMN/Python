-- Note: This code has been run on Posit (previously known as R Studio). I saved the "NBA team data" file in the working directory.


##  Import pandas package    

```
import pandas as pd
```


## Import dataset      


```
nba = pd.read_excel("NBA_team_data.xlsx")
```

## Read the data   


```
nba.columns                            # column labels of the DataFrame

nba.info                               # print a consice summary of a DataFrame

nba.dtypes                             # Return the dtypes in the DataFrame.

nba.select_dtypes(include='float64')   # Return a subset of the DataFrame’s columns based on the column dtypes.

nba.select_dtypes(exclude='float64')   # I have four 'float64' columns (WIN%, FG%, 3P%, FT%) which won't return

nba.values                             # Return a Numpy representation of the DataFrame

nba.ndim                               # Return an int representing the number of axes / array dimensions.

nba.size                               # Return an int representing the number of elements in this object.

nba.shape                              # Return a tuple representing the dimensionality of the DataFrame. (Number of columns, number of rows)

nba.head(5)                            # Return the first 5 rows

nba.tail(5)                            # Return the last 5 rows

nba.describe()                         # Generate descriptive statistics.

nba_copy = nba.copy()                  # Create a copy of the dataframe

nba.pop('W')                           # Return column and drop from dataframe

nba.nlargest(3, 'W')                   # select the top three in Wins

nba.nlargest(3, 'W', keep = 'last')    # select the top three in wins and keep all duplicated items

nba.nlargest(3, ['W', 'PTS'])          # select the top three based on two columns

nba.nsmallest(3, 'W')

nba.nsmallest(3, 'W', keep = 'last')

nba.nsmallest(3, ['W','PTS'])
```

## Data analysis  


#### Add a new column displaying the difference between W and L

```
nba['difference'] = nba['W']-nba['L']
```

#### Create a new column to add up games won and lost

```
nba['Total_games'] = nba.iloc[:,3:5].sum(axis=1) 
```

#### We need to include one more column at the end. I want to add up columns 3 and 4

```
nba['Total'] = nba.iloc[:,3:5].sum(axis=1) 
```

#### Select columns TEAM and GP (games played)

```
nba = nba [['TEAM','GP']]

nba2 = nba[['TEAM']]
```

#### group by one column and sum

```
nba3 = nba.groupby(['Season']).sum()
```

#### group by one column and more operations

```
nba_2 = nba[['TEAM','PTS']]

nba_3 = nba_2.groupby(['TEAM']).sum().sort_values('PTS', ascending = False)

nba_3_one_line=nba[['TEAM','PTS']].groupby(['TEAM']).sum().sort_values('PTS',ascending=False)

nba4 = nba[['TEAM','PTS', 'BLK']].groupby(['TEAM']).sum(['PTS', 'BLK']).sort_values('PTS', ascending=False)
```

#### Total number of points in the season

```
nba[['Season','PTS']].groupby(['Season']).sum('PTS')  
```

#### filter by Miami and Lakers and then group by team and sum points

```
nba_filter_ML = nba[['TEAM', 'PTS']]

nba_filter_ML2= nba_filter_ML.loc[
  (nba.TEAM =='Miami Heat') | (nba.TEAM == 'Los Angeles Lakers'),
  :
]

nba_filter_ML3 = nba_filter_ML2.groupby(['TEAM']).sum('PTS').sort_values('PTS', ascending = False)
```


#### Update a single value using iloc for it

```
nba.iloc[0,28] = 84  # Updata the first value of the last column
```


#### Drop a column

```
nba=nba.drop(columns=['difference'])
```

#### Drop rows

```
nba.isnull().sum(). # number of rows with Null values

nba.dropna(inplace=True)  #drop all rows with NA values
```


#### Sort values

```
nba=nba.sort_values('PTS', ascending = False)

nba=nba.sort_values(by=['W','PTS'], ascending=False)

nba.sort_values(by=['W','PTS'], ascending=False,inplace=True) #inplace can be used as well

nba.sort_values(by=['W','PTS'], ascending = False, na_position = 'first')  # Put NAs first
```

#### Return the top three in wins

```
nba.sort_values('W', ascending = False).head(3)

nba.sort_values('W', ascending = False) \
   .head(3)

```
   
#### Return the lowest three in wins

```
nba.sort_values('W', ascending = True).head(3)

nba.sort_values('W', ascending = True) \
    .head(3)

nba.sort_values('W', ascending = False).tail(3)

nba.sort_values('W', ascending = False) \
    .tail(3)

``` 

#### Group by 

```
nba[['Season','PTS']].groupby(['Season']).sum('PTS')  # Total number of points in the season

nba_filter_ML = nba[['TEAM', 'PTS']]

nba_filter_ML3 = nba_filter_ML2.groupby(['TEAM']).sum('PTS').sort_values('PTS', ascending = False)
```

## Clean data

#### Rename a column

```
nba.rename(columns={"PTS":"Points"})

nba.rename(columns={"TEAM": "team"})
```


#### Renama multiple columns at the same time

```
nba = nba.rename(columns = 
        {"W": "Wins",
        "TEAM": "Team"}
        )
```     
   
#### Replace one value

```
nba=nba.replace('Miami Heat', 'MIA')
```

#### Replace multiple values

```
nba=nba.replace(
                ['Miami Heat', 'Milwaukee Bucks','Boston Celtics'],
                ['MIA', 'MIL', 'BOS']
                )
```

#### Remove duplicates - #It will remove duplicates in W column keeping the last 

```
nba=nba.drop_duplicates(subset=['W'], keep='last')

nba = nba.drop_duplicates(subset=['W','PTS'], keep = 'last') #Drop duplicates in two columns
```

#### Drop columns

```
nba = nba.drop(columns = ['PTS','W'])

nba = nba.drop([0,1]) # drop first two columns
```

#### Drop NA

```
nba.dropna() 

nba.dropna(subset=['W'])
```

#### Check non-missing values

```
nba.notna()
```

#### Check if NA

```
nba.isna()
```

#### Fill the NA with 0

```
nba.fillna(0)
```
  
#### Check notnull

```
nba.notnull()
```

#### Isnull

```
nba.isnull()

nba.isnull().sum(). # number of rows with Null values
```

#### Access a single value for a row/column label pair. Loc can be used as well.

```
nba.at[0,'W'] # It will return the first win 

nba.at[1,'W'] # It will return the second win number 
```

#### Access a single value for a row/column pair by integer position. iloc can be used as well

```
nba.iat[1,1]
```

#### Filter - Subset the dataframe rows or columns according to the specified index labels.

```
nba.filter(['W','PTS']) # Extract two columns

nba.filter(regex='W$', axis=1)   

nba.filter(like='W', axis=1) # Extract columns which contains W in their name - Axis = 1(columns)
```

#### Take  -Return the elements in the given positional indices along an axis 

```
nba.take([0,3]) # Select 0th and 3rd rows
```

#### Query

```
nba.query('W > L') # Find the teams with more victories than losses

nba.query('W == 42') # Find the teams with 42 victories
```

#### Same as above

```
nba.loc[
  (nba.W == 42),
  :
]

nba.query('W >= 42') # Find the teams with 42 or more victories

```

#### Same as above

```
nba.loc[
  (nba.W >= 42),
  :
]
```

#### Select Teams with more than 42 victories and the team name starts by M

```
nba.query('W >= 42 & TEAM.str.startswith("M")') # Find the teams with 42 or more victories
```

#### Select Teams with more than 42 victories and the team names contain M  G L

```
nba.query('W >= 42 & TEAM.str.contains("M|G|L")') # Find the teams with 42 or more victories
```

#### Select Teams with more than 42 victories and the team name ends with T

```
nba.query('W >= 42 & TEAM.str.endswith("t")')
```

#### More to come

