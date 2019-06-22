---
title: "Notes on NZ Beech forest dynamics"
subtitle: "A collection of grey information"
bibliography: Beech-forests.bib
type: post
tags: ["phd", "beech", "rmd", "RStudio", "invasive-spp", "general", "ecology", "thesis"]
image: /img/doc-image-logo.png
permlink: /beech-seed-dynamics.html
---

There are many many publications that explain beech forests. Generally, the overall understanding of beech forest dynamics could be summaries as:

## Contents

- [Publications](#Publications)
- [Grey literature]: NZ context
  - DOC
  - LandCare
  - Councils
  - Guiding companies
- [Biogeographical parameters]
  - Spatial variation
  - Locations
- [Temporal variation]
  - Annual trends
  - Seasonal trends

## Invasive species notes

<div class="post">
<ul>
{% for post in site.tags["invasive-spp"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

# Methods

Below I have attempted to incorporate the published population dynamics of beech forests into the estimation process of beech seed.

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

## Publications

- [Holland beech mast model](): This model builds a simple mast model for beech seed in the lower north island of NZ.

## Grey literature

Some of the most interesting literature is "grey" literature".

Weirdly, here is an interesting resource can be found from a guiding company.

![1560916992918](../img/1560916992918.png)

Screen shot of [guide landing page](http://www.routeguides.co.nz/) showing guided trails.