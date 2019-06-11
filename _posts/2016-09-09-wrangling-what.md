---
title: "Wrangling data"
subtitle: "An important and timely excersize"
permalink: /wrangling.html
layout: post
---

When dealing with data in a project whether it is my personal research or a statistics project I always start by "wrangling" the data. What I mean by this is that I begin by just viewing and plotting the relationships that are easily observed in the data.

During this stage I often find and identify many of the key challenges of a project at this time. To the point where I often say to colleages that this stage of the research path can take up to 90% of the total time needed to clean and analysis the data.

Overall, I always try and run the following code at the beginning of a project:

```{r}
# for each year calculate the cumulative number of seeds
seed.paper.1 <- seed.paper %>%
            group_by(grid, year) %>%
              mutate(cum.seed = cumsum(seedm2)) %>%
                filter(trip.no > 0) %>%
                  # arrange(grid, trip.no) %>%
                    subset(!(grid.id %in% c("R1", "R2")))
```

**Key resource**
[R for data science](https://r4ds.had.co.nz/wrangle-intro.html)

## Tutorials

This is a section of the website where I will extend on other open-source science projects to build a collection of resources to help other researchers.

##### External info

- [R4DS wrangling intro](https://r4ds.had.co.nz/wrangle-intro.html)

##### Internal info

## My notes

For my PhD I will use this approach to all my research questions in combination with a [reproducible workflow](https://www.github.com/davan690/reproducible-guidebook/)