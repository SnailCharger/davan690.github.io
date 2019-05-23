---
title: Bio-informatics workflow
subtitle: Notes from Kanwal et al. 2017
tags: ["workflow", "phd", "bioinformatics"]
layout: post
---

## My notes

<img src= "/img/workflow-pub1.png" />

*Investigating reproducibility and tracking provenance – A genomic workflow case study*

<img src= "/img/abstract1.png" />

This was the paper I was thinking about. A key few points are in the figures here.

#### General workflow

<img src= "/img/fig1-workflow.png" />

#### Bioinformatics

<img src= "/img/fig3-workflow.png" />

## Tutorials

I often work with colleagues in genetics and have done a small bit of work with [dartR]("https://cran.r-project.org/web/packages/dartR/"). Here is a very limited list of genetics resources for statistics. I am no way an expert with these packages or analyses but have a look here for some detailed resources and lab discussions with [Arthur Gorges](http://georges.biomatix.org/).

- [Monash Bio-informatics Platform](https://monashbioinformaticsplatform.github.io/): This is github repository with information for Monash bio-informatics team.

- [Workbook from compgenr package](https://al2na.github.io/compgenr/Genomics/)

- [Comparative Genomics workbook](https://isugenomics.github.io/bioinformatics-workbook/)

- [DartR Genomics workbook](https://cran.r-project.org/web/packages/dartR/vignettes/IntroTutorial_dartR.pdf)

- [R population genetics workbook](https://github.com/green-striped-gecko/PopGenReport/)

- [A reproducible course](https://nlm-repro.github.io/)

### GITHUB gems

- [bionix](https://github.com/PapenfussLab/bionix/): This is a a tool for reproducible bioinformatics that unifies workflow engines, package managers, and containers. It is implemented as a lightweight library on top of the Nix deployment system. BioNix is currently a work in progress.

**AND more**
- [https://github.com/davfre/RRIB]
- [https://github.com/seandavi/wdlRunR]
- [https://github.com/lmweber/cytometry-clustering-comparison]
- [https://github.com/nhoffman/bioscons]
- [https://github.com/NCBI-Hackathons/ContainerInception]
- [https://github.com/mibwurrepo/Microbial-bioinformatics-introductory-course-Material-2018]
- [https://github.com/imagejs/imagejs.github.com]
- [https://github.com/rabix/rabix]
- [https://github.com/nlm-repro/nlm-repro.github.io]

## News

 <div class="posts-list">
    {% for post in paginator.posts %}
    <article class="post-preview">
      <a href="{{ post.url | prepend: site.baseurl }}">
      <h2 class="post-title">{{ post.title }}</h2>
  
      {% if post.subtitle %}
      <h3 class="post-subtitle">
        {{ post.subtitle }}
      </h3>
      {% endif %}
      </a>
  
      <p class="post-meta">
        Posted on {{ post.date | date: "%B %-d, %Y" }}
      </p>
  
      <div class="post-entry-container">
        {% if post.image %}
        <div class="post-image">
          <a href="{{ post.url | prepend: site.baseurl }}">
            <img src="{{ post.image }}">
          </a>
        </div>
        {% endif %}
        <div class="post-entry">
          {{ post.excerpt | strip_html | xml_escape | truncatewords: site.excerpt_length }}
          {% assign excerpt_word_count = post.excerpt | number_of_words %}
          {% if post.content != post.excerpt or excerpt_word_count > site.excerpt_length %}
            <a href="{{ post.url | prepend: site.baseurl }}" class="post-read-more">[Read&nbsp;More]</a>
          {% endif %}
        </div>
      </div>
  
      {% if post.tags.size > 0 %}
      <div class="blog-tags">
        Tags:
        {% if site.link-tags %}
        {% for tag in post.tags %}
        <a href="{{ site.baseurl }}/tags#{{- tag -}}">{{- tag -}}</a>
        {% endfor %}
        {% else %}
          {{ post.tags | join: ", " }}
        {% endif %}
      </div>
      {% endif %}
  
     </article>
    {% endfor %}
  </div>
  
  {% if paginator.total_pages > 1 %}
  <ul class="pager main-pager">
    {% if paginator.previous_page %}
    <li class="previous">
      <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&larr; Newer Posts</a>
    </li>
    {% endif %}
    {% if paginator.next_page %}
    <li class="next">
      <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Older Posts &rarr;</a>
    </li>
    {% endif %}
  </ul>
  {% endif %}