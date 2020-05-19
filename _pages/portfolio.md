---
layout: page
title: Portfolio
nav_order: 2
permalink: /portfolio/
# Reference: https://www.thebalancecareers.com/how-to-write-about-me-page-examples-4142367
---
# Portfolio

## Featured Projects
{% assign sorted_pages = site.featured_portfolio | sort:"order" %}
{% for project in sorted_pages %}
  <h2>
    <a href="{{ project.url }}">
      {{ project.name }} - {{ project.context }}
    </a>
  </h2>
  <p>{{ project.excerpt_separator | markdownify }}</p>
{% endfor %}

## Latest Projects
{% assign sorted = site.portfolio | reverse %}
{% for project in sorted %}
  <h2>
    <a href="{{ project.url }}">
      {{ project.name }} - {{ project.context }}
    </a>
  </h2>
  <p>{{ project.excerpt_separator | markdownify }}</p>
{% endfor %}
