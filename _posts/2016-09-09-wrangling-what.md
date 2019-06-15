---
layout: post
title: "Wrangling data"
subtitle: "An important and timely exercise"
image: /img/background-image.jpg
bigimg: /img/background-image.jpg
permalink: /wrangling.html
---

When dealing with data in a project whether it is my personal research or a statistics project I always start by "wrangling" the data. What I mean by this is that I begin by just viewing and plotting the relationships that are easily observed in the data.

During this stage I often find and identify many of the key challenges of a project at this time. To the point where I often say to colleages that this stage of the research path can take up to 90% of the total time needed to clean and analysis the data.

Overall, I always run following code at the beginning of any project:

```{r}
# packages
library("tidyverse")
library("ggplot2")

# view data structure
glimpse(data)
```

**Key resource**: [R for data science](https://r4ds.had.co.nz/wrangle-intro.html)

## Tutorials

This is a section of the website where I will extend on other open-source science projects to build a collection of resources to help other researchers.

##### External info

- [R4DS wrangling intro](https://r4ds.had.co.nz/wrangle-intro.html)

##### Internal info

## My notes

For my PhD I will use this approach to all my research questions in combination with a [reproducible workflow](https://www.github.com/davan690/reproducible-guidebook/)