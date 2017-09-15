---
title: Decision Tree Classification
sidebar: machine_sidebar
permalink: dtc.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

**CART: Classification AND Regression Trees**

## Introduction

The goal of the Decision Tree Regression Algorithm is to split your data into groups. The algorithm uses something called *information entropy*, which is a mathematical process. The point of the algorithm is to split the data in such a way that information is added and stops splitting the data when it's unable to add any more information to the dataset. 

Before we saw the Decision Tree Regression. Remember Classification trees, classify the data and predict categories and Regression Trees predict data of real numbers. Here in this part we will be looking at how Decision Tree's can be used to classify data.

<img src="\images\machine-learning\classification\dtc1.png" alt="Decision Tree Splits" style="width:650px;height:358px;">

Here we see a graph with a split across different categories using a decision tree algorithm. The decision tree makes splits in a way that would maximize the number of points in each class. Tries to minimize entropy.

The decision tree would like this:

<img src="\images\machine-learning\classification\dtc2.png" alt="Decision Tree Splits" style="width:650px;height:358px;">

This is the method that will be used to add a new data point and classify it to the graph. Additionally, who don't always have to go all the way to the very end of the tree. Most of the time the tree will be very long and so at any point you could stop and have it run a probability of where to classify the point.

## Decision Tree in Python (classification part)

~~~python
from sklearn.tree import DecisionTreeClassifier
classifier = DecisionTreeClassifier(criterion = 'entropy', random_sate = 0)
classifier.fit(X_train, y_train)
~~~