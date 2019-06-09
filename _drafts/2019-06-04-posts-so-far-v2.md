---
layout: post
title: My blogs
subtitle: This is where I will tell my friends way too much about me
use-site-title: true
---

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>