---
title: Invasive Species Modelling
layout: page
tags: ["phd", "page-index"]
---

The New Zealand government set a "apollo shot" to make NZ free of mammalian predators by 2050. I believe that as part of this research it is essential that the information is made available to the general public as there are many volunteer community groups that may not have access or the time to collate and communicate the current understanding of mammalian predators in NZ.

# News

- [How NZ might make PFNZ happen](https://news.nationalgeographic.com/2016/07/new-zealand-invasives-islands-rats-kiwis-conservation/)

- [Enviroment guide](http://www.environmentguide.org.nz/issues/biodiversity/key-threats/invasive-species/)

- [NZ geographic PFNZ plan](https://www.wired.com/2016/07/new-zealand-plans-kill-non-human-invasive-mammals/)

<div class="post">
<ul>
{% for post in site.tags["beech"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

# Online resources

- [Predator-free NZ](https://predatorfreenz.org/)

- [DOC](https://www.bnz.co.nz/assets/business-banking/cards-payments/pdfs/doc-casestudy-flexipurchase.pdf)

- [Worst Invasive Species](https://www.worldatlas.com/articles/the-worst-invasive-mammal-species.html)

- [Wiki NZ invasive species](https://en.wikipedia.org/wiki/Invasive_species_in_New_Zealand#Mammals): This needs updating as it is missing a few species such as weasals?

# My notes

<div class="post">
<ul>
{% for post in site.tags["tools"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

# Thesis projects

<div class="post">
<ul>
{% for post in site.tags["phd"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

Please excuse any '404' errors as I am learning and working as I go. Using version control and git means that I am able to use other coders templates and test things out before committing.