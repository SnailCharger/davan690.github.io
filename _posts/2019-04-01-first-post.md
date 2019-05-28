---
title: The beginning
subtitle: Starting a website is a daunting process and I've tried many times but that is for another blog post
layout: post
tags: ["phd", "general", "overview", "website"]
image: /img/centre-logo-white.jpg
---

This website is a simple collection of detailed resources and information I use for my PhD work, as part of the statistics network and other research projects. 




I have needed an accessible location to store statistics and ecology resources for a while now and the combination of [Jekyll]("https://jekyllrb.com/") and [GitPages]("https://pages.github.com/") makes it the right time to work on it. I have always written personal notes on methods and techniques I use or recommend such as the [tidyverse]("https://www.tidyverse.org/learn/") approach or the [UBC]("https://stat545.com/") statistics course or the [markdown]("https://en.wikipedia.org/wiki/Markdown") script I am writing this post in. Now I work in Markdown almost exclusively it means these can easily be posted as blogs or webposts. Here is the [webpage]("https://davan690.github.io/") repository for more computer minded (open-source resources and my research), and a [facebook]("https://www.facebook.com/StatisticsNetwork/")/[twitter]("https://twitter.com/statistics_the/") feed for new blog posts about statistics and ecology (not all from me). Welcome to the "Pit of Success!" [Great meme from a talk Hadley Wickham gave last year](https://i.imgur.com/7J1bEaJ.mp4/)

<h1>Info so far</h1>
<div class="posts-list">
  {% for post in paginator.posts %}
<article class="post-preview">
  <a href="{{ post.url | prepend: site.baseurl }}">
  <h3 class="post-title">{{ post.title }}</h3>
  
  {% if post.subtitle %}
<h4 class="post-subtitle">
{{ post.subtitle }}
</h4>
{% endif %}
</a>
  
  <p class="post-meta">
  Posted on {{ post.date | date: "%B %-d, %Y" }}
</p>
  
  <div class="post-entry-container">
  {% if post.image %}
<div class="post-image">
  <a href="{{ post.url | prepend: site.baseurl }}">
  <img src="{{ post.image }}">
  </a>
  </div>
  {% endif %}
<div class="post-entry">
{{ post.excerpt | strip_html | xml_escape | truncatewords: site.excerpt_length }}
{% assign excerpt_word_count = post.excerpt | number_of_words %}
{% if post.content != post.excerpt or excerpt_word_count > site.excerpt_length %}
<a href="{{ post.url | prepend: site.baseurl }}" class="post-read-more">[Read&nbsp;More]</a>
{% endif %}
</div>
  </div>
  
  {% if post.tags.size > 0 %}
<div class="blog-tags">
  Tags:
  {% if site.link-tags %}
{% for tag in post.tags %}
<a href="{{ site.baseurl }}/tags#{{- tag -}}">{{- tag -}}</a>
{% endfor %}
{% else %}
{{ post.tags | join: ", " }}
{% endif %}
</div>
{% endif %}

</article>
{% endfor %}
</div>
  
{% if paginator.total_pages > 1 %}
<ul class="pager main-pager">
{% if paginator.previous_page %}
<li class="previous">
  <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&larr; Newer Posts</a>
  </li>
  {% endif %}
{% if paginator.next_page %}
<li class="next">
  <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Older Posts &rarr;</a>
  </li>
  {% endif %}
</ul>
{% endif %}