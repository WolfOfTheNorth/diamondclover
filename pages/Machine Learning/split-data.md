---
title: Splitting Dataset into Training and Test sets
sidebar: machine_sidebar
permalink: /split-data.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Introduction

In machine learning we want to split our dataset into two parts. A training set and a test set. This is used as a way to avoid the machine learning model from relying on correleations too much. We want to do this because if the model learns about correlations that may not always exist in other datasets it may put more weight than it should on those correlations when making a prediction. The test set is meant as away for machine learning model to test it's predictions and re-adjust how it is learning.

**Training Set** : The machine learning model uses this to identifiy correlations
**Test Set** : MAchine learning model makes predictions and adjusts weight of correlation based on the how the predction relates to the actusal value.

## Performing the split in Python 

Import the `crossvalidation` library from scikit learn
  ~~~ python 
  from sklearn.cross_validation import train_test_split
  ~~~
  Split the data using the method `train_test_split`
  The arguments:
  `Arrays`: Array of set. In the case `X` and `y` corresponds to the entire Dataset
  `test_size`: Is a number between 0 to 1 that corresponds to the % size of the test size. Typically we want anywhere between 15% - 30% for our test size.
  `random_state` : Set to 0 to keep the results the same all the time. Used for random sampling. Usually 42 or 0.
  
  ~~~ python 
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 0)
  ~~~
  
  ## **Template for Splitting the Data**
  ~~~ python
  #Splitting the dataset into the Training set and Test set
  from sklearn.cross_validation import train_test_split
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 0)
  ~~~