---
<!-- layout: default -->
layout: page
title: Portfolio
---

  {% for portfolio in site.portfolio %}
  ![{{ portfolio.title }}]({{ site.baseurl }}/images/portfolio/{{ portfolio.image}})
    <h2>
    <a href="{% if portfolio.ext_url %} {{ portfolio.ext_url }} {% else %} {{ portfolio.url | prepend: site.baseurl }} {% endif %}" {% if portfolio.ext_url %}target="_blank"{% endif %}>
    <!-- <a href="{{ portfolio.url | prepend: site.baseurl }}"> -->
      {{ portfolio.title }}</a>
      {{ portfolio.excerpt }}
      </h2>
  {% endfor %}