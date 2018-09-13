---
layout: post
title: "Will machine learners be as significant as their overall performance?"
date: 2018-09-13 13:09:02
categories: [bioinformatics]
tags: [machine learning]
---

Comparing machine learning models entails comparison of their overall performance.
Such performance takes into consideration different metrics.

* These metrics showcase the amount of statistical power a model ranks against others
   - Accuracy score
   - Significance score
   - F1 statistics
   - Feature importance score
   - Area under the ROC curve
   - Recall/Precision ratio
   - Specificity/Sensitivity ratio
   - Confidence intervals at 95%
   - Chi-squared, Kappa & false discovery rates
   - Positive & negative likelihood ratio
   - Precision & prevalence 
   - Divergence score
   - Miss rates & false negative

Accordingly, in the scatterplot below, I show a clear linearity between increased accuracy predicting a machine learning class and the significance of the classification. 
This significance consider how much chance is involved in predicting randomly one class as the correct class.

![Performance scatterplot](/assets/2018/performance.png)


