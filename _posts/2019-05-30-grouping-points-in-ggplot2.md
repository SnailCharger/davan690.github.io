---
title: "Taking advantage of all the symbols in ggplot2"
layout: post
output:
  word_document: default
  html_document:
    df_print: paged
  pdf_document: default
image: /img/filing.jpg
permalink: /ggplot-symbols.html
---

There are a few things in R that I find are particularly frustrating. I guess this is the situation for any package or set of tools we choice to use as researchers. `ggplot symbols` hard to understand.

## My notes

For these notes I have used the same data as for my first data chapter of my PhD. This data will be available when I finalise the publication.

### `ggplot2` symbols


```r
# export .r code only
# knitr::purl("./Davidson_2019_BeechForest.Rmd")

# render draft to webpage
# rmarkdown::render(input = "Davidson_2019_BeechForest.Rmd")
# ,
#                   output_format = "html_document",
#                   output_file = "Davidson_2019_t.html")

#document global rules
knitr::opts_chunk$set(comment=NA,
                      fig.path = "./figs/",
                      echo=FALSE, 
                      include = FALSE,
                      fig.height=5.5, 
                      fig.width=12.5,
                      message=FALSE, 
                      warning=FALSE, echo=FALSE)
# how do I do this??
# ,eval = FALSE,include = FALSE

# libraries needed
source("./rcode/r-packages-needed.R", echo = FALSE)

# themes
# source("./Rcode/davidson-2019-theme.r", echo = FALSE)

#overall code
# source("./rcode/manuscript-source-code.R", echo = FALSE)
```




I have been writing my first paper for my PhD for a ridiculously long time and as I am finally finishing figures for the manuscript I have had huge issues trying to sort these symbols.

## My solution for this script

##### `aes(shape = Valley; colour = Control, fill = Rats)`

Overall the three factors plotted as colours looks like so:

![plot of chunk plot-1](/./figs/plot-1-1.png)

[Figure 1: Plot of the three different factors, each with two levels that I want to each have the following representative symbols](./figs/plot3-symbols.jpeg)



For the example above there are three factors (valley, control, rats) each has 2 levels. However, because we are missing some combinations we have a total of 6 treatments.



##### `aes(shape = Valley; colour = Control)`

To plot this I need to split the symbols. I have decided to do this as follows: `shape = Valley`; `colour = Control`; `fill = Rats`. And in ggplot2 this is wrapped with the `aes()` function.

![plot of chunk plot2-valley-shape](/./figs/plot2-valley-shape-1.png)

[Figure 2: PLots including shape for Valley but two different plots showing the different factors in Control and Rats factors](./figs/plot2-symbols.jpeg)

## `aes(shape = Valley; colour = Control, fill = Rats)`

And in ggplot2 this is wrapped with the `aes(shape = Valley; colour = Control, fill = Rats)` function. And then it looks like this:

![plot of chunk plot1-valley-contol-rats](/./figs/plot1-valley-contol-rats-1.png)

[Figure 3: Attempting to understand why the colouring is not working with fill](./figs/plot1alpha-symbols.jpeg)

**WHAT makes this such a hard question??**

But for some reason fill doesn't work the way I want with rings for rats! 

## Working out plots space

Working with factors below to check this is not the issue. In this case the issue is exactly that to do with the 8 grids and the 6 treatments across 20 time intervals. 

- I am confused about these replicates but none are as complex is what I have here.

## Solutions

1. First issue is that it is by grid not treatment

##### This is why?? I had a look at examples I could find that have done this and the following stack-exchange and other blogs helped to produce this:

EXEPT ONE [here](http://www.audhalbritter.com/complicated-figure/)

or a few more options... 

2. And it turns out you can do this by creating a dumby variable

3. Or change alpha to 0.5 so solid lines come up? 

4. Or us alpha as facet

5. Change size of some just slightly so can see black?


![plot of chunk working-plot1](/./figs/working-plot1-1.png)

## Resources

Dealing with factors can be hard in R and here are some resources for FACTORS in R:

- [A collection of scripts I use](https://github.com/davan690/usefulr/)

- [An .Rmd file for factoring](https://github.com/davan690/usefulr/tree/gh-pages/RMarkdown-vigettes)

- Simple example 1 [coming]

- Simple example 2 [coming]

- Complex fill solution [coming]


# The dreaded legend

Legends are really tricky to work out in ggplot I find. Manly for one reason, that they are directly linked to the data rather than manually entering it. Anyway here is my code to manually control the legend.



## Resources
