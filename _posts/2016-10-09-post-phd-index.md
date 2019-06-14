---
layout: post
title: Phd posts
subtitle: Building my resources
tags: ["general", "overview", "website", "resources", "tools", "phd"]
image: /img/filing.jpg
permlink: /resources/
---

As I build my Phd I am simulatiously building a website of resources and references to support reproducible science in New Zealand Predator Control.

## Invasive species notes

<div class="post">
<ul>
{% for post in site.tags["invasive-spp"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

## Thesis info

<div class="post">
<ul>
{% for post in site.tags["phd"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

## My coding/tool notes

<div class="post">
<ul>
{% for post in site.tags["tools"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>







