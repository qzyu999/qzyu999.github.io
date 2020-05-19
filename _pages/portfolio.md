---
layout: page
title: Portfolio
nav_order: 2
permalink: /portfolio/
# Reference: https://www.thebalancecareers.com/how-to-write-about-me-page-examples-4142367
---
# Portfolio
1
{% for staff_member in site.staff_members %}
  <h2>
    <a href="{{ staff_member.url }}">
      {{ staff_member.name }} - {{ staff_member.position }}
    </a>
  </h2>
  <p>{{ staff_member.content | markdownify }}</p>
{% endfor %}

2
{% for project in site.portfolio %}
  <h2>
    <a href="{{ project.url }}">
      {{ project.name }} - {{ project.context }}
    </a>
  </h2>
  <p>{{ project.content | markdownify }}</p>
{% endfor %}
