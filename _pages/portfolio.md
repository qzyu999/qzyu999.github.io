---
layout: page
title: Portfolio
nav_order: 2
permalink: /portfolio/
# Reference: https://www.thebalancecareers.com/how-to-write-about-me-page-examples-4142367
---
# Portfolio

{% for staff_member in site.portfolio %}
  <h2>{{ staff_member.name }} - {{ staff_member.position }}</h2>
  <p>{{ staff_member.content | markdownify }}</p>
{% endfor %}
