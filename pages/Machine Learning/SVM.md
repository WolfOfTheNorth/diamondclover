type: "MARKDOWN_NOTE"
folder: "0d374c8040ef660e27e1"
title: "SVM - Support Vector Machine"
content: '''
  SVM - Support Vector Machine 
  =============================
  
  Given training examples, each marked as belongong to one or the other of two categories, an SVM training algorithm builds a model that assigns new examples to one category or the other, making it a non-probabilistic binary linear classifier. 
  
  Building an SVM 
  ===============
  
  Us ethe classification template to set eveything up
  
  Create the classifer 
  
  ~~~ python 
  from sklearn.svm import SVC
  classifier = SVC(kernel = 'linear', random_state = 0)
  classifier.fit(X_train, y_train)
  ~~~
  
  Building an SVM (Not linearily seperable)
  =========================================
  
  Create classifer
  
  `kernal` : linear, ploy, rbf 
  
  ~~~ python 
  from sklearn.svm import SVC
  classifier = SVC(kernel = 'rbf', random_state = 0)
  classifier.fit(X_train, y_train)
  ~~~
'''
tags: []
isStarred: false
createdAt: "2017-06-07T16:04:36.164Z"
updatedAt: "2017-06-07T19:08:19.999Z"
