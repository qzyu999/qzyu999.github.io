---
layout: default
name: Low Birthweight and Heart Disease Prediction Analytics
date: 2019-12-17
context: Analysis of Categorical Data, UCD
toc: true
toc_sticky: true
toc_label: "Table of Contents"
toc_icon: "cog"
excerpt_separator: The final project for the Analysis of Categorical Data (STA 138) course, utilizing logistic regression and Poisson regression.
teaser: /assets/img/plots_health_proj.JPG
gallery:
  - url: /assets/img/plots_health_proj.JPG
    image_path: /assets/img/plots_health_proj.JPG
    alt: "Exploratory plots to visualize the data with transformations."
  - url: /assets/img/residuals_health_proj.JPG
    image_path: /assets/img/residuals_health_proj.JPG
    alt: "Analysis of different residuals."
  - url: /assets/img/coef_health_proj.JPG
    image_path: /assets/img/coef_health_proj.JPG
    alt: "Resulting prediction of coefficients."
---
# Low Birthweight and Heart Disease Prediction Analytics

Two different datasets were studied in the final project for an Analysis of Categorical Data (STA 138) course at the University of California, Davis with Prof. Burman. The first dataset consisted of predictors and a binary response variable. The second dataset consisted of predictors and a count response variable. The former was modeled using Logistic Regression, and the latter was modeled using Poisson Regression. Different statistical summaries were performed on both datasets, along with an analysis of which variables would be best suited to be used as predictors. Scatter plots and box plots were used to analyze relationships between possible predictors and the response variables. Goodness-of-Fit tests were done using the Likelihood Ratio statistic. Backward Stepwise Regression was the primary tool for selecting a final model, utilizing the AIC criterion as the metric. Residuals were calculated using deviance and Pearson residuals, including their standardized versions. An analysis of the final model consisted of examining the final predictors and the interaction terms in relation to the variable definitions given through the dataset. The final part of the report consisted of a discussion of the main points such as possible assumption violations and data errors, and a conclusion on what sort of possible steps could be taken if there were more available time. This last part included the possibility that a certain model was not appropriate for the data, given assumptions that the model is based upon.

[Link to project](https://github.com/qzyu999/analysis-of-categorical-data-ucd-fall-18/blob/master/project/proj_pdf.pdf)

{% include gallery caption="Plots from the project include (1) exploratory plots to visualize the data with transformations, (2) analysis of different residuals, (3) resulting prediction of coefficients." %}
