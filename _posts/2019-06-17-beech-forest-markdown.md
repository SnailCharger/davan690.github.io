---
title: "Displaying reports from RMarkdown in RStudio"
subtitle: "A temporary solution"
layout: post
tags: ["general", "overview", "website"]
image: /img/method-graf.jpg 
bigimg: /img/method-graf.jpg 
permlink: /beech-output-wrangle.html
---

Many of the options I wanted to work just dont!.

## Tutorials

*May 2019*
This is a simple vignette template rendered in RStudio as an html and copied to the `_includes` folder.

*June 2019*
BOOKDOWN all the way....

## My notes

AS I have been working on this I have now converted my projects into a bookdown project. This is helping me prepare to build my thesis in `bookdown` but also so that I can manage these documents better. I am currently writing a series of blogs on doing this below:

<div class="post">
<ul>
{% for post in site.tags["beech"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>