---
title: Random Forest Tree
sidebar: machine_sidebar
permalink: randomForest.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>


A version of Ensemble Learning.
**Ensemble Learning**: Take multiple algorithms and use them together.


## Steps Involoved:
1. Pick at random K data points from the Training set.
- Using the entire dataset we pick k data points from that set
2. Build the Decision Tree associated to these K data points.
- Rather than building a decicion tree based on everything in you dataset. We just build it based of those K datapoints. 
3. Choose the number of Ntree of tress you want to build and repeat Step 1 and step 2.
4. For a new data point, make each one of your Ntree trees predict the value of Y to the data point in question, and assign the new data point the avaerage across all of the predicted Y values. 
- Basically, instead of getting one prediction from a Decision Tree we get many (usually 500 trees) and we take the average across those.

## Why we use it

The reason for using Ensemble Learning is because one algorithm is typically not too accurate or may have major flaws in some aspects. By using many algorithms and averaging their results we reduce errors. Because changes in the dataset can greatly affect one algortihm that could ruin the prediction but with many algorithms being used it is much harder for results to get skewed, making it very durable.

## Building a Random Forest Regression 

Use the [regression template](/reg-template.html) to set everything up. Use **Higher resolution visualization**.

### Create Regressor

Import the `RandomForestRegressor` class from the library `sklearn.ensemble`
`n_estimators`: Number of trees in forest

~~~ python 
from sklearn.ensemble import RandomForestRegressor
regrssor = RandomForestRegressor(n_estimators = 300, random_state = 0)
regressor.fit(X, y)
~~~


  
  
  
  