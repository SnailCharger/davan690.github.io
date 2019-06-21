---
title: "Data wrangling"
subtitle: "for stoat control paper"
bibliography: Beech-forests.bib
type: post
tags: ["phd", "beech", "rmd", "RStudio", "invasive-spp", "general", "ecology", "thesis"]
image: /img/doc-image-logo.png
permlink: /beech-seed-wrangling.html
---

Below I have attempted to incorporate the known dynamics of beech forests into the estimation process of beech seed. Most of this focuses on the possibility that differences/or lack of, is not a fact of stoat control but in fact differences in un-measured variables between the sites. I believe that this is not the case because:

1. Differences are within the range of other publication.

2. Working on this... 

 on the estimating process for the different species in the Beech Forest model. These files are the supporting documentation for this paper. As have been doing this I have also realised that there are many more supporting documents coming in the future.

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

{% include outputs.html %}