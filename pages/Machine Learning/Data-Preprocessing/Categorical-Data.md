---
title: Encoding categorical Data
sidebar: machine_sidebar
permalink: /categorical-data.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Introduction

Categorical data is data that is typically formatted in a string format in the dataset. Things like names, places, Countries, etc... In order for the machine learning model to be able to properly use this information it first needs to be encoded into a numerical form.

The methodology behind this is simple. Let's say we have a column of countries with three countries: Canada, USA, and Mexico. In order to properly encode this we can first split the entire column into three seperate columns each for a different country. We the simply insert '0' when the country isn't in that column and '1' when it is.

Example: 
<table> 

<tr><td>

Original

| Countries |
|-----------|
| Canada    |
| USA       |
| Canada    |
| Spain     |
| USA       |
| Spain     |
| USA       |
| USA       |
| Spain     |

</td><td>

Applying the Label Encoder

|Countries|
|--|
|0 |
|1 |
|0 |
|2 |
|1 | 
|2 |
|1 | 
|1 |
|2 |

</td><td>

Applying the OneHotEncoder

| Canada | USA | Spain |
|--------|-----|-------|
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 0 | 1 | 0 |
| 0 | 0 | 1 |
</td></tr>
</table>

These three are called Dummy Variables


So, to actually encode data in python we need to use the `preprocessing` library from scikit learn and import the `LabelEncode` method and `OneHotEncoder` method.

~~~ python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
~~~

Then we'll need to handle the independent and dependent variables seperately.

Let's create an LabelEncoder Object for our column:

~~~ python
labelencoder_X = LabelEncoder()
~~~
Now use fit this object to our independent column to return an array of encoded data. This array will only represent just this one column. So in the example of countries, Canada becomes 0, USA become 1, Spain becomes 2. We then set this endoded data to the column in the dataset.

~~~ python
X[:, 0] = labelencoder_X.fit_transform(X[:, 0])
~~~

This isn't good yet. Since the data is numerically valued 0, 1, and 2. Our machine learning model will take the rank of these numbers into account. So, 2 is better than 1 which is better than 1. So to fix this we wan to split the colum into three seperate columns where 0 represents that the value isn't true and 1 states that the value is true. This called using Dummy Encoding to have Dummy Variables.

`categorical_features` : Wants the index of the column of where we want to encode
`.toarray`: Converts to array 

~~~ python 
onehotencoder = OneHotEncoder(categorical_features = [0])
X = onehotencoder.fit_transform(X).toarray()
~~~

The same logic applies to encoding the dependent variable:

~~~ python 
labelencoder_y = LabelEncoder()
y = labelencoder_y.fit_transform(y)
~~~

**Template for Encoding Categorical Data**
~~~ python
#Encoding categorical data
#Encoding the Independent Variable
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_X = LabelEncoder()
X[:, 0] = labelencoder_X.fit_transform(X[:, 0])
onehotencoder = OneHotEncoder(categorical_features = [0])
X = onehotencoder.fit_transform(X).toarray()
#Encoding the Dependent Variable
labelencoder_y = LabelEncoder()
y = labelencoder_y.fit_transform(y)
~~~