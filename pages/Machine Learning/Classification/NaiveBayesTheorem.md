---
title: Naive Bayes Theorem 
sidebar: machine_sidebar
permalink: bayes.html
folder: Machine Learning
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Bayes Theorem 

$$ P(A|B) = \frac{P(B|A)*P(A)}{P(B)} $$

Probabilty that A occurs given B has occured P(A &#124; B)

The Bayes Theorem is a method of finding what the proababilty is of something ocuuring (A) given that something else has just occured (B).

## Example for Bayes Theorem 

Two machines produce wrenches. We know that:

- Machine 1 : Produces 30 Wrenches Per Hour
- Machine 2 : Produces 20 Wrenches Per Hour
- 1% of all wrenches are defective, where 50% of the wrenches that are defective are from machine 1 and 50% from machine 2.

**Question**: What is the probabilty that a part produced by machine 2 is defective?

- P M1) = 30/50 = 0.6
- P (M2) = 20/50 = 0.4
- P (D) = 0.01 
- P (M1 &#124; D) = 0.5 and P(M2 &#124; D) = 0.5
- P (D &#124; M2) = ??? (Question statement)

**Answer**:

$$ P(D | M2) = \frac{P(M2 | D)*P(D)}{P(M2)} = \frac{ 0.5 * 0.01}{0.4} = 0.0125 $$

## Naive Bayes Classifier




## Naive Bayes Theorem in Python

Use the classification template to set everything up.

Create the classifier and set it up

``` python 
from sklearn.naive_bayes import GaussianNB
classifier = GaussianNB()
classifier.fit(X_train, y_train)
```
run code...

