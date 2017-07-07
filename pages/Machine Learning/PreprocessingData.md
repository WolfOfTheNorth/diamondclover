
  Preprocessing the Data
  =======================
  
  **Precondition**: Set you working directory
  
  1 - Importing Libraries
  -------------------
    1. Numpy: Package for scientific computing withPython
    2. MATPLOTLIB: Used for graphing
    3. Pandas: Data Structures and Data Analysis Tool
  
  ~~~ python
  #Importing the libraries
  import numpy as np
  import matplotlib.pyplot as plt
  import pandas as pd
  ~~~
  
  2 - Importing the Dataset
  ----------------------
  We want to use the `pandas` library to import the dataset from a CSV file, using the `.read_csv()` funtion.
  
  ~~~ python
  dataset = pd.read_csv('Data.csv')
  ~~~
  
  The next step is to distinguish between the matrix of featues (the independent variables) and the dependent variable. To do this we need to tell python which columns are independent and which are dependent.
  
  **Note**: In python the index for columns and rows starts at zero. 
   To do this we take our variablle dataset and use the `.iloc[]` method from pandas. The method takes two inputs (or 4).
   
   `.iloc[ :, ]` : The first input is the rows we wish to use. The `:` simply implies that we want to use all the rows. 
   `.iloc[rows, columns start : columns end but not including]` : The left side takes columns and this part gets a little confusing so here are examples to explain:
            1. `iloc[rows, : -1]` : All columns except the last one
            2. `iloc[rows, 2:13]` : All columns from 2 until 12. 13 is NOT INCLUDED
  
  we then use the `.values` function to retrieve the values from the column. 
  ~~~ python
  X = dataset.iloc[:, :-1].values
  Y = dataset.iloc[:, 3]
  ~~~
  **Note** : We always want to make sure that X is an array so size should like (10,1) and Y should be a vector, which looks like (10,)
  
  3 - Handling Missing Data 
  -------------------------
  Sometimes our dataset may have missing data that we will want to handle
  A simple way to deal with missing data is to enter the average of the rest of the column and replace it.
  
  To do this we can import scikit learns Imputer class from the preprocessing sub-class which will help take care of the missing data.
  The Sckit Learn library is a library used to make machine learning models. 
  ~~~ python
  from sklearn.preprocessing import Imputer
  ~~~
  Create object of the Imputer class: 
        - `missing_values = 'NaN'` : Placeholder for misisng values that will be replaced by the Imputer class
        - `strategy='mean'` : Take the mean of the columns.
        - `axis = 0` : Takes the mean of the column. axis=1 takes mean of the rows
        
  ~~~ python
  imputer = Imputer(missing_values = 'NaN', strategy = 'mean', axis = 0)
  ~~~
  
  Next, fit the Imputer object to the part of the Dataset where we have to make the change, specifically in the X axis. Here, we want columns 1 and 2 with all the rows, so:
  ~~~ python
  imputer = imputer.fit(X[:, 1:3])
  ~~~
  Finally, replace the columns with missing data X[:, 1:3] to the transform method replaces the missing data with the mean of the column.
  ~~~ python
  X[:, 1:3] = imputer.transform(X[:, 1:3])
  ~~~
  
  **Template for Handling Missing Data**
  ~~~ python
  #Taking care of missing data
  from sklearn.preprocessing import Imputer
  imputer = Imputer(missing_values = 'NaN', strategy = 'mean', axis = 0)
  imputer = imputer.fit(X[:, 1:3])
  X[:, 1:3] = imputer.transform(X[:, 1:3])
  ~~~
  
  4 - Encoding categorical Data
  -----------------------------
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
  
  Let's create an LabelEncoder Object for our column 
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
