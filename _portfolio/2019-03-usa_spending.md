---
layout: default
name: USA Spending Data Analytics for Business Owners
date: 2019-03-10
context: Adv. Stat Computing, UCD
excerpt_separator: The final group project for the Adv. Stat Computing (STA 141C) course, utilizing big data.
#header:
#  teaser: /assets/img/lda_plot_nut_proj.JPG
gallery:
  - url: /assets/img/sta_141c_img_1.JPG
    image_path: /assets/img/sta_141c_img_1.JPG
    alt: "Geospatial plot showing the prevalence of the services sector by state."
  - url: /assets/img/sta_141c_img_2.JPG
    image_path: /assets/img/sta_141c_img_2.JPG
    alt: "Plot of California annual GDP with a red line highlighting the global financial crisis."
  - url: /assets/img/sta_141c_img_3.JPG
    image_path: /assets/img/sta_141c_img_3.JPG
    alt: "Top 25 weighted words gathered through text mining from the business category."
---
# USA Spending Data Analytics for Business Owners

This was a group final project for Adv. Stat Computing (STA 141C) at the University of California, Davis that was taught by a graduate student, Clark Fitzgerald. Our project analyzed the big data from usaspending.gov and created a platform from which potential business owners could understand their potential for finding contractual work with the federal government. Time series analysis was used to model future government spending for all 50 states. An ARIMA model was fit to each state where the AICc criterion was used to determine the optimal fit. Geo plotting was done with the Plotly package to create geographic heatmaps of the major business sectors using the NAICS code from the dataset. Various macroeconomic variables were plotted using ggplot2 and an API from the St. Louis Federal Reserve. Also, text mining was done on two different descriptive variables, where a weighted character vector was created using Natural Language Processing (NLP) techniques to determine a description of the business categories and awarding agencies for each state. Lastly, different machine learning algorithms were modeled to try and predict possible future spending for each state. This information was compiled in a report in a Google document where there was an abstract, introduction, methods section, results, conclusion, and a discussion section.

[Link to project](https://github.com/qzyu999/big-data-and-high-performance-statistical-computing-ucd-winter-19/blob/master/project/USA%20Spending%20Data%20Analytics%20for%20Business%20Owners.pdf)

{% include gallery caption="Plots from the project include (1) geospatial plot showing the prevalence of the services sector by state, (2) plot of California annual GDP with a red line highlighting the global financial crisis, (3) top 25 weighted words gathered through text mining from the business categorys." %}
