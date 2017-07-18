---
title: SVM - Support Vector Machine 
sidebar: machine_sidebar
permalink: svm.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Introduction

The goal of support vector machines is to seperate categorcial data in the most optimal way, so that when a new data point is entered it can easily be classified. 

Given training examples, each marked as belongong to one or the other of two categories, an SVM training algorithm builds a model that assigns new examples to one category or the other, making it a non-probabilistic binary linear classifier. 

## Building an SVM 

Use the classification template to set eveything up

Create the classifer 

~~~ python 
from sklearn.svm import SVC
classifier = SVC(kernel = 'linear', random_state = 0)
classifier.fit(X_train, y_train)
~~~

## Building an SVM (Not linearily seperable)

Create classifer

`kernal` : linear, ploy, rbf 

~~~ python 
from sklearn.svm import SVC
classifier = SVC(kernel = 'rbf', random_state = 0)
classifier.fit(X_train, y_train)
~~~
