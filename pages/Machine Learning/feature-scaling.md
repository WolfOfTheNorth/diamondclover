---
title: Feature Scaling
sidebar: machine_sidebar
permalink: /feature-scaling.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Introduction 

When we have independendt variable that are numerical and not on the same scale. For example it one of our independent variables was: 0, 3, 2, 1 ,4 ,6 and the other column was 2312, 1231, 6712, 1232. Then we have a problem, since many machine learning models are based on the Euclidian Distance (Distance between two point on a plane). Since the second column has much larger values the Euclidian Distance will be dominated by it, making our machine learning model think that the other column will lower values has less impact than the 2nd column, which is not the case. 

Typically there are two mathematical solutions to solve this issue. 

**Standardization**: X minus the mean Divided by the Standard Deviation

**Normalization**: X minus the minimum value Divided by Max value minus min value.

## Performing Feature Scaling in Python 
From the preprocessing library from scikit learn we'll import the StandardScaler library to perfom standardization on our variables.
~~~ python 
from sklearn.preprocessing import StandardScaler
~~~
Create an object
~~~ python 
sc_X = StandardScaler()
~~~
Next we need to fit the object to the test set and then transform it like this:
~~~ python 
X_train = sc_X.fit_transform(X_train)
~~~
Do the same for the training set but we do not need to fit it because its already fitted to the training set.
~~~ python 
X_test = sc_X.transform(X_test)
~~~
Lastly, we just do the same to the training set for the dependent variable. We don't need to do it the Y test set because
~~~ python 
sc_y = StandardScaler()
y_train = sc_y.fit_transform(y_train)
~~~

## **Template for Splitting the Data**
~~~ python
#Feature Scaling
from sklearn.preprocessing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X_train)
X_test = sc_X.transform(X_test)
sc_y = StandardScaler()
y_train = sc_y.fit_transform(y_train)
~~~