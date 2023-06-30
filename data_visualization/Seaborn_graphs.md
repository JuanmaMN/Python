-- Note: This code has been run on Posit (previously known as R Studio). I saved the "NBA team data" file in the working directory.


##  Import packages    

```
import pandas as pd
import numpy as np
import matplotlib.pylab as plt
import seaborn as sns

```


##  Import dataset

```
healthexp= sns.load_dataset('healthexp')
healthexp.head()

```


## Lineplot


```
healthexp_two = healthexp.loc[
  (healthexp.Country == 'Canada') | (healthexp.Country == 'USA'),
  :
]

sns.lineplot(data=healthexp_two, x="Year", y="Spending_USD", hue="Country")
plt.show()

```

<img width="596" alt="lineplot" src="https://github.com/JuanmaMN/Python/assets/37122520/91086aa7-0905-416a-b5a8-f80c857ff0ff">
