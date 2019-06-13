---
layout: post
---
{% for product in site.data.products %}
   <product>
      <id>{{ product.id }}</id>
      <name>{{ product.name }}</name>
      <description>{{ product.description }}</description>
      <price>{{ product.price }}</price>
   </product>{% endfor %}