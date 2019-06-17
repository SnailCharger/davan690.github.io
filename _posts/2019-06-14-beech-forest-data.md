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

This RMarkdown file is intend to be extended on the estimationg process for the different species of trees, fruit and seed. These files are the supporting documetation to the data-wrangling code in the Beech forest manuscript [here]("https://www.ssnhub.com/invasive-species-research.html/").

But there is also many other supporting resources and less formal tutorials on my [website](https://www.ssnhub.com) and the feed below:

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