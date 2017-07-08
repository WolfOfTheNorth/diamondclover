---
title: MultiLinear Regression
sidebar: machine_sidebar
permalink: multilinear-regression.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

**Multiple Linear Regression**

## 1 - Intuititon

Formula for Simple Linear Regression:

$$y= b_{_0} + b_{_1}x_{_1}$$ 

Formula for Multiple Linear Regression

$$y= b_{_0} + b_{_1}x_{_1} + b_{_2}x_{_2} + ... + b_{_n}x_{_n}$$ 

There are multiple independent vaiables in this case.

**Assumptions for Linear Regressions which must be true**
1. Linearity
2. Homoscedasticity
3. Multivariate Normality
4. Independence of Errors
5. Lack of Multicollinearity

**2 - Dummy Variables**

As discussed before dummy variables are used as a way to turn categorical data into numerical data by creating a new set of columns in which 1 represents that category being true and 0 meaning that the category is false. 

Multivariable Linear Regression we add the dummy variables to our machine learning model:
$$y = b_{_0} + b_{_1}X_{_1} + b_{_2}X_{_2} + b_{_3}D_{_1} + b_{_4}D_{_2}$$
where, $$D_{_0}$$ : Represents the Dummy Variable being used for our categorical data

So, if we had for example a column with two cities like Tokyo and Beijing. We could split them into there own two sepreate categories where we define its state with a '1' or '0'. 


|City   | 
|-------|
|Tokyo  |
|Beijing|
|Beijing|
|Tokyo  |
|Beijing|


|Tokyo|Beijing| 
|-----|-------|
|1    |0      |
|0    |1      |
|0    |1      |
|1    |0      |
|0    |1      |


Where $$D_{_1}$$ will represent Tokyo. Beijing is ignored

Now, it may seem biased that we would have a variable for Tokyo and not one for Beijing. The reason for this is that is because when $$D_{_1}$$ is zero the entire part of that equation $$b_{_4}D_{_1}$$ will be zero. Regression models will take, by default, the dummy variable taht is not included will become the default situation when $$D_{_1}$$ is zero and is included in the constant $$B_{_0}$$

So basically when $$D_{_1}$$ is 1 the state is for Tokyo and when its '0' the state is for the deafult state (the one not included) in this case Beijing.

**Dummy Variable Trap**
Occurs when we add all Dummy variable to our equation. The reason why this bad is basically because we would be duplicating a varaible. This is because : $$D_{_2} = 1 - D_{_1}$$. The phenomenon where one or several independednt variables in a linear regression predict another is called multi-colinearity. As a result of this effect, the model cannot disguinsh between the effect of $$D_{_1}$$ and $$D_{_2}$$ and therefore will not work properly. 

** SO ALWAYS EMIT ONE DUMMY VARIABLE ** 


## Building a model (Step by step)

When we have many independent variable ( $$X_{_1},X_{_2}, ... , X_{_n}$$ ) we may need to remove some of these variables.

**Why?**
1. Some independent variable are not important and having them could ruin our model
2. We need to be able to understand what certain variables predict and what there imapct is and it's impractical to do that if we have hundreds of variables.

**Types of Models**
1. All-in
2. Backward Elimination (Stepwise Regression)
3. Forward Elimination (Stepwise Regression)
4. Bidirectional Elimation (Stepwise Regression)
5. Score Comparison

## 1 - All-In Method

Using all variables.

**USAGE**:
1. You prior knowledge of all your variables. 
2. Framework
3. Preparing for a Backward Elimination

## 2 - Backward Elimination

1. Select the significance level to stay in the model (by default its 5% so, SL = 0.05).
2. Fit the full model with all possible predictors (all independednt variables).
3. Consider the predictor with the highest P-Values. P-Value > SL --> Go to Step 4 Else FIN
4. Remove that predictor
5. Fit model without this variable. Going back to step 3.
**FIN** : Model is ready

## 3 - Forward Selection Model

1. Select the significance level to enter the model. (SL = 0.05)
2. Fit the simple regression models $$y ~ x_{_n}$$ . Select the one with the lowest P - Value.
  - So we take the dependent variable and we create a regression model with EVERY single independent variable that we have. Then select out of all models the one with the lowest P - Value for the independent variables.
