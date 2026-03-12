---
layout: default
title: Teaching
nav_order: 4
---

# Teaching

## Instructor

{% assign courses = site.data.teaching | where:"type","instructor" %}
{% for course in courses %}
<div class="card border-light">
<div class="card-body"> 
  <h3 class="card-title">{{ course.title }}</h3>
  <h5 class="card-subtitle text-muted pb-2"> 
  {% for time in course.time %}
    {% if forloop.index < course.time.size %} 
    {{ time.time }},
    {% else %} {{ time.time }}
    {% endif %}
  {% endfor %}
  </h5>
</div>
</div>
{% endfor %}
