---
title: "Thesis Overview"
subtitle: "Draft material"
layout: post
tags: ["phd", "invasive", "overview"]
---

Population dynamics of interacting invasive species in New Zealand forests. !<--[Here are some other options (coming)]()-->

## Thesis Overview

The general overview and structure is below currently but as the documents increase I will convert this into a bookdown document (and a real book) for my thesis. The key research objectives of this thesis are [here](https://davan690.github.io/2019-05-01-Key-thesis-objectives) for comment.

1. To build a research synthesis database of the theoretical relationships proposed in over 100 years of conservation research in NZ and the experimental work supporting these models. We need a uniform set of models and notation to develop from (e.g. Holland et al. 2015; Ruscoe et al. 2005; Choquenot & Ruscoe 2000; Ruscoe et al. 2004; King et al. 2003).

2. Use a combined theoretical modelling and experimental approach to clarify the outcomes of invasive species control in three large-scale ecological datasets (Chapters 2,3,4). I build and test previous research that has attempted to characterize these interactions between invasive species, resources and native species in New Zealand Forests (Choquenot & Ruscoe 2000 + +).

3. Advances in ecological modelling tools have opened up opportunities to assess and parameterize theoretical models from observational data (King 2012). Along with this comes the correct partitioning of observation and process error. We use statistical software such as JAGS (Plummer 2010), WinBUGS (Suess & Trumbo 2010) and STAN (STAN development Team 2015) to develop the understanding of how these sources of error may effect the goals and targets of conservation managers and researchers alike.

## Overall PhD

- Abstract: [coming]()
- Introduction: [coming]()
- Beech Forest Dynamics: [here](https://davan690.github.io/2019-05-02-beech-forest-pub-thesis)
- Mixed Forest Dynamics: [coming]()
- DOC paper: [coming]()
- Discussion: [coming]()

## Additional Chapters

- Reproducibility in science: *I have began a comprehensive guide [here](https://davan690.github.io/2019-05-08-reproducible-code)

## Supporting resources

Here is an [example](https://github.com/davan690/PestManagement/blob/master/README.md) individual based pest modelling This is a `repo` from a recent publication on dynamic pest management

# PhD thesis

<div class="post">
<h1>Draft publications and chapters</h1>{{This is a collection of my drafts and current working developments}}
<ul>
{% for post in site.tags["phd"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>
<hr>

In this thesis I will use observed data to build ecosystem models that allow researchers to directly quantify the interactions among invasive species (Peng 2015).

