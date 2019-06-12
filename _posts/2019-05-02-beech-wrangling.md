---
title: "Data wrangling"
subtitle: "for stoat control in beech forest"
bibliography: Beech-forests.bib
type: post
image: /img/doc-image-logo.png
permlink: /beech-seed-wrangling.html
---

New Zealand beech forests exhibit boom-bust dynamics [below](https://www.osnz.org.nz/sites/osnz.org.nz/files/DOC%20brochure%20battle%20for%20our%20birds.pdf). Where, beech trees mast in spatial synchronised but annually variable years dependant [@wardle1991]. Mice populations have invaded these systems and studies have shown that populations response numerically to changes in resources (beech seed) and mice have been modelled under a range of both functional and numerical responses [@king1983]. ![DOC diagram of Beech Masting](/img/doc-mast-diagram.PNG)

This short report investigates the possible bias in the estimation of available seed to the raw data commonly used for estimation of food availability [@ruscoe2005]. This is important because the following bias are known and need to be accounted for before analysing data.

1. Seeds without the kernel have no energy value and need to be removed [here](#Seed Measurement).

2. Different beech species produce different sized seeds and this has an effect on the "available seed".

3. As our models build in complexity we will include a variety of food resources and therefore need to model these relationships in the future

# Introduction and Methods

*Generally look at thesis drafts [here]("https://www.ssnhub.com/").*

This RMarkdown file is intend to be extended on for different species of trees, fruit and seed. These files are the supporting documetation to the data-wrangling code in the Beech forest manuscript [here]("https://www.ssnhub.com/invasive-species-research.html/").

Bbut there is also many other supporting resources and less formal tutorials on my [website](https://www.ssnhub.com) and the feed below:

# Invasive species notes

<div class="post">
<ul>
{% for post in site.tags["invasive-spp"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

## Meta-data

### Contents

- [Current draft](https://www.dropbox.com/home/phd-drafts-anthony/beech-forest-dynamics/drafts/Davidson_2019_BeechForest.html)

- [Style sheet](https://www.dropbox.com/home/phd-drafts-anthony/beech-forest-dynamics/Styles_manual_sheet.md/)

- [Introduction](https://www.dropbox.com/sh/5h4mp67p7u6t1lj/AAAQVKS4qnvu2oQLu53JQUofa?dl=0)

- [Bayesian methods](https://www.dropbox.com/home/phd-drafts-anthony/beech-forest-dynamics/A1_full_bayesian_model.pdf)

- [Figures](https://www.dropbox.com/home/phd-drafts-anthony/beech-forest-dynamics/figs)

- [Functional response](https://www.dropbox.com/home/phd-drafts-anthony/beech-forest-dynamics/Davidson_2019_BeechForest_Appendix.pdf)

- [References](): *coming online soon*

All other data and resources to render project from raw data (copied from my private GIT repository) can be found on [dropbox](https://www.dropbox.com/home/phd-drafts-anthony) but will be available here when I have incorporated the co-authors feedback

<div class="post">
<ul>
{% for post in site.tags["invasive-spp"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>
