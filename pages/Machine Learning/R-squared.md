type: "MARKDOWN_NOTE"
folder: "ca803f222493d2f21dfd"
title: "R - Squared"
content: '''
  R - Squared 
  ===========
  
  Remeber: To find the line of best fit for a simple linear regression is SUN(y - y hat)^2 and we say that this is equal to the Sum of Squares of Residules (SSres).
  
  Now, instad of taking the line of best fit. Imagine drawing a line to represent the average of 'y'. This line can be found with the formula SUM(yi - yavg)^2 and is cqlled or equal to the totla sum of squares (SStot).
  
  R^2 = 1 - SSres/ SStot 
  
  R squared tells us how good our line is compared to the average line. Ideal scienario is that R^2 is equal to 1 or SSres is 0.
  
  
  Adjusted R Squared 
  ===================
  
  SSres --> MIn
  R^2 : GGoodness of fit
  
  Problem: Adding variables 
  
  R^2 will never decrease by adding a new variable. This is because the regression model will try and minimize SSres. Even if cannot do so it can make the 'b' coefficient 0. However, this will likely never happen since the model will find a very very small correlation between the independent variable and the dependent variable and make 'b' slightly greater than zero. Even though there is no actual correlation.
  This is a problem because we can't know if a independent variable actually has a correlation or not. And so this means that there is bias because it will always try and make R^2 larger.
  
  To solve this we use adjusted R Squared with the formula 
  
  Adj R^2 = 1 (1- R^2) (n-1)/(n - p -1)
  p: # of regressors
  n: sample size
  
  When adding regressors to the model p increases and when the bottom increases, the ratio will increase. This means that adj R squared has penalizing factor that makes it so that adding independent variables that don't help your model will instead hurt it.
  
  
  Linear Regression Coefficients 
  ==============================
  
  Magnitude: The size has no direct relationship to the impact of that coeffient. 
  Var 1 has mag = 5
  Var 2 has mag = 2
  Dependent var mag = 30 
  
  Increasing either var will increase the dependent variable, however increasing Var 1 by 5 won't have a greateer than if you did the same with Var 2 necessarily. 
  
  The correct way to determine the impact from the magnitude is to make sure to look at the independent variables in terms of the same unit as the dependent variable. We can say that per unit of Var 1 your dependent variable will increase by 5 units. 
'''
tags: []
isStarred: false
createdAt: "2017-06-05T18:20:57.798Z"
updatedAt: "2017-06-06T14:55:07.156Z"
