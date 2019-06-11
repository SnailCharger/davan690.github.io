---
title: New Zealand beech forests
subtitle: Draft
layout: post
tags: ["phd", "invasive", "overview", "beech", "mice", "thesis"]
---

This is just a simple template to help explain why and how my editing documents are layed out on the website.

## Status

*Here just gives an overview of the project*

### Drafts for comments

*These links take the user to either the raw files or the dropbox account they are stored in. If you are a collaborator you need to accept the invitation to share dropbox files and then these links will take you directly to the correct documentation.*

#### Feedback

*One of the things I find hardest about science is the writing. I am always open to comments and suggestions. If you would like to help feel free to comment and send me any comments however it works best for you*

##### Supervisors

*This section contains private links and other resources that will be avaible if we are collaborating. :)*

##### General

*Any comments on these sections are always welcome.*

##### Posts

*At the end of each post there is a button that takes the user directly to the GIThub file of the website. It is very helpful to commit changes here*

<div class="post">
<ul>
{% for post in site.tags["beech"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>

## Working Title

## Overview

## Contents

*coming online soon*

- [Current draft]()
- [Style sheet]()
- [Introduction]()
- [Bayesian methods]()
- [Figures]()
- [Functional response]()
- [References]()

All other data and resources to render the full project from raw data (copied from my private GIT repository) can be found on [dropbox](https://www.dropbox.com/home/phd-drafts-anthony) but will be available here when I have incorporated the co-authors feedback.