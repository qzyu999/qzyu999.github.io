---
layout: default
name: Country Fertility and PPgdp Analytics
date: 2017-10-15
context: Regression Analysis, UCD
toc: true
toc_sticky: true
toc_label: "Table of Contents"
toc_icon: "cog"
excerpt_separator: The first project for the Regression Analysis (STA 108) course, utilizing linear regression.
#teaser: /assets/img/plots_health_proj.JPG
#gallery:
  - url: /assets/img/sta_108_proj_1_img_1.JPG
    image_path: /assets/img/sta_108_proj_1_img_1.JPG
    alt: "Fitted line through the predictor and response variables along with confidence intervals."
#  - url: /assets/img/residuals_health_proj.JPG
#    image_path: /assets/img/residuals_health_proj.JPG
#    alt: "Analysis of different residuals."
#  - url: /assets/img/coef_health_proj.JPG
#    image_path: /assets/img/coef_health_proj.JPG
#    alt: "Resulting prediction of coefficients."
---
# Country Fertility and PPgdp Analytics

This was the first project for Linear Regression (STA 108) with Prof. Chen at the University of California, Davis. A set of data which had an $$x$$ and $$y$$ variable which corresponded with country GDP per person plotted against the fertility rate for that country was given. The goal was to find the best way to transform the data such that it could obtain an ideal $$R^2$$ value. Despite the ideal transformation appearing to be the log of both the $$x$$ and $$y$$ plotted against each other, it was later understood that the best possible $$R^2$$ could be found using only $$1/log(x)$$ against the untransformed $$y$$ data.

After transforming the data, it was possible to reattempt the regression analysis on the changed version of the data, allowing for confidence intervals to be developed and retested back on the original data.

[Link to project (RMD only)](https://github.com/qzyu999/regression-analysis-ucd-fall-17/blob/master/project_1.pdf)

{% include gallery caption="Plot from the project includes the fitted line through the predictor and response variables along with confidence intervals." %}
