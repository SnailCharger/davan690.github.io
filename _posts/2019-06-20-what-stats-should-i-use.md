---
title: "What statistics should I use?"
layout: post
tags: ["general", "overview", "website", "tools", "searching", "research"]
image: /img/tools.jpg
bigimg: /img/aboutme-image.jpg
permalink: /searching-research.html
---

<a href="{{ site.github.repository_url }}/tree/master/{{ page.relative_path }}" align = "center">Help make it better here</a>

![1560990182973](../img/1560990182973-1560990209718.png)

I have always found this hard to work out because I never report what I really should because I am never sure what the rules are.

## Tutorials

### Reporting statistics in Ecology

- 

### Reporting bayesian statistics

- 

## My notes

<div class="post">
<ul>
{% for post in site.tags["tools"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>