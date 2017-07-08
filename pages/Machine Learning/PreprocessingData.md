lorical_features = [0])
  X = onehotencoder.fit_transform(X).toarray()
  #Encoding the Dependent Variable
  labelencoder_y = LabelEncoder()
  y = labelencoder_y.fit_transform(y)
  ~~~
  
  
  5 - Splitting Dataset into Training and Test sets
  ---------------------------------------------------
  In machine learning we want to split our dataset into two parts. A training set and a test set. This is used as a way to avoid the machine learning model from relying on correleations too much. We want to do this because if the model learns about correlations that may not always exist in other datasets it may put more weight than it should on those correlations when making a prediction. The test set is meant as away for machine learning model to test it's predictions and re-adjust how it is learning
  
  **Training Set** : The machine learning model uses this to identifiy correlations
  **Test Set** : MAchine learning model makes predictions and adjusts weight of correlation based on the how the predction relates to the actusal value.
  
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
  
  **Template for Splitting the Data**
  ~~~ python
  #Splitting the dataset into the Training set and Test set
  from sklearn.cross_validation import train_test_split
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 0)
  ~~~
  
  6 - Feature Scaling 
  --------------------
  When we have independendt variable that are numerical and not on the same scale. For example it one of our independent variables was: 0, 3, 2, 1 ,4 ,6 and the other column was 2312, 1231, 6712, 1232. Then we have a problem, since many machine learning models are based on the Euclidian Distance (Distance between two point on a plane). Since the second column has much larger values the Euclidian Distance will be dominated by it, making our machine learning model think that the other column will lower values has less impact than the 2nd column, which is not the case. 
  
  Typically there are two mathematical solutions to solve this issue. 
  Standardization: X minus the mean Divided by the Standard Deviation
  Normalization: X minus the minimum value Divided by Max value minus min value.
  
  From the preprocessing library from scikit learn we'll import the StandardScaler library to perfom standardization on our variables.
  ~~~ python 
  from sklearn.preprocessing import StandardScaler
  ~~~
  Create an object
  ~~~ python 
  sc_X = StandardScaler()
  ~~~
  Next we need to fit the object to the test set and then transform it like this:
  ~~~ python 
  X_train = sc_X.fit_transform(X_train)
  ~~~
  Do the same for the training set but we do not need to fit it because its already fitted to the training set.
  ~~~ python 
  X_test = sc_X.transform(X_test)
  ~~~
  Lastly, we just do the same to the training set for the dependent variable. We don't need to do it the Y test set because
  ~~~ python 
  sc_y = StandardScaler()
  y_train = sc_y.fit_transform(y_train)
  ~~~
  
  **Template for Splitting the Data**
  ~~~ python
  #Feature Scaling
  from sklearn.preprocessing import StandardScaler
  sc_X = StandardScaler()
  X_train = sc_X.fit_transform(X_train)
  X_test = sc_X.transform(X_test)
  sc_y = StandardScaler()
  y_train = sc_y.fit_transform(y_train)
  ~~~
  
  7 - Preprocessing Template 
  ----------------------------
  **Template **
  ~~~ python
  #Importing the libraries
  import numpy as np
  import matplotlib.pyplot as plt
  import pandas as pd
  
  #Importing the dataset
  dataset = pd.read_csv('Data.csv')
  X = dataset.iloc[:, :-1].values
  y = dataset.iloc[:, 3].values
                  
  #Taking care of missing data
  from sklearn.preprocessing import Imputer
  imputer = Imputer(missing_values = 'NaN', strategy = 'mean', axis = 0)
  imputer = imputer.fit(X[:, 1:3])
  X[:, 1:3] = imputer.transform(X[:, 1:3])
  
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
  
  #Splitting the dataset into the Training set and Test set
  from sklearn.cross_validation import train_test_split
  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 0)
  
  #Feature Scaling
  from sklearn.preprocessing import StandardScaler
  sc_X = StandardScaler()
  X_train = sc_X.fit_transform(X_train)
  X_test = sc_X.transform(X_test)
  sc_y = StandardScaler()
  y_train = sc_y.fit_transform(y_train)
  ~~~
