---
title: Decision Tree Regression 
sidebar: machine_sidebar
permalink: decision-tree.html
folder: Machine Learning
---
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>



**CART: Classification AND Regression Trees**

### Regression Trees


For example, given a scatter plot with two Independent Variables $$X_{_1}$$ and $$X_{_2}$$ with 'y' being in the third dimension.



## Building Decision Tree Regression


Use the Regression Template to preprocess the data

## Creating the Regressor 

Import the `DecisionTreeRegressor` class from the library `sklearn.tree` and create an object of the class.

DecisionTreeRegressor takes the arguments:
`random_state`: to get the same result use the same number for random_state

~~~ python 
from sklearn.tree import DecisionTreeRegressor
regressor = DecisionTreeRegressor(random_state = 0)
regressor.fit(X, y)
~~~

The problem is that we need to make sure the resolution is higher using the template. This is because a Decision Tree is not a continous function but instead a **step wise function**

~~~ python
#HIGH RESOLUTION AND SMOOTHER CURVE
X_grid = np.arrange(min(X), max(X), 0.01)
X_grid = X_grid.reshape((len(X_grid), 1))
plt.scatter(X, y, color='red')
plt.plot(X_grid, regressor.predict(X_grid), color = 'blue')
plt.title('Title of my Model)
plt.xlabel('X Axis Title')
plt.ylabel('Y Axis Title')
plt.show()
~~~