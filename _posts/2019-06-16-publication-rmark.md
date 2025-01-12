---
title: Journal of Applied Ecology
subtitle: A simple publication template
type: post
image: /img/tools.jpg
bigimg: /img/first-image1.png
tags: ["markdown", "website", "tools", "rmd"]
permalink: /typora-blogging.html
---

This is a simple blog with the RMarkdown code explained for a Journal of Applied Ecology manuscript. I would love any comments on how to make this better from anyone who has more experience.

```{r var-yaml-code, eval=FALSE, include=FALSE}
#     theme: cerulean
#     csl: mee.csl

# bibliography: references.bib
  # html_document:
  #   fig_caption: yes
  #   highlight: pygments
  #   number_sections: no
  #   theme: cerulean
  # pdf_document:
  #   fig_caption: yes
  #   keep_tex: yes
  #   number_sections: yes
  # word_document: default
  
```

```{r enviroment, include=FALSE}
# libraries
  library(tidyverse)
  library(lubridate)
  library(jagsUI)
  library(knitr)
  library(gridExtra)
  library(extrafont)
  library(gdata)

# sorting fonts
  windowsFonts()
  loadfonts(device = "win")
  
# this just simply reduces long name to TIMES as in code below
  windowsFonts(Times=windowsFont("TT Times New Roman")) 
  
# devtools::install_github("cboettig/knitcitations@v1")
  library(knitcitations); cleanbib()
  cite_options(citation_format = "pandoc", check.entries=FALSE)
  library(bibtex)
```

## Publishing notes

Journal choice: [Journal of Applied Ecology](http://www.journalofappliedecology.org/view/.../authorGuideline.html)

- [Author Guidelines](http://mc.manuscriptcentral.com/jappl-besjournals)
  - A research **"article"** should not exceed **7000** words (the word count is inclusive of all parts of the manuscript, including the title page, abstract, references, table and figure legends, but excluding files uploaded as Supporting Information). See Manuscript specifications below.

- [Assistant editor's email](admin@journalofappliedecology.org)

- [Submission checklist](https://besjournals.onlinelibrary.wiley.com/hub/journal/13652664/about/author-guidelines#quickchecklistinitialsubmission)

##### Title page

##### Abstract

##### Keywords

##### Introduction

##### Materials and methods

##### Results

##### Discussion

##### Conclusions (optional)

##### Authors’ contributions

##### Acknowledgements (optional)

##### Data accessibility

##### References
