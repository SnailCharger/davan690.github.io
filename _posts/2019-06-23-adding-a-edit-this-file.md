---
title: "Bookdown cooking guide"
subtitle: "Working through some simple steps"
layout: post
image:  /_posts/figs/working-at-night.jpg
bigimg: /_posts/figs/working-at-night.jpg
tags: ["markdown", "website", "tools", "rmd", "jekyll", "TTS"]
permalink: /bookdown-template.html
---

[![Build Status](https://travis-ci.org/rstudio/bookdown.svg)](https://travis-ci.org/rstudio/bookdown)
[![Downloads from the RStudio CRAN mirror](https://cranlogs.r-pkg.org/badges/bookdown)](https://cran.r-project.org/package=bookdown)

<a href="https://bookdown.org/yihui/bookdown"><img src="https://bookdown.org/yihui/bookdown/images/logo.png" alt="bookdown logo" align="right" /></a>

A open-source (GPL-3) R package to facilitate writing books and long-form articles/reports with R Markdown.

## My notes

So once I had everything downloaded and ready to go I realised I wasn’t sure how to deal with rendering different bits’n’bobs of the “book”.

My simple steps:

1. From RStudio from the very start I can’t render `rmd` file from the simple `knit` button I am so used to![Screenshot](../img/index-issues-rstudio.png)
2. So I can look at it in `vs-code` quickly![1561348386533](../img/vs-code-rmd-file-view.png)
3. So first step is to work out rendering options for `RStudio`;
   1. `servr`
   2. `rmarkdown`
   3. `bookdown`
   4. `render`
   5. many many more....

### Extra note

If you have just cloned the `bookdown` template then you will need to create a new repository on `github` with the following commands:

“I still haven’t got this sorted yet”

```shell
# Sets the new remote
$ git remote add origin remote 
repository URL

# Verifies the new remote URL
$ git remote -v

# Pushes the changes in your local repository up to the remote repository you specified as the origin
$ git push origin master

```

### A “maybe” simpler way

A manual way to do this is to create the repository online and add `bookdown` manually then pull it down to your local computer like so:

1. Create new public repository ![1561346525125](../img/repo-example2.jpg)

2. Copy files from `bookdown` repository (locally or from web)![bookdown link](https://bookdown.org/yihui/bookdown/images/logo.png)

3. Clone new repository locally `git clone`![1561347003110](../img/bookdown-on-vs-code.png)

4. ``git` commit your life away

   ![1561347067642](../img/git-commit-image.png)

   

For my PhD I will need this to be compiled and build like this so I have set up the framework for this and the layout here in my repository:

And my first draft publication is also now in this format with all relevant information here

www.ssnhub.com/beech-forest-dynamics/

### Resources

I have written a series of blogs around this topic and will continue to build these resources as I come up against challenges in building and publishing my PhD in this format.

{% for post in site.tags["tools"] %} [{{ post.title }}](https://github.com/davan690/beech-forest-dynamics/blob/master/{{ post.url }}) ({{ post.date | date_to_string }})
{{ post.description }} {% endfor %}