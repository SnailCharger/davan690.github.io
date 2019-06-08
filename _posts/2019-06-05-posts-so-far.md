---
title: A description of my repositories
subtitle: This is most likely always out of date
permalink: /repos-i-collect.html/
layout: post
tags: ["phd", "general", "overview", "website"]
image: /img/repo-example-screenshot.jpg
---
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>