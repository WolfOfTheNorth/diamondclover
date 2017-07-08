---
title: Handling Missing Data
sidebar: machine_sidebar
permalink: missing-data.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Introduction

Sometimes our dataset may have missing data that we will want to handle
A simple way to deal with missing data is to enter the average of the rest of the column and replace it.

To do this we can import scikit learns Imputer class from the preprocessing sub-class which will help take care of the missing data.

The Sckit Learn library is a library used to make machine learning models. 

~~~ python
from sklearn.preprocessing import Imputer
~~~

## Handling the missing data 

Create object of the Imputer class: 
    - `missing_values = 'NaN'` : Placeholder for misisng values that will be replaced by the Imputer class
    - `strategy='mean'` : Take the mean of the columns.
    - `axis = 0` : Takes the mean of the column. axis=1 takes mean of the rows
    
~~~ python
imputer = Imputer(missing_values = 'NaN', strategy = 'mean', axis = 0)
~~~

Next, fit the Imputer object to the part of the Dataset where we have to make the change, specifically in the X axis. Here, we want columns 1 and 2 with all the rows, so:
~~~ python
imputer = imputer.fit(X[:, 1:3])
~~~
Finally, replace the columns with missing data X[:, 1:3] to the transform method replaces the missing data with the mean of the column.
~~~ python
X[:, 1:3] = imputer.transform(X[:, 1:3])
~~~

**Template for Handling Missing Data**
~~~ python
#Taking care of missing data
from sklearn.preprocessing import Imputer
imputer = Imputer(missing_values = 'NaN', strategy = 'mean', axis = 0)
imputer = imputer.fit(X[:, 1:3])
X[:, 1:3] = imputer.transform(X[:, 1:3])
~~~