---
title: "Data wrangling"
subtitle: "for stoat control in beech forest"
bibliography: Beech-forests.bib
type: post
tags: ["phd", "beech", "rmd", "RStudio", "invasive-spp", "general", "ecology", "thesis"]
image: /img/doc-image-logo.png
permlink: /beech-seed-wrangling.html
---

*Generally look at thesis drafts [here]("https://www.ssnhub.com/").*

This RMarkdown file is intend to be extended on the estimationg process for the different species in the Beech Forest model. These files are the supporting documentation for this paper. As have been doing this I have also realised that there are many more supporting documents coming in the future.

# Invasive species notes

<div class="post">
<ul>
{% for post in site.tags["invasive-spp"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

# Methods

{% for post in site.tags["beech-methods"] %}
  {{ post.title }} ({{ post.date | date_to_string }})
    {{ post.description }}
{% endfor %}

<div class="post">
<ul>
{% for post in site.tags["tools"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

# Current drafts

{%- include post-test2.nb.html -%}