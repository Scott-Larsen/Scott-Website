---
layout: page
title: Projects
---

<div class="projectBoxes">
  {% for portfolio in site.portfolio %}
  <div class="project">
  <a class="projectImg" href="{% if portfolio.ext_url %} {{ portfolio.ext_url }} {% else %} {{ portfolio.url | prepend: site.baseurl }} {% endif %}" {% if portfolio.ext_url %}target="_blank"{% endif %}><img src="{{ site.baseurl }}/images/portfolio/{{ portfolio.image}}" width="300" height="300" alt="{{ portfolio.title }}"></a>
  <h2>
    <a class="projTitle" href="{% if portfolio.ext_url %} {{ portfolio.ext_url }} {% else %} {{ portfolio.url | prepend: site.baseurl }} {% endif %}" {% if portfolio.ext_url %}target="_blank"{% endif %}>{{ portfolio.title }}</a>
      </h2>
      <div class="projSubTitle"> {{ portfolio.excerpt }} </div>
      </div>
  {% endfor %}
</div>