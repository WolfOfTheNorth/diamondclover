---
title: K - Nearest Neighbors Algorithm (K-NN)
sidebar: machine_sidebar
permalink: knn.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

Steps
1. Choose the number k of neighbors (default is usually 5) 
2. Take the K nearest neighbors of the new data point, accoding to the Euclidean distance
3. Among these K neighbors, count the number of data points in each category
4. Assign the new data point to the category where you counted the most neighbors 

## Building the K-NN in Python

Use classsification Template and preprocess the data.

import `kNeighborsClassifier` from the `sklearn.neighbors` library and fit the object to the training set.

'KNeighborsClassifier' has the following parameters :
`n_neighbors` : # of neighbors to use 
`metric` : Distance metric for use for tree. Use 'minkowski'
`p` : Power parameter. Euclidean distance = 2.

~~~python
from sklearn.neighbors import KNeighborsClassifier
classifier = KNeighborsClassifiers(n_neighbors = 5, metric = 'minkowski', p = 2)
classifier.fit(X_train, y_train)
~~~

