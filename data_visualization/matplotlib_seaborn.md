-- Note: This code has been run on Posit (previously known as R Studio). I saved the "NBA team data" file in the working directory.


##  Import packages    

```
import pandas as pd
import numpy as np
import matplotlib.pylab as plt
import seaborn as sns
plt.style.use('ggplot')
pd.set_option('max_columns', 200)
```


## Import dataset      


```
nba = pd.read_excel("NBA_team_data.xlsx")
```

## Visualizations

#### Bar chart    

```
nba_graph = nba[['TEAM','W']] \
            .query('W >= 50') \
            .sort_values('W', ascending=True)
            
nba_graph.plot('TEAM','W', kind='barh',figsize=(4, 2), color='#add8e6')
plt.xlabel('Wins')
plt.title('Number of victories by Team')
plt.show()
```


#### Scatter plot with Matplotlib

```
nba.plot(kind='scatter',
          x = 'W',
          y = 'PTS',
          title = 'Wins vs Points')
plt.show()
```


#### Scatter plot with Seaborn

```
nba_scatter = sns.scatterplot(
            x = 'W',
          y = 'PTS',
          hue = 'L',
          data=nba
)

nba_scatter.set_title('Wins vs. Points')
plt.show()
```

