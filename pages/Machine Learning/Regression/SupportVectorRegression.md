---
title: Support Verctor Regression
sidebar: machine_sidebar
permalink: svr.html
folder: Machine Learning
---
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Support Vector Regression (SVR)

Setup the using the Regression Template.
**FEATURE SCALING** is not done by SVR class so make sure to do it.

~~~python
#Applying feature scaling with no X/y train/ test
sc_X = StandardScalar()
sc_y = StandardScalar()
X = sc_X.fit_transform(X)
Y = sc_y.fit_transform(y)
~~~

## Create Regressor

Import the SVR class from scikit learn library
Create the object for SVR class
Argumnets of SVR() class:

`kernal` : Choose between linear, polynomial, sigmoid or rbf kernal
rbf: Gaussian Kernal. Most popular for nonlinear regressions

~~~python 
from sklearn.svm import SVR
regressor = SVR(kernal='rbf')
regressor.fit(X,y)
~~~

Predicting the value. We can either input an array like X_test or a single value like 6.5 (that needs to be converted into an array) into our predict() method.

Since however the value '6.5' is not feature scaled we will need to do that. this can be done with `sc_X.transform(6.5)`.
To convert 6.5 into an a array just do : np.arra([[6.5]])
However now that we feature scaled we would get the wrong value as a prediction. This is because 6.5 will be converted into a vaule like 0.303 and we would predict that value.
To fix this problem we apply the `inverse_transform` method. 

~~~python 
y_pred = sc_y.inverse_transform(regressor.predict(sc_X.transform(np.array([[6.5]]))))
~~~
