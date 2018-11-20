
# Distance Metrics - Lab

## Introduction

In this lab, we'll calculate various distances between multiple points using the distance metrics we learned about!

## Objectives

You will be able to:

* Calculate Euclidean Distance between 2 points
* Calculate Manhattan Distance between 2 points
* Compare and Contrast Manhattan, Euclidean, and Minkowski Distance

### Getting Started

To begin this lab, we'll start by writing a generalized function to calculate any of the three distance metrics we've learned about. Let's review what we know so far:

#### How These Distance Metrics Are Related

Recall from the previous lesson that **_Manhattan Distance_** and **_Euclidean Distance_** are both just special cases of **_Minkowski Distance_**. Take a look at the formula for Minkowski Distance below:

<img src='minkowski-equation.png'>

**_Manhattan Distance_** is a special case where $r=1$ in the equation above (which means that we can remove the root operation and just keep the summation).  

**_Euclidean Distance_** is a special case where $r=2$ in the equation above.

Knowing this, we can create a generalized `distance` function that just calculates minkowski distance, and takes in `r` as a parameter. That way, we can use the same function for every problem, and still calculate Manhattan and Euclidean distance metrics by just passing in the appropriate values for the `r` parameter!

In the cell below:

* Complete the `distance` function. 
* This function should take in 3 arguments:
    * `a`, a tuple or array that describes a vector in n-dimensional space. 
    * `b`, a tuple or array that describes a vector in n-dimensional space (this must be the same length as `a`!)
    * `r`, which tells us the norm to calculate the vector space (if set to `1`, the result will be Manhattan, while `2` will calculate Euclidean distance)
* Since euclidean distance is the most common distance metric used, this function should default to using `r=2` if no value is set for `r`.
* Include a parameter called `verbose` which is set to `True` by default. If true, the function should print out if the distance metric returned is a measurement of Manhattan, Euclidean, or Minkowski distance.  
* This function should implement the minkowski distance equation above, and return the result. 

**_NOTE:_**  Remember that for Manhattan Distance, you need to make use of `np.abs()` to get the absolute value of the distance for each dimension, since we don't have the squaring function to make this positive for us!

**_HINT:_** Use `np.power()` as an easy way to implement both squares and square roots. `np.power(a, 3)` will return the cube of `a`, while `np.power(a, 1/3)` will return the cube root of 3. For more information on this function, see the numpy [documentation](https://docs.scipy.org/doc/numpy-1.15.1/reference/generated/numpy.power.html)!


```python
import numpy as np

def distance(a, b, r=2, verbose=True):
    if len(a) != len(b):
        raise ValueError("Both vectors must be of equal length!")
    
    root = 1 / r
    running_total = 0
    
    if verbose:
        if r == 1:
            print("Calculating Manhattan Distance:")
        elif r == 2:
            print('Calculating Euclidean Distance:')
        else:
            print("Calcuating Minkowski Distance (r={}):".format(r))
    
    for ind, val_a in enumerate(a):
        val_b = b[ind]
        running_total += np.power(np.abs(val_a - val_b), r)
    
    return np.power(running_total, root)

test_point_1 = (1, 2)
test_point_2 = (4, 6)
print(distance(test_point_1, test_point_2)) # Expected Output: 5.0
print(distance(test_point_1, test_point_2, r=1)) # Expected Output: 7.0
print(distance(test_point_1, test_point_2, r=3)) # Expected Output: 4.497941445275415
```

    Calculating Euclidean Distance:
    5.0
    Calculating Manhattan Distance:
    7.0
    Calcuating Minkowski Distance (r=3):
    4.497941445275415
    

Great job! 

Now, let's use the function so solve some practice problems.

### Problem 1:

Calculate the **_Euclidean Distance_** between the following points in 5-dimensional space:

Point 1: (-2, -3.4, 4, 15, 7)

Point 2: (3, -1.2, -2, -1, 7)


```python
print(distance((-2, -3.4, 4, 15, 7), (3, -1.2, -2, -1, 7))) # Expected Output: 17.939899665271266
```

    Calculating Euclidean Distance:
    17.939899665271266
    

### Problem 2:

Calculate the **_Manhattan Distance_** between the following points in 10-dimensional space:

Point 1: \[0, 0, 0, 7, 16, 2, 0, 1, 2, 1\]  
Point 2: \[1, -1, 5, 7, 14, 3, -2, 3, 3, 6\]


```python
print(distance( [0, 0, 0, 7, 16, 2, 0, 1, 2, 1],  [1, -1, 5, 7, 14, 3, -2, 3, 3, 6], r=1)) # Expected Output: 20
```

    Calculating Manhattan Distance:
    20.0
    

### Problem 3: 

Calculate the **_Minkowski Distance_** with a norm of 3.5 between the following points:

Point 1: (-2, 7, 3.4)
Point 2: (3, 4, 1.5)


```python
print(distance((-2, 7, 3.4), (3, 4, 1.5), r=3.5)) # Expected Output: 5.268789659188307
```

    Calcuating Minkowski Distance (r=3.5):
    5.268789659188307
    

# Conclusion

Great job! Now that we know how to calculate distance metrics, we can easily apply this to writing a K-Nearest Neighbors classifer from scratch!