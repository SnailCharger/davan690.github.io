---
title: "Jekyll vs Windows"
subtitle: "What is it all about?"
layout: post
bigimg: /img/jekyll-fill.jpg
image: /img/jekyll-fill-sq.jpg
tags: ["compile", "tools", "general"]
permalink: /jekyll-in-windows.html
---

IMPOSSIBLE...but i need to do it so here goes:

## Tutorials

- [Jekyll documents](https://jekyllrb.com/docs/installation/windows/)

"While Windows is not an officially-supported platform, it can be used to run Jekyll with the proper tweaks. This page aims to collect some of the general knowledge and lessons that have been unearthed by Windows users."

- [Notes for a MAC user](https://www.alspur.com/moving-to-blogdown/)

- [Andy's notes]()
These notes are great. I have extended them below but all credit to [Andy]() and other `knitr` developers (...)

- But I am still left with the issue of not being able to run jekyll and gems on my local machine. So this is how I have done it.

## My notes

1. Install ruby but make sure it is x86 not x64 that can cause issues  
2. INstall jekyll
3. Install bundler
4. 

## Below is for RMarkdown files

### Andy's blog post modified by me
* writing posts in `Rmarkdown`
* converting posts to markdown from R
* push to Github where Jekyll renders the markdown
* organising all as an RStudio project 

## Desired outcome

I wanted to be able to write about R related things without having to copy and paste code, figures or files. I use [Rmarkdown](http://rmarkdown.rstudio.com/) and [knitr](http://yihui.name/knitr/) for research so wanted to use them. As many others have done before me I played around with a wordpress site elsewhere but struggled to create a workflow that wasn't to time expensive.

Initially I tried seeing if I could create posts using `RMarkdown` and put them into that wordpress blog. A brief search revealed that was not straightforward and that Jekyll was the way to go.  

## Result

I can write posts in RMarkdown (`.Rmd`) and run an R function to convert them to markdown (`.md`). 

- The blog is hosted for free on [Github](https://github.com/) (you get one free personal site). 

- The site is created using [Jekyll](http://jekyllrb.com/) on Github, so I didn't need to install Jekyll or Ruby. 

- I simply edit files locally, then commit and push to Github. 

- I manage the site as an [RStudio](http://www.rstudio.com/products/RStudio) project, enabling me to edit text, keep track of files and interact with Git all from one interface.

## Method

### creating Jekyll site on Github

I used Barry Clarks amazing [Jekyll-Now repository](https://github.com/barryclark/jekyll-now) which you can fork directly from Github and start editing to customize. He gives excellent instructions. What attarcted me to it was that it takes a matter of minutes to set up initially and if you decide you don't like it you can just delete.  

Thanks to Jan Gorecki whose answer on [stackoverflow](http://stackoverflow.com/a/26703757/1718356) pointed me in this direction and I've copied some extra features like the Links and Index pages from his [site](https://github.com/jangorecki/jangorecki.github.io).  

### enabling editing of the site from RStudio

I cloned the Github repository for my site using RStudio :

* File, New project, Version control, Clone git
* Repo URL : https://github.com/AndySouth/andysouth.github.io
* Project directory name : andysouth.github.io

### setting up so that I can write the posts in RMarkdown
This was the tricky bit for me. I followed inspiration from [Jason Bryer](http://jason.bryer.org/posts/2012-12-10/Markdown_Jekyll_R_for_Blogging.html) and [Jon Zelner](http://www.jonzelner.net/jekyll/knitr/r/2014/07/02/autogen-knitr/). I had to tweak them both, the relative paths of figures was my main stumbling block. This was partly because I'm running windows and I couldn't run the shell scripts that they created. Instead I just run an R function [rmd2md](https://github.com/AndySouth/andysouth.github.io/blob/master/rmd2md.r) which is much the same as Jason's with some edits to paths and jekyll rendering.

Jason's function searches a folder that you specify for `.Rmd` files and then puts `.md` files into another folder. I set this up so that any plots are put into a third folder. Thus in the root of my site includes these 3 folders.

| Folder |     | Contents |
| ------ | --- | --- |
| _Rmd   |  | RMarkdown files that I edit |
| _md    |  | md files created by RMarkdown |
| figures |  | plots created by any chunks of R code |

This then means that any R plot is automatically generated, saved as a png and it's address is written into the md document so that the plot is displayed in the blog. This is shown in a simple example below that queries the WHO API to get the number of cases of one of the forms of sleeping sickness in 2013.

```{r, 14-12-10-rworldmap, hide=TRUE, warning=FALSE, message=FALSE, echo=TRUE}
code <- "NTD_4"
year <- 2013
url <- paste0('http://apps.who.int/gho/athena/api/GHO/',code,'.csv?filter=COUNTRY:*;YEAR:',year)
#read query result into dataframe
dF <- read.csv(url,as.is=TRUE)
library(rworldmap)
sPDF <- joinCountryData2Map(dF, nameJoinColumn="COUNTRY", joinCode="ISO3")
mapCountryData(sPDF,nameColumnToPlot="Numeric",catMethod="fixedWidth",mapRegion="africa", mapTitle="Gambian sleeping sickness cases in 2013")

```

The code syntax highlighting and dark grey background for both code and R text outputs are what come as the default with Jekyll-Now. I'm a little unsure about them. They seem to be specified in [_highlights.scss](https://github.com/AndySouth/andysouth.github.io/blob/master/_scss/_highlights.scss), perhaps I'll look at modifying later.

If you'd like to look here is the [entire source code](https://github.com/AndySouth/andysouth.github.io/) for the blog and for this [individual page](https://github.com/AndySouth/andysouth.github.io/blob/master/_rmd/2014-12-10-blog-setup.Rmd).