3. Keep selected variable and fit all possible models with one extra predictor added to the ones you already have. (basically we started by adding a single variable in step 2 and we're adding variables to our model).
4. Consider the predictor with the lowest P-value. If P < SL --> Step 3. ELse fo to FIN
**FIN** Model Completed

## 4 - Bidirectional Elimination 

1. Select a significance level to enter and to stay in the model (e.g: SL_Enter = 0.05, SL_Stay = 0.05)
2. Perform the next step of FORWARD ELIMINATION (new variable has: P < SL_Enter to enter)
3. Perform ALL steps of the BACKWARD ELIMINATION method (old variable has P < SL_Stay to stay). 
4. No new varibales can enter and no old variables can exit. Go to FIN
**FIN** Model is ready

## 5 - All possible Models

1. Select a criterion of goodness of fot (e.g Akaike Criterion)
2. Construct all possible regression models (2^n -1 total combinations)
3. Select the one with the best criterion
**FIN**: Model is complete


## Multivariable Linear Regression Python

Preprocess the data using the template from the preprocessing section.

If you creates dummy variables using `OneHotEncoder` you'll need to make sure we avoid the **Dummy VAriable Trap**. To do this we remove the last dummy variable from our quation 

~~~ python
X = [:, 1:]
~~~

By doing this, we're taking all the lines of X. By doing "1:" we take all the coulmns of X starting from the first index to one. That way if our dummy variables start from index 0 we can remove it.

**IMPORTANAT** : The Pyhton library for Linear Regression will automatically take care of the dummy variable trap for us, so we do not need to add this piece of code. Smae for **FEATURE SCALING**

Import the linear regression library and store the object of the `LinearRegression` method inside a variable.

~~~ python
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
~~~

Fit object to training set

~~~ python 
regressor.fit(X_train, y_train)
~~~

Predicting the results of the Test Set. We create the vector of predictions which we can call y_pred and use the `predict()` method to predict the y_test from X_test. 

~~~ python 
y_pred = regressor.predict(X_test)
~~~

Now, we can start looking at ways at improving out models prediction.This is where we can use thinhs like BAckward Elimination or Bidirectional Elimination to choose independent variables that are more statistically significant instead of using them all.

Using Backward Elimination,

Preparing the backward elimination,
Import the stats models formula API.

~~~ python 
import statesmodels.formula.api as sm
~~~

The stats model library does not take into account the $$b_{_0}$$ constant in the equation for multilinear regression $$y= b_{_0} + b_{_1}X_{_1} +...$$ so to do this we need to create a column for the constant $$b_{_0}$$ and we'll call it $$X_{_0}$$, which we can set to be "1". SO in out dataset we will have a coulmn of 1's corresponding to this variable.

To do this we will use the append function from the numpy library to create a new column of 1's for our dataset of X.
append() will take the following arguments

`arr` : array to which we will want to add our coulmn too. Which is our matrix of features X.
`values` : array of what we want to append.
  - To do this we will use the `ones()` function from the numpy library. This function will create an array with ones. 
  - The `ones()` function takes the shapes parameter which is specified in brackets like (# of lines, # of columns). So if we want 50 lines and 1 coulmn it'll be ones((50,1)).
  - Finally we simply need to convert to integer with the `asType(int)`
`axis` : 0 means append a row. 1 means append a column. 

~~~ python 
X = np.append(arr = X, values = np.ones((50,1)).asType(int), axis = 1)
~~~

The problem however is that we are adding the column of 50 ones to our matrix of features X but we're adding it at the end of our matrix of features X. We want to add it to the beginning.

To solve this, instead of adding the array of 50 ones to X we can invert it and add the array X to the array of 50 ones by changing X and values to be the opposite of what they are now.

~~~ python 
X = np.append(arr = np.ones((50,1)).asType(int), axis =1)
~~~

Starting Backward Elimination,

Create a variable for our optimal matrix of features that is a variable that will have the independent variable that are statistically most signficant for the dependent variable.

So the first step is to take our matrix of features X with ALL the independent variables. So if we have 6 independent variables, we will have to specifiy the index [0,1,2,3,4,5].

~~~ python
X_opt =  X[:, [0,1,2,3,4,5]]
~~~

Previously, we craeted a variable called 'regressor' from the `LinearRegression` library. We'll want to re-create a new 'regressor' variable this time using the `statsmodels` library that we imported. The class we'll want to implement is called OLS (Ordinaril Linearly Sqaured).
OLS will have two important arhuments
`endog` : Dependent variable array
`exdog` : Array with # of observations and k is the number of regressors.

~~~ python
#Fit the full model with all possible predictors
regressor_OLS = sm.OLS(endog, y, exdog = X_opt.fit())
~~~

We will use the .suumary() function to inspect the P-value for every independent variable
~~~ python 
regresso_OLS.summary()
~~~

Once we run that we will be given a table a we need to look for the P-values under `P > |t|`.
Remember that our significance level is 5% (SL = 0.05). 
|const|P > t|
|----|-----|
|const|0.000|
|x1  |0.953|
|x2  |0.990|
|x3  |0.000|
|x4  |0.608|
|x5  |0.123|

First pick the variable with largest P-value (in this case it's x2 @ 99 %). Since this is greater than our SL we will remove it.

So, to remove the predictor simply do it like this: 

~~~ python 
x_opt = X[: , :[0,1,3,4,5]]
regressor_OLS.summary
~~~

Repreat the steps until the variable with largest P-value has a P-value that is less than or equal to 0.05.

Once this method is done we should have all statistically significant variables.
We can use this to then build a new y_pred for our predictions.



