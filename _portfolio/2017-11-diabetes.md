---
layout: default
name: Diabetes Prediction Analytics
date: 2017-11-15
context: Regression Analysis, UCD
toc: true
toc_sticky: true
toc_label: "Table of Contents"
toc_icon: "cog"
excerpt_separator: The final project for the Regression Analysis (STA 108) course, utilizing linear regression.
#teaser: /assets/img/plots_health_proj.JPG
gallery:
  - url: /assets/img/sta_108_proj_2_img_1.JPG
    image_path: /assets/img/sta_108_proj_2_img_1.JPG
    alt: "Table of models."
  - url: /assets/img/sta_108_proj_2_img_2.JPG
    image_path: /assets/img/sta_108_proj_2_img_2.JPG
    alt: "Table with best models for each criterion."
#  - url: /assets/img/coef_health_proj.JPG
#    image_path: /assets/img/coef_health_proj.JPG
#    alt: "Resulting prediction of coefficients."
---
# Diabetes Prediction Analytics

The final project for Linear Regression (STA 108) with Prof. Chen at the University of California, Davis. The course involved utilizing a set of data related to diabetes patients and identifying the different variables which best predicted that a person in the population would have diabetes. Doing this meant performing a transformation on an indicator variable with BoxCox and then regressing it on all the other variables. The data was then split into training and validation data for cross-validation. Techniques that were used included "best" subset, AIC, BIC, Cp, R squared, Adjusted R squared, SSE, and the forward stepwise procedure. Multiple models were created to test different prediction criteria, and in the end, a model was selected according to it having the lowest MSPR value. Most of the work was performed in RStudio, and a report of the data along with commentary was done using Microsoft Word.

[Link to project](https://github.com/qzyu999/regression-analysis-ucd-fall-17/blob/master/project_2.pdf)

{% include gallery caption="Plots from the project include (1) Table of models, (2) Table with best models for each criterion." %}
