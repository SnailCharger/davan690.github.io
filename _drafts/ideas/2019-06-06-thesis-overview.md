---
title: Thesis Overview
subtitle: Draft
layout: post
tags: ["phd", "invasive", "overview", "thesis"]
---

This page is an overview/content page for my phd. Because I am publishing all my PhD resources and information into a web format as well. This is possible because of `.md` work.

## Status

### Drafts for comments

#### Supervisors

- Planning and overview of [thesis](https://www.ssnhub.com/2019-05-02-thesis-overview/)

#### Feedback

##### General feedback

## Working Title

*Population dynamics of interacting invasive species in New Zealand forests.*

## Thesis Overview

The general overview and structure is below currently but as the documents increase I will convert this into a [bookdown document](https://bookdown.org/) for my thesis. The key research objectives are:

1. To build a research synthesis database of the theoretical relationships proposed in over 100 years of conservation research in NZ and the experimental work supporting these models. We need a uniform set of models and notation to develop from (e.g. Holland et al. 2015; Ruscoe et al. 2005; Choquenot & Ruscoe 2000; Ruscoe et al. 2004; King et al. 2003).

2. Use a combined theoretical modelling and experimental approach to clarify the outcomes of invasive species control in three large-scale ecological data-sets (Chapters 2,3,4). I build and test previous research that has attempted to characterize these interactions between invasive species, resources and native species in New Zealand Forests (Choquenot & Ruscoe 2000 + +).

3. Advances in ecological modelling tools have opened up opportunities to assess and parameterise theoretical models from observational data (King 2012). Along with this comes the correct partitioning of observation and process error. We use statistical software such as JAGS (Plummer 2010), WinBUGS (Suess & Trumbo 2010) and STAN (STAN development Team 2015) to develop the understanding of how these sources of error may effect the goals and targets of conservation managers and researchers alike.

## Supporting resources

*Coming soon ...*

## Overall PhD

- Abstract: [coming]()
- Overview: *This page*
- Introduction: [coming]()
- Beech Forest Dynamics: [here](https://www.ssnhub.com/2019-05-03-beech-forest-objectives)
- Mixed Forest Dynamics: [coming](https://www.ssnhub.com/2019-05-03-mpd-forest-objectives)
- DOC paper: [coming]()
- Discussion: [coming]()

## PhD News

This is a collection of drafts and current developments

<div class="post">
<ul>
{% for post in site.tags["phd"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>