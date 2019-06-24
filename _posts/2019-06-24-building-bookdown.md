---
title: "Bookdown template"
subtitle: "My forked phd repo"
layout: post
image:  /img/centre-logo-white.jpeg
bigimg: /img/filing.jpg
tags: ["markdown", "website", "tools", "rmd", "jekyll", "TTS"]
permalink: /bookdown-template.html
---

This is a up and coming application of reproducible science using a combination of `git` and `R`

You can download the repository here from `RStudio`: https://github.com/rstudio/bookdown. It is quite easy to build this in Rstudio following the instructions in the Bookdown book .... believe it or not

### bookdown

[![Build Status](https://travis-ci.org/rstudio/bookdown.svg)](https://travis-ci.org/rstudio/bookdown)
[![Downloads from the RStudio CRAN mirror](https://cranlogs.r-pkg.org/badges/bookdown)](https://cran.r-project.org/package=bookdown)

<a href="https://bookdown.org/yihui/bookdown"><img src="https://bookdown.org/yihui/bookdown/images/logo.png" alt="bookdown logo" align="right" /></a>

A open-source (GPL-3) R package to facilitate writing books and long-form articles/reports with R Markdown. Features include:

- Generate printer-ready books and ebooks from R Markdown documents
- A markup language easier to learn than LaTeX, and to write elements such as section headers, lists, quotes, figures, tables, and citations
- Multiple choices of output formats: PDF, LaTeX, HTML, EPUB, and Word.
- Possibility of including dynamic graphics and interactive applications (HTML widgets and Shiny apps)
- Support for languages other than R, including C/C++, Python, and SQL, etc.
- LaTeX equations, theorems, and proofs work for all output formats
- Can be published to GitHub, bookdown.org, and any web servers
- Integrated with the RStudio IDE
- One-click publishing to <https://bookdown.org>

The full documentation is the **bookdown** book, freely available at <https://bookdown.org/yihui/bookdown>. You may see "Get Started" at <https://bookdown.org/home/about/> to know how to get started with writing a book. The source of the **bookdown** book (and a complete working example) can be found in [inst/examples/](https://github.com/rstudio/bookdown/tree/master/inst/examples) of this repo. See <https://bookdown.org> for more information and featured books. You are welcome to send us feedback using [Github issues](https://github.com/rstudio/bookdown/issues) or ask questions on [StackOverflow](http://stackoverflow.com/questions/tagged/bookdown) with the `bookdown` tag.

## My notes

My simple steps:

1. Fork the simple [bookdown](https://bookdown.org/home/about/) template for Jekyll [here](https://bookdown.org/home/about/)
2. Create a`gh-pages` branch
3. Publish under www.ssnhub.com/“new project” following the `settings` section of your github repository

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

