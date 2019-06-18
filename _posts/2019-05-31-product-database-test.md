---
layout: default
title: "Output of product database test"
tags: ["compile", "r", "rmd", "RStudio", "tools", "general"]
---
[{% for product in site.data.products %}
  {
    "id": "{{ product.id }}",
    "name": "{{ product.name }}",
    "description": "{{ product.description }}",
    "price": "{{ product.price }}"
  }{% if forloop.last == false %},{% endif %}
{% endfor %}]