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