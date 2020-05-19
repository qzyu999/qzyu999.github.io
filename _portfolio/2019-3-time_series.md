---
layout: default
name: Time Series Analysis of Annual Temperature Anomalies
date: 2019-03-10
context: Applied Time Series Analysis, UCD
toc: true
toc_sticky: true
toc_label: "Table of Contents"
toc_icon: "cog"
excerpt_separator: The final project for the Applied Time Series Analysis (STA 137) course, utilizing ARIMA models, ACF and PACF plots, and spectral analysis.
teaser: /assets/img/pred_time_proj.JPG
gallery:
  - url: /assets/img/plots_time_proj.JPG
    image_path: /assets/img/plots_time_proj.JPG
    alt: "Exploratory plots that help to visualize the data."
  - url: /assets/img/pacf_time_proj.JPG
    image_path: /assets/img/pacf_time_proj.JPG
    alt: "Plots of Loess residuals for the final ARIMA(4,0,4) model."
  - url: /assets/img/periodogram_time_proj.JPG
    image_path: /assets/img/periodogram_time_proj.JPG
    alt: "Criterion function of Loess residuals with a smoothed periodogram."
---
This was a final group project for Applied Time Series Analysis (STA 137) from the University of California, Davis course taught by Prof. Burman. In the project, students were given time series data related to fluctuating annual temperatures. Together with a classmate, a report was written where all the methods and materials utilized were briefly introduced and explained. The results of the analysis using RStudio were then shared using various graphs and tables. Three possible ARIMA models were developed and reasons were given for why they were chosen. Reasons for model selection included: ACF, PACF, normality assumptions, p-values of coefficients, and periodograms through spectral analysis. Eventually, the final model was used to forecast future temperatures using linear extrapolation. The conclusion summarized the results of the analysis along with further interpretation about other possibilities that could have been approached given more time. Final grade, 100%.

{% include gallery caption="Plots from the project include (1) exploratory plots that help to visualize the data, (2) plots of Loess residuals for the final ARIMA(4,0,4) model, (3) criterion function of Loess residuals with a smoothed periodogram." %}
