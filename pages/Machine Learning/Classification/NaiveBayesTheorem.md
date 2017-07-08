---
title: Naive Bayes Theorem 
sidebar: machine_sidebar
permalink: bayes.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>


Use the classification template to set everything up.

Create the classifier and set it up

``` python 
from sklearn.naive_bayes import GaussianNB
classifier = GaussianNB()
classifier.fit(X_train, y_train)
```
run code...

