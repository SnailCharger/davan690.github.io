---
title: Invasive Species Modelling
layout: page
---

The New Zealand government set a "apollo shot" to make NZ free of mammalian predators by 2050. I believe that as part of this research it is essential that the information is made available to the general public as there are many volunteer community groups that may not have access or the time to collate and communicate the current understanding of mammalian predators in NZ.

# Thesis

<div class="post">
<h1>Draft publications and chapters</h1>{{This is a collection of my drafts and current working developments}}
<ul>
{% for post in site.tags["phd"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

Please excuse any '404' errors as I am learning and working as I go. Using version control and git means that I am able to use other coders templates and test things out before committing.