---
title: image options
subtitle: Draft
layout: post
tags: ["phd", "invasive", "overview", "thesis", "tools", "general"]
image: /img/tools.jpg
bigimg: /img/tools.jpg
permlink: /image-options-current.html
---

Here is a simple step through of my issues with adding and working with images in RStudio and all the different options to get the correct images and code into a manuscript or website.

It is all about `paths`...and links I think. And its taking me ages to get my head around it.

## This is what is working

Right now I have used...

## My notes

So at the moment I do this:

#### options as simple as

| RMarkdown                                                    | Markdown github                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ```# {r image-using-knitr}```                                | `![image](./_assets/img/compareGroups-gui-shot.jpg){ width=50% }` |
| -  r plot can be done with the plot data (summaries and reconstructions of the originally collected data) | - This needs to be a a set size to begin with and then easy to “slightly” shift |

But now that I have rendered my first publication in `bookdown` here it has become much easier to manage manuscript figures for size using the same two steps above.