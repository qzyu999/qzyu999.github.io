---
layout: default
name: Nutrition Analysis
date: 2019-06-10
context: Multivariate Data Analysis, UCD
toc: true
toc_sticky: true
toc_label: "Table of Contents"
toc_icon: "cog"
excerpt_separator: The final project for the Multivariate Data Analysis (STA 135) course, utilizing principal component analysis (PCA) and linear discriminant analysis (LDA).
#header:
#  teaser: /assets/img/lda_plot_nut_proj.JPG
gallery:
  - url: /assets/img/scree_plot_nut_proj.JPG
    image_path: /assets/img/scree_plot_nut_proj.JPG
    alt: "Scree plot and proportion of variance plot."
  - url: /assets/img/beef_vege_biplot_nut_proj.JPG
    image_path: /assets/img/beef_vege_biplot_nut_proj.JPG
    alt: "Biplot of beef and vegetable data."
  - url: /assets/img/lda_hist_nut_proj.JPG
    image_path: /assets/img/lda_hist_nut_proj.JPG
    alt: "Stacked histogram of the LDA values for the beef and vegetable groups."
---
# Nutrition Analysis

This was an individual project for the Multivariate Data Analysis (STA 135) class from the University of California, Davis with Prof. Li. The programming analysis was done using R. In the project, a nutritional dataset selected from online with thousands of observations divided into various food groups was utilized. Each observation consisted of columns that described the various nutrient contents for 100 grams of a given food (e.g., Australian Wagyu Steak, grilled beef patty, etc.). Then performed multivariate analysis comparing the food groups beef and vegetable products. The different methods included simultaneous confident intervals using Hotelling’s T-squared and Bonferroni’s corrected method, Hotelling’s two-sample test, principal component analysis (PCA), and linear discriminant analysis (PCA). The analysis was compiled into a report that summarized the data, described the process of analysis, along with interpretations and conclusions of the results. Final grade, 100%.

{% include gallery caption="Plots from the project include (1) scree plot and proportion of variance plot, (2) biplot of beef and vegetable data, (3) stacked histogram of the LDA values for the beef and vegetable groups." %}
