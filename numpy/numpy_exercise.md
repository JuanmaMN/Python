-- Note: This code has been run on Posit (previously known as R Studio).


##  Import numpy package    

```
import numpy as np
```


## The basics: Numpy 1D Arrays
   

```
a = np.array([0,1,2,3,4])  # Numpy 1D arrays
print(a)
```

```

# The attribute size is the number of elements in the array. As there are 5 elements, the result is 5.

a.size 

# The attribute “ndim” represents the number of array dimensions or the rank of the array, in this case one.	

a.ndim 

# The attribute "shape” is a tuple of integers indicating the size of the array in each dimension.

a.shape 

```

### Indexing and slicing

```
a[0]
a[2:3]
```

### Basic operations

```
a.mean()
a.max()
a.min()
a+1
```



## The basics: Numpy 2D Arrays 

```
a = [[1,2,3], [4,5,6], [7,8,9]]
A = np.array(a)
print(A)
```

```
A.shape
A.size
A.ndim
```




### Indexing and slicing

```
A[0,0]      # it will return 1
A[1,2]      # it will return 6
A[0][0]     # it will return 1
A[0,0:2]    # it will return array([1, 2])

A[A < 4]    # Print all of the values in the array that are less than 4
A[A>=4]     # Print all of the values in the array that are equal to or greater than 4
A[A%2==0]   # You can select elements that are divisible by 2

# Or you can select elements that satisfy two conditions using the & and | operators:

A[(A>2) & (A < 11)]
A[(A>2) | (A < 11)]

```



## Basic array
   


### Create an array filled with 0’s:

```
np.zeros(2)
```

### Create an array filled with 1’s:

```
np.ones(2)
```


### Create an empty array with 2 elements

```
np.empty(2)
```

### Create an array with a range of elements

```
np.arange(4)

np.arange(2, 9, 2)
```

### You can also use np.linspace() to create an array with values that are spaced linearly in a specified interval

```
np.linspace(0, 10, num=5)
```








