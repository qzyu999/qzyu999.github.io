---
layout: default
name: USA Spending Data Analytics for Business Owners
date: 2019-03-10
context: Adv. Stat Computing, UCD
toc: true
toc_sticky: true
toc_label: "Table of Contents"
toc_icon: "cog"
excerpt_separator: The final group project for the Adv. Stat Computing (STA 141C) course, utilizing big data.
#header:
#  teaser: /assets/img/lda_plot_nut_proj.JPG
gallery:
  - url: /assets/img/sta_141a_img_1.JPG
    image_path: /assets/img/sta_141a_img_1.JPG
    alt: "Example of an image from the frog category for image recognition."
  - url: /assets/img/sta_141a_img_2.JPG
    image_path: /assets/img/sta_141a_img_2.JPG
    alt: "Heatmap of the confusion matrix showing the actual versus predicted correct utilizing the Manhattan distance."
  - url: /assets/img/sta_141a_img_3.JPG
    image_path: /assets/img/sta_141a_img_3.JPG
    alt: "Plot of the error rates for each of k folds."
---
# Image Recognition Machine Learning/k-NN/Cross Validation

An image recognition group project was completed as part of the Statistical Data Science (STA 141A) course at the University of California, Davis, with Prof. Gupta. The goal was to create an Image Recognition program in R that could analyze 32×32 pixel images and predict their category. To predict an image’s category, each image was seen in an RGB color matrix, and the distance function was used to create a distance matrix between all of the pixels in a given image with every other image. To determine which class a particular image may belong to, k-Nearest Neighbors, or k-NN, was used to ‘vote’ for which class an image may belong to based on which images are most similar. Another step was to use Cross-Validation to train a training set. The Cross-Validation used 10-folds, where the training set was divided into 10 groups, and k-NN was performed on each of the folds to determine the accuracy for the different parameters of $$k = 1,\cdots,5$$, and the distance metric of either Euclidean or Manhattan distances. In the end, the optimal parameters were then used on the test set to determine the best accuracy possible that may be achieved.

[Link to project](https://github.com/qzyu999/fundamentals-of-statistical-data-science-ucd-spring-18/blob/master/final/Final-Project-STA-141A.pdf)

{% include gallery caption="Plots from the project include (1) example of an image from the frog category for image recognition, (2) heatmap of the confusion matrix showing the actual versus predicted correct utilizing the Manhattan distance, (3) plot of the error rates for each of k folds." %}
