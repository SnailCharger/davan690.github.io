---
title: "Zotero"
permalink: /zotero.html
layout: page 
header:
  overlay_color: "444444"
---

Ever since I made a reluctant transition from my trusty [Mendeley account]("https://mendeley.com") to a [Zotero database]("https://www.zotero.org/download/") I have saved the resources and blogs I have used along the way.

I originally moved to Zotero to for three main reasons:

1. Referencing in [Markdown]("https://en.wikipedia.org/wiki/Markdown") 

2. Work in software that fit an open-source format 

3. To finally wade through 10 years of saved and un-organised literature.

Here are some notes, handy blogs and references for using Zotero to help with my reproducible workflow.

## Simple stuff

I haven't developed any content for this section as the following resources cover much more than I ever could.

- http://r.iresmi.net/2019/02/02/bibliography-with-knitr-cite-your-references-and-packages/

And the extensions should be easy as a click of a few buttons... which some are:

- https://www.zotero.org/support/plugins#attachment_file_management

## More difficult stuff

There are many many extensions that we can use the `zotero database` structure for. Here are my notes to remind me how to do these.

### Citation styles

These are `.csl` scripts that define the style of the references in the document.

- [RMarkdown explaination]("https://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html")

- [csl repository]("https://github.com/davan690/styles")

### Saving pdfs somewhere

I have been through a few steps with this and now have come to "yet another" solution that avoids the issues over the past 6months.

#### webDAV and Zotero

This is one of the last things I need to get right in my Zotero database. I first found out what webDAV was and that this is a way to save anything. 

- [webDAV]()

- [Zotero support for webDAV]()

- [Box]()

**Box offers 5gb for free.**

A few months later I had sorted over 5gb of pdfs and the sync no longer works. But thats ok because it is spose to de depreciaded anyway (as far as this mentions).

### ZOTfile and Syncing

This add-on to Zotero is very helpful for tablets and syncing but I did not get this to work with a statfactory pdf reader. I am still working on this however now that webDAV.

- [What does the ZOT do?]()

- [Download ZotFile]()

- [Someones instructions](): They kinda worked??..

### Current solution

I finally found a great walk through for setting up pdf sync for free [here](). In short:

- [Step 1]()

- [Step 2]()

###  R packages

`citr`

`rbbt`