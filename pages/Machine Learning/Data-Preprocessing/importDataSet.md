---
title: Import Dataset and Libraries 
sidebar: machine_sidebar
permalink: import.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

**Precondition**: Make sure to set your working directory.

## Important Libraries

1. **Numpy**: Package for scientific computing withPython
2. **MATPLOTLIB**: Used for graphing
3. **Pandas**: Data Structures and Data Analysis Tool

## Import the libraries 

~~~ python
#Importing the libraries
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
~~~
`as` is used as a shorthand to access the imported library.

## Importing the Dataset

We want to use the `pandas` library to import the dataset from a CSV file, using the `.read_csv()` funtion:

~~~python
dataset = pd.read_csv('Data.csv')
~~~

Now we need to be able to distinguish between the data we just imported, the independent variables (matrix of featues) and the dependent variable. To do this we need to tell python which columns are independent and which are dependent.

**Note**: In python the index for columns and rows starts at zero. 

To do this we take our variablle dataset and use the `.iloc[]` method from pandas. The method takes two inputs (or 4).

`.iloc[ :, ]` : The first input is the rows we wish to use. The `:` simply implies that we want to use all the rows. 
`.iloc[rows, columns start : columns end but not including]` : The left side takes columns and this part gets a little confusing so here are examples to explain:
        1. `iloc[rows, : -1]` : All columns except the last one
        2. `iloc[rows, 2:13]` : All columns from 2 until 12. 13 is NOT INCLUDED

we then use the `.values` function to retrieve the values from the column. 

~~~ python
X = dataset.iloc[:, :-1].values
Y = dataset.iloc[:, 3]
~~~

 **Note** : We always want to make sure that X is an array so size should like (10,1) and Y should be a vector, which looks like (10,)