---
title: "DiffPrivML"
subtitle: "Differential Private Machine Learning"
author: Terence Tam
date: 2018-03-21 9:00:00
layout: post
header-img: "img/post-bg-06.jpg"
---

Machine learning algorithms collectively strive to extract population information and learn general patterns from data sets. The output of machine learning algorithms are generally trained models, where raw data points are distiled to far more compact forms that capture the essence of the origninal data. It is a type of summary aggregation in short that is no different than COUNT and SUM.

The release of these trained machine learning models, however, comes with a cost–individual data privacy. Oftentimes, machine learning models inadvertently give away information on individual data points used in the training data, even though these ML models are meant to release population information only.

To analyze and potentially solve this problem, one unified framework proposed by Cynthia Dwork’s paper is the $\epsilon$-differential private mechanism. This is a model that quantifies the degrees of privacy loss for a given data release system, and a privacy loss tolerance level as a parameter–$\epsilon$. A lot of theoretical research has been done on different ML models with regards to differential privacy, such as these research [here](https://arxiv.org/pdf/1412.7584.pdf), but not enough efforts are being done to apply these in practice.

Therefore, we developed a R package, diffPrivML, that aims to put these differential private enhanced ML algorithms in the hands of data practitioners. Just like how a unified framework is developed to measure differential privacy, diffPrivML is a precursor in standardizing a library of ML algorithms and workflows that have differential privacy baked in. End users do not need to worry about HOW to perturb the data to release their models; the ML algorithm itself makes the guarantee.

Please view the package [here](https://github.com/terencekwt/diffPrivML) on github.

## References

Geetha Jagannathan, Krishnan Pillaipakkamnatt, and Rebecca N. Wright.
  "A practical differentially private random decision tree classifier". In International
  Conference on Data Mining Workshops, pages 114–121, 2009.

Kamalika Chaudhuri, Claire Monteleoni, Anand D. Sarwate. "Differentially Private Empirical Risk Minimization".
  In Journal of Machine Learning Research 12 (2001) 1069-1109.

Jaideep Vaidya, Basit Shafiq, Anirban Basu, and Yuan Hong. "Differentially
  private naive Bayes classification." In Web Intelligence, pages 571–576, 2013.
  
Zhanglong Ji, Zachary C Lipton, and Charles Elkan. “Differential privacy and machine learning:
  A survey and review”. In: arXiv preprint arXiv:1412.7584 (2014).


