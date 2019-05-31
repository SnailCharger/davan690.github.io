---
title: "All blog posts so far..."
layout: page
image: /img/RStudio_library.jpg
permlink: /all-posts.html
---

This is a full list of all my blog posts so far. An easy way to find what I am on about is to use `ctrl + F` in chrome on this page and search....

  {% for post in site.posts %}
  <article>
    <h2>
      <a href="{{ post.url }}">
        {{ post.title }}
      </a>
    </h2>
    <time datetime="{{ post.date | date: "%Y-%m-%d" }}">{{ post.date | date_to_long_string }}</time>
    {{ post.content }}
  </article>
{% endfor %}