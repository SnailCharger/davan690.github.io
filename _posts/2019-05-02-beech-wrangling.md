---
title: "Data Wrangling explaination"
author: "Anthony Davidson"
date: '2019-05-16'
output:
  html_document:
    df_print: paged
  html_notebook: default
subtitle: For Stoat control in Beech forest paper
bibliography: Beech-forests.bib
type: post
---

```{r global-options, message=FALSE, warning=FALSE, include=FALSE}
# export .r code only
# knitr::purl("./Davidson_2019_BeechForest.Rmd")

# render draft to webpage
# rmarkdown::render(input = "Davidson_2019_BeechForest.Rmd")
# ,
#                   output_format = "html_document",
#                   output_file = "Davidson_2019_t.html")

# compareGroups::cGroupsGUI(mtcars)
#document global rules
knitr::opts_chunk$set(comment=NA,
                      fig.path = "./figs/",
                      echo=TRUE, 
                      fig.height=6, 
                      fig.width=10,
                      message=FALSE, 
                      warning=FALSE)
# how do I do this??
# ,eval = FALSE,include = FALSE


```

# Overview

```{r eniviroment, message=FALSE, warning=FALSE, include=FALSE}
# libraries needed
source("./rcode/r-packages-needed.R", echo = FALSE)
source("./rcode/theme_raw_fig3s.r", echo = FALSE)
source("./rcode/davidson_2019_theme.r", echo = FALSE)
```

New Zealand beech forests exhibit boom-bust dynamics (Figure 1). Where, beech trees mast in spatial synchronised but annually variable years dependant [@wardle1991]. Mice populations have invaded these systems and studies have shown that populations response numerically to changes in resources (beech seed) and mice have been modelled under a range of both functional and numerical responses [@king1983]. 

This short report investigates the possible bias in the estimation of available seed to the raw data commonly used for estimation of food availability [@ruscoe2005]. This is important because the following bias are known and need to be accounted for before analysising data.

1. Seeds without the kernal have no energy value and need to be removed.

2. Different beech species produce different sized seeds and this has an effect on the "available seed".

3. As our models build in complexity we will include a variety of food resources and therefore need to model these relationships in the future

# Introduction and Methods

*Generally look at thesis drafts [here]("https://www.ssnhub.com/").*

This RMarkdown file is intend to be extended on for different species of trees, fruit and seed. These files are the supporting documetation to the data-wrangling code in the Beech forest manuscript [here]("https://www.ssnhub.com/invasive-species-research.html/").

Bbut there is also many other supporting resources and less formal tutorials on my [website](https://www.ssnhub.com) and the feed below:

# Invasive species notes

```{}
<div class="post">
<ul>
{% for post in site.tags["invasive-spp"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>
```

## Meta-data

### Contents

- [Current draft](https://www.dropbox.com/home/phd-drafts-anthony/beech-forest-dynamics/drafts/Davidson_2019_BeechForest.html)

- [Style sheet](https://www.dropbox.com/home/phd-drafts-anthony/beech-forest-dynamics/Styles_manual_sheet.md/)

- [Introduction](https://www.dropbox.com/sh/5h4mp67p7u6t1lj/AAAQVKS4qnvu2oQLu53JQUofa?dl=0)

- [Bayesian methods](https://www.dropbox.com/home/phd-drafts-anthony/beech-forest-dynamics/A1_full_bayesian_model.pdf)

- [Figures](https://www.dropbox.com/home/phd-drafts-anthony/beech-forest-dynamics/figs)

- [Functional response](https://www.dropbox.com/home/phd-drafts-anthony/beech-forest-dynamics/Davidson_2019_BeechForest_Appendix.pdf)

- [References](): *coming online soon*

All other data and resources to render project from raw data (copied from my private GIT repository) can be found on [dropbox](https://www.dropbox.com/home/phd-drafts-anthony) but will be available here when I have incorporated the co-authors feedback

```{}
<div class="post">
<ul>
{% for post in site.tags["invasive-spp"] %}
  <a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date_to_string }})<br>
    {{ post.description }}
{% endfor %}
</ul>
</div>
```

## Importing data

The orginal data was in excel format and manually covered to csv as below. This has had the non-viable material removed and only whole kernals of seed for three species of beech tree were reported.

```{r seed-data, echo=TRUE}
# raw seed file generated from input file
# create seed data file
seed <- read_csv("C://GIT/beech-paper-private/manuscript/data/seed_data_jan2017.csv")
```

## Data wrangling

This is just me looking at a few of the seed dynamics of the raw dataset. (After the removal of non-nutrious material)

### Seed Measurement 

The data is very clean with all the information but to make life simplier for the analysis and bindng to output data to be correct.

#### Method - `metre sq (m2)`

1. `Bucket radius = 0.125m`

2. `Bucket area = 0.049087385m2`

3. `4 buckets per grid = total catch area = 0.19635 m2`

4. `So seeds /m2  =# Seeds counted/0.1963`

Therefore, if $800$ seeds were counted on a grid on a particular trip, this will equate to $4000 m^2$.

### Variable structure

I have defined the following parameters that help to keep the type of variable the same throughout the joining of the raw data and the model outputs.

```{r variable-str-labels, echo = TRUE}
#month levels to get it right
month_levels <- c("Jan", "Feb", "Mar", "Apr", "May", "Jun","Jul", "Aug", "Sep", "Oct", "Nov", "Dec")

# Grid labels
labels <- c("egl M1" = "Grid one", 
            "egl M2" = "Grid two", 
            "egl MR1" = "Grid three",
            "egl MR2" = "Grid four",
            "hol M1" = "Grid five",
            "hol M2" = "Grid six",
            "hol MR1" = "Grid seven",
            "hol MR2" = "Grid eight")

# Valley labels
labels2 <- c(egl = "Eglinton valley", hol = "Hollyford valley")
```

In this the structure of the variables for the seed dataset have to be joint and visualised we need to insure that there are the same number of replicates in this dataset as the output dataset (from the JAGS model). 

### Tidyverse

To aviod issues with factors and data management I have used the following pre-print publications authored by the creators of `dplyr` and `ggplot2`. Tidyverse is a group of packages that together make use a `tidy` approach effective.

Here is some more information about the [tidyverse approach]("https://www.ssnhub.com/a-tidy-world.html")

```{r current-seed-wrangling}
# data
# glimpse(seed)

# use seed in the previous quarter to predict rate of increase
# so add one to trip to align with r
seed.paper <- mutate(seed, mountain = ifelse(is.na(mountain), 0, mountain),
                 red = ifelse(is.na(red), 0, red),
                 silver = ifelse(is.na(silver), 0, silver),
                 total = red + silver + mountain,
                 valley = ifelse(valley == "E", "egl", "hol"),
                 grid = paste(valley, grid.id),
                 seedm2 = total/0.19635,
                 logseed = log(seedm2)) %>%
  select(valley,red,silver,seedm2, grid.id, grid, trip.no, year, month, total) %>%
  filter(trip.no > 0)
```

### Find extra trips and grids

```{r remove-trips}
# for each year calculate the cumulative number of seeds
seed.paper.1 <- seed.paper %>%
            group_by(grid, year) %>%
              mutate(cum.seed = cumsum(seedm2)) %>%
                filter(trip.no > 0) %>%
                  # arrange(grid, trip.no) %>%
                    subset(!(grid.id %in% c("R1", "R2")))

#these are trips that seed was collected but trapping was not done on these grids
a <- bind_rows(subset(seed.paper.1, grid == "egl M2" & trip.no == "13"),
               subset(seed.paper.1, grid == "egl M2" & trip.no == "14"),
               subset(seed.paper.1, grid == "hol M1" & trip.no == "13"))
```

### Remove additional data

```{r}
seed.paper.2 <- anti_join(seed.paper.1,a) %>%
              mutate(trip = trip.no,
                     month = factor(month, month_levels),
                     log.cum.seed = log10(cum.seed + 1))
```

## Final seed dataset

This is the full raw data reduction for the publication and in all the analysis. This data is lagged by a single trip (as a proxy for seed to "intake rate" relationship).

```{r}
glimpse(seed.paper.2)
```

# Descriptive plots

## Temporal variation in seed

The overall trend in each season is well documented. We have collected data every four months.

```{r seasonal-seed, echo=FALSE, message=FALSE, warning=FALSE}
annual.trend <- ggplot(seed.paper.2, aes(y = seedm2, x = year, fill = valley)) +
  geom_bar(stat = "identity", position=position_dodge()) +
  scale_fill_manual(values=c("#999999", "#E69F00")) +
  labs(x = "Year", y = "Total seed per m2??") +
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) +
  theme_bw() +
  ggtitle("Annual trend")
  
  
seasonal.trend <- ggplot(seed.paper.2, aes(y = seedm2, x = month, fill = valley)) +
  geom_bar(stat = "identity", position=position_dodge()) +
  scale_fill_manual(values=c("#999999", "#E69F00")) +
  labs(x = "Month", y = "Total seed per m2??") +
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) +
  theme_bw()+
  ggtitle("Seasonal trend")

gridExtra::grid.arrange(annual.trend, seasonal.trend, ncol = 2)
```

### Seasonal factorisation

In the data the seasonal parameter is month where:

| Month    | Season | Factor level |
|----------|--------|--------------|
| February | Summer | 1            |
| May      | Autumn | 2            |
| August   | Winter | 3            |
| November | Spring | 4            |

# Mouse dataset

The mouse dataset is generated from the full CR model found [here]("https://www.ssnhub.com/jags-bayesian-model.html")

## Import data

The seed data above needs to be joined to the mouse dataset below. I will step through this process to insure that there are no errors in the merging of the two datasets.

## Output data

The output data of the model is in JAGS format. This means that it needs to be converted into a `dataframe` format. There are many different ways to do this. I have choosen the following tidy approach.

```{r results-output}
# raw counts (ind) into CR model
source("./Rcode/wrangling/Data_CRinput_mice_jan2019.R", echo = FALSE)

```

We save and sort the bayesian model outputs in a `.rds` file and extract these results using:

```{r}
#CR model output data
CR.model.out<-readRDS("C://Code/final_cauchy_2_5.rds")
```

### JAGS output

*JAGSui output* [@kellner2018].

```{r jagsui-output}
# for now this is hand selected...
abund.dat <- data.frame(CR.model.out$summary[, c(1, 2, 3, 7)])
```

#### Naming variable

```{r naming}
#renaming variables
names(abund.dat) <- c("N", "se.N", "lcl.N", "ucl.N")

# adding para for each variable id
abund.dat$var <- rownames(abund.dat)
```

#### Extract only N

```{r extract-n}
#reduce dataset to 136 or 144 rows
## right now it is raw data
abund.dat1 <- abund.dat %>%
  filter(substr(var, 1, 1) == "N")
```

## Restructuring dataset

```{r n-wrangling}
#reduce dataset to 136 or 144 rows
## right now it is raw data
abund.dat1 <- abund.dat %>%
  filter(substr(var, 1, 1) == "N") %>%
  mutate(
    grid = case_when(
      str_detect(var, ",1]") ~ "egl M1",
      str_detect(var, ",2]") ~ "egl M2",
      str_detect(var, ",3]") ~ "egl MR1",
      str_detect(var, ",4]") ~ "egl MR2",
      str_detect(var, ",5]") ~ "hol M1",
      str_detect(var, ",6]") ~ "hol M2",
      str_detect(var, ",7]") ~ "hol MR1",
      str_detect(var, ",8]") ~ "hol MR2",
      TRUE ~ "other"
    ),
    trip = case_when(
      str_detect(string = var, pattern = "N\\[1,") ~ 1,
      str_detect(string = var, pattern = "N\\[2,") ~ 2,
      str_detect(string = var, pattern = "N\\[3,") ~ 3,
      str_detect(string = var, pattern = "N\\[4,") ~ 4,
      str_detect(string = var, pattern = "N\\[5,") ~ 5,
      str_detect(string = var, pattern = "N\\[6,") ~ 6,
      str_detect(string = var, pattern = "N\\[7,") ~ 7,
      str_detect(string = var, pattern = "N\\[8,") ~ 8,
      str_detect(string = var, pattern = "N\\[9,") ~ 9,
      str_detect(string = var, pattern = "N\\[10,") ~ 10,
      str_detect(string = var, pattern = "N\\[11,") ~ 11,
      str_detect(string = var, pattern = "N\\[12,") ~ 12,
      str_detect(string = var, pattern = "N\\[13,") ~ 13,
      str_detect(string = var, pattern = "N\\[14,") ~ 14,
      str_detect(string = var, pattern = "N\\[15,") ~ 15,
      str_detect(string = var, pattern = "N\\[16,") ~ 16,
      str_detect(string = var, pattern = "N\\[17,") ~ 17,
      str_detect(string = var, pattern = "N\\[18,") ~ 18,
      str_detect(string = var, pattern = "N\\[19,") ~ 19,
      str_detect(string = var, pattern = "N\\[20,") ~ 20
    ),
    grid.n = as.numeric(factor(grid)),
    grid = factor(grid),
    trip.no = trip,
    valley = factor(ifelse(grepl("egl", grid), "egl", "hol"))
  )
```

### Group levels

THis has been hard to do with as little manual mistakes in factor levels as possible. The levelling structure should be the same throughout this document as descripted in beech data above. But in short:

```{r variable-str-labels2, echo = TRUE}
#month levels to get it right
month_levels <- c("Jan", "Feb", "Mar", "Apr", "May", "Jun","Jul", "Aug", "Sep", "Oct", "Nov", "Dec")

# full dates
true.date <- as.Date(c("1999-05-01","1999-08-01","1999-11-01","2000-02-01","2000-05-01","2000-08-01","2000-11-01","2001-02-01","2001-05-01","2001-08-01", "2001-11-01","2002-05-01","2002-11-01","2003-02-01","2003-05-01","2003-08-01","2003-11-01","2004-02-01","2004-05-01","2004-08-01"))

# Grid labels
labels <- c("egl M1" = "Grid one", 
            "egl M2" = "Grid two", 
            "egl MR1" = "Grid three",
            "egl MR2" = "Grid four",
            "hol M1" = "Grid five",
            "hol M2" = "Grid six",
            "hol MR1" = "Grid seven",
            "hol MR2" = "Grid eight")

# Valley labels
labels2 <- c(egl = "Eglinton valley", hol = "Hollyford valley")

# COntrol labels
# Stoats yes/no


# Conditions labals
# Rats yes/no

# Full treatment 
# 6 levels
treat.six.levels <- c("hol no control rats.removed",
                                     "hol control rats.present",
                                     "hol control rats.removed",
                                     "egl control rats.present",
                                     "egl control rats.removed" ,
                                     "hol no control rats.present")

```

### Adding grouping variables

```{r set-upmanuscript}
abund.dat2 <- abund.dat1 %>%
  mutate(control = case_when(
    trip > 12 & valley == "hol" ~ "H+",
    str_detect(string = valley, pattern = "egl") ~ "E+",
    str_detect(string = grid, pattern = "hol") ~ "H-"
  ),
  Valley = valley)
```

```{r wrangling-code, eval=FALSE, include=FALSE}
# RUN IN r
# compareGroups::cGroupsGUI(abund.dat2)

# ALL TRIP VARIABLES ARE NUMBERS AT THIS STAGE
# WHAT TO DO???

names(abund.dat)
names(abund.dat1)
names(abund.dat2)


#check data
# summary(abund.dat5)
# glimpse(abund.dat5)
# Sorting factors for plots
#nice labels
# abund.dat5 %>%
#   mutate(Rats = factor(Conditions, labels = c("Full", "Reduced")),
#          Control = factor(control, labels = c("Yes", "No")),
#          Valley = factor(valley, labels = c("Eglinton", "Hollyford")),
#          Date = as.Date(true.date))
```

### Reduced seed joining dataset

```{r joining-datasets}
# ISSUE WITH trip == nonsense numbers
# this is where months died maybe>!>!
join.seed <- select(seed.paper.2, grid,trip, year, month, cum.seed, valley)
```

Check the structure of this to make sure that the variables being joined are being correctly merged.

```{r}
glimpse(join.seed)

levels(join.seed$month)
labels(join.seed$month)

# levels(abund.dat5$month)
# labels(abund.dat5$month)
# 
# table(join.seed$month,abund.dat5$month)
```


### Joining seed and mice

```{r}
# full data

abund.dat3 <- right_join(abund.dat2, join.seed, by = c("valley", "trip", "grid"))%>%
# glimpse(abund.dat3)
  mutate(seed.account.N = cum.seed / N,
    # seed.paper = ifelse(cum.seed>0,cum.seed / N, cum.seed),
    log.seed = ifelse(cum.seed > 0, log10(cum.seed), cum.seed),
    control = NA)
```

### Stoat control

**control variable**

```{r control-variable}
# Stoat control
for (i in 1:length(abund.dat3$valley)) {
  abund.dat3$control[i]  <-
    ifelse(abund.dat3$valley[i] == "hol" &
             abund.dat3$trip[i] > 12,
           "control",
           "no control")
  abund.dat3$control[i]  <-
    ifelse(abund.dat3$valley[i] == "egl", "control", abund.dat3$control[i])
}
```

### Added rat Conditions

```{r}
grids.dat <-
  colsplit(string = abund.dat3$grid,
    pattern = " ",
    names = c("valley.rep", "grid.rats")
  )

abund.dat4 <- abund.dat3 %>%
  bind_cols(grids.dat) %>%
  mutate(
    grid.rats = factor(grid.rats, levels = c("M1", "M2", "MR1", "MR2")),
    Conditions = ifelse(
      grid.rats == "M1" | grid.rats == "M2",
      "rats.removed",
      "rats.present"
    )
  )

glimpse(abund.dat4)
```

### More grouping options

```{r}
# create variable for grouping
abund.dat5 <- abund.dat4 %>%
  mutate(grouping.1 = ifelse(N < 49, "treat.lowN", "treat.highN"),
    grouping.2 = ifelse(N < 10, "treat.lowN", "treat.highN"),
    grouping.3 = ifelse(
      year == 2001 |
        year == 2002 | year == 2004,
      "treat.lowN",
      "treat.highN"
    ),
    grouping.4 = ifelse(year == 2001 |
                          year == 2002, "treat.lowN", "treat.highN"),
    true.date = as.Date(factor(trip,labels = c("1999-05-01","1999-08-01","1999-11-01","2000-02-01","2000-05-01","2000-08-01","2000-11-01","2001-02-01","2001-05-01","2001-08-01", "2001-11-01","2002-05-01","2002-11-01","2003-02-01","2003-05-01","2003-08-01","2003-11-01","2004-02-01","2004-05-01","2004-08-01"))),
    treat.six = paste(valley, control, Conditions)
  )
```

### Re-leveling 

Just a final check that everything has worked.

```{r}
# getting factor levels correct for once
plot.dat.all1 <-  abund.dat5 %>%
    mutate(Rats = factor(Conditions, labels = c("Full", "Reduced")),
           Control = factor(control, labels = c("Yes", "No")),
           Valley = factor(valley, labels = c("Eglinton", "Hollyford")),
           Date = as.Date(true.date), 
           Treatments = factor(treat.six, levels = c("hol no control rats.removed",
                                                             "hol control rats.present", 
                                                             "hol control rats.removed",
                                                             "egl control rats.present",
                                                             "egl control rats.removed" ,    
                                                             "hol no control rats.present")),
           Prediction = NA) %>%
      mutate(Prediction = ifelse(Date == "2000-08-01", "A", Prediction),
             Prediction = ifelse(Date == "2001-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" , "B", Prediction),
             Prediction = ifelse(Date == "2001-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" , "B", Prediction),
             Prediction = ifelse(Date == "2001-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" , "B", Prediction),
             Prediction = ifelse(Date == "2001-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" , "B", Prediction))

# overall larger points
plot.dat.sum <- plot.dat.all1 %>%
    mutate(counter = 1) %>%
    group_by(Rats, Valley, Control) %>%
    summarise(reps = sum(counter), 
              max.date = max(Date),
              min.date = min(Date))
  
plot.dat.sum1 <- plot.dat.sum %>%
    gather(key = limit, 
           value = Date, 
           max.date:min.date) %>%
    mutate(limit = factor(ifelse(limit == "max.date", "max", "min")),
           treat = paste(Valley,Control, Rats)) %>%
    ungroup()

# table(plot.dat.sum1$Control)
# plot labels
#find in overall plot.dat by filtering on A?
#april 2019

labels.dat <- filter(plot.dat.all1, Prediction == "A" | Prediction == "B") 

# %>% 
#   distinct(Prediction, .keep_all = TRUE) %>%
#     mutate(Valley = c("Hollyford", "Hollyford"))
# glimpse(plot.dat.all1$Rats)

# table(plot.dat.all1$Rats,plot.dat.all1$Control, plot.dat.all1$Valley)

p.design <- plot.dat.all1 %>%
  mutate(grid = as.numeric(factor(grid)))

# glimpse(plot.dat.all1)
```

## Generalising trends

The final plots. All extended plots are in the `Rcode/figures/`.

### Seed

```{r echo=TRUE}
# turn seed.paper.2 into plot
# for publication
# May2019

names(abund.dat5)

# Valley and Control summaries
seed.2mean <- plot.dat.all1 %>%
  group_by(Control, Valley, Date) %>%
  summarise(
    mean.s = mean(cum.seed),
    sd.s = sd(cum.seed),
    se.s = sd(cum.seed) / sqrt(length(cum.seed)) * 1.96,
    lcl.s = mean(cum.seed) - (sd(cum.seed) / sqrt(length(cum.seed)) *
                                1.96),
    ucl.s = mean(cum.seed) + (sd(cum.seed) / sqrt(length(cum.seed)) *
                                1.96)
  ) %>%
  ungroup()

# Valley, control and Conditions summaries
seed.2mean <- plot.dat.all1 %>%
  group_by(Control, Valley, Date) %>%
  summarise(
    mean.s = mean(cum.seed),
    sd.s = sd(cum.seed),
    se.s = sd(cum.seed) / sqrt(length(cum.seed)) * 1.96,
    lcl.s = mean(cum.seed) - (sd(cum.seed) / sqrt(length(cum.seed)) *
                                1.96),
    ucl.s = mean(cum.seed) + (sd(cum.seed) / sqrt(length(cum.seed)) *
                                1.96)
  ) %>%
  ungroup()


# levels(seed.2mean$gp.treat)
# note that plot uses both meanS and meanS.1
# seed.aver.plot <-
ggplot(data = plot.dat.all1,
       aes(y = cum.seed,
         x = Date,
         shape = Valley,
         fill = Control,
         col = Rats)) +
  
  # extra goodies
  geom_rect(aes(
    xmin = ymd('2000-01-01'),
    xmax = ymd('2000-12-31'),
    ymin = -Inf,
    ymax = Inf
  ),
  colour = "grey90",
  fill = "grey90") +
  
  geom_rect(aes(
    xmin = ymd('2002-01-01'),
    xmax = ymd('2002-12-31'),
    ymin = -Inf,
    ymax = Inf
  ),
  colour = "grey90",
  fill = "grey90") +
  
  geom_rect(aes(
    xmin = ymd('2004-01-01'),
    xmax = ymd('2004-12-31'),
    ymin = -Inf,
    ymax = Inf
  ),
  colour = "grey90",
  fill = "grey90") +
  
  geom_point(aes(fill = Control), stroke = 1.15, size = 3) 

# +
   # geom_line(data = seed.2mean, aes(y = mean.s, x = Date), size = 0.9) 
#
  # # +
  #   # geom_errorbar(data = meanS.1, mapping = aes(ymin = lcl.s, ymax = ucl.s), width = 0, alpha = 0.5, lwd = 0.75) +
  #
  # geom_line(data = seed.2mean,
  #           aes(y = mean.s,
  #               x = Date),
  #           size = 1,
  #           col = "grey50") +
  # 
  # geom_point(data = seed.2mean, aes(y = mean.s,
  #                                  x = Date), size = 5) +
  # 
  # 
  # 
  # scale_color_manual(name = "Stoat Control",
  #                    values = c("white", "black")) +
  # 
  # scale_shape_manual(name = "Ecosystem",
  #                    values = c(24, 21)) +
  # 
  # # manually define the fill colours
  # #
  # scale_fill_manual(
  #   name = "Stoat Control",
  #   values = c("cornflowerblue", "darkorange", "white", "black")
  # ) +
  # 
  # # defining size with 2 marginally different values
  # scale_size_manual(name = "Rat Control", values = c(5, 4)) +
  # 
  # # geom_abline(intercept = 5, slope = 0, size = 1) +
  # # theme
  # theme_new() +
  # 
  # 
  # # labels
  # # scale_y_discrete(labels = c("1","2","3","4"," ","1","2","3","4")) +
  # # scale_x_date() +
  # # defining size with 2 marginally different values
  # # scale_size_manual(name = "Rat Control", values = c(4, 3)) +
  # 
  # # Remove fill legend and replace the fill legend using the newly created size
  # guides(
  #   col = "none",
  #   shape = guide_legend(override.aes = list(shape = c(24, 21))),
  #   fill = guide_legend(override.aes = list(col = c(
  #     "cornflowerblue", "darkorange"
  #   )))
  # )



# study design plot
# may 2019
#anthony

source("./rcode/davidson_2019_theme.r")
# source("./rcode/figures/study-design-data.R")

p.design <- plot.dat.all1 %>%
  mutate(grid = as.numeric(factor(grid)))

# glimpse(plot.dat.all1)

# adding NA grid to plot

bd.row <- p.design[1, ]
bd.row$grid <- "blank"
bd.row$grid <- "blank"
bd.row$grid <- "blank"
bd.row$grid <- "blank"
bd.row$Date <- NA

# bind row to plot data
p.design145 <- rbind(p.design, bd.row)
# glimpse(p.design145$grid)

# labels
rat.labs <- c("No", "Reduced")

#re-factoring
p.design1 <- p.design145  %>%
  mutate(grid = factor(grid, levels = c(
    "1", "2", "3", "4", "blank", "5", "6", "7", "8"
  )),
  Rats = factor(Rats, labels = rat.labs))


#checking
# tail(p.design1)
# tail(filter(p.design1, grid == "blank"))
# levels(p.design1$grid)
# labels() <- c("1","2","3","4"," ","5","6","7","8")

# p.design1$grid <- factor(p.design1$grid,  labels = c("1","2","3","4"," ","1","2","3","4"))

#plot raw seed
fig.3.plot.seed <- ggplot(p.design1,
                          aes(
                            y = cum.seed,
                            col = Rats,
                            shape = Valley,
                            fill = Control,
                            x = Date
                          ),
                          size = 4) +
  # geom_line(col = "grey50") +
  geom_point(aes(size = Rats,
                 group = grid), stroke = 1.25) +
  
  scale_color_manual(name = "Stoat Control",
                     values = c("white", "black")) +
  
  scale_shape_manual(name = "Ecosystem",
                     values = c(24, 21)) +
  
  # manually define the fill colours
  
  scale_fill_manual(name = "Stoat Control",
                    values = c("cornflowerblue", "darkorange")) +
  # geom_abline(intercept = 5, slope = 0, size = 1) +
  # theme
  theme_new() +
  
  scale_size_manual(name = "Rat Control", values = c(4, 3)) +
  # labels
  # scale_y_discrete(labels = c("1","2","3","4"," ","1","2","3","4")) +
  # scale_x_date() +
  # defining size with 2 marginally different values
  
  # Remove fill legend and replace the fill legend using the newly created size
  guides(
    col = "none",
    size = guide_legend(override.aes = list(shape = c(16, 1))),
    shape = guide_legend(override.aes = list(
      shape = c(24, 21), size = 4
    )),
    fill = guide_legend(override.aes = list(
      col = c("cornflowerblue", "darkorange"),
      size = 4
    ))
  ) +
  #   col = "none",
  #   # size = guide_legend(override.aes = list(shape = c(16, 1))),
  #   shape = guide_legend(override.aes = list(
  #     shape = c(24, 21), size = 4
  #   ))
  #   # fill = guide_legend(override.aes = list(
  #     # col = c("cornflowerblue", "darkorange"), size = 4
  #   # ))
  # ) +
  
  #   geom_hline(yintercept = 0,
#              lty = 5,
#              alpha = 0.7)  +
#
xlab(expression(paste("Time", "(", italic(t), ")"))) +
  
  ylab(expression(paste("Available seed ", "(", italic(Seed[jt]), ")")))

fig.3.plot.seed


# sorting summary dataset for the last time -------------------------------
#summarising seed
table(is.na(p.design1$grid))
#remove NA for making space in last plot
p.design1 <- p.design1[1:144, ]
#no grid na anymore
table(is.na(p.design1$grid))

#making datasest
p.design2 <- p.design1 %>%
  group_by(Control, Valley, Date) %>%
  summarise(cum.seed = mean(cum.seed),
            Rats = factor("Full", levels = c("Full", "Reduced"))) %>%
  ungroup() %>%
  mutate(grid = factor(paste(Control, Valley)))

# grouping of grid correct?
levels(p.design2$grid)
p.design2$Rats

# glimpse(p.design2)
#plot summary seed

# Add NA so legend works
row.input.leg <- p.design2[1, ]
row.input.leg$Control <- NA
row.input.leg$Valley <- NA
row.input.leg$Date <- NA
row.input.leg$cum.seed <- NA
row.input.leg$Rats <- "Reduced"
row.input.leg$grid <- NA

p.design3 <- rbind(p.design2, row.input.leg)
# glimpse(p.design3)
levels(p.design3$Rats)
col = c("cornflowerblue", "darkorange")

#plot raw seed
fig.3.plot.seed.sum <- ggplot(p.design2,
                              aes(
                                y = cum.seed,
                                col = Rats,
                                shape = Valley,
                                fill = Control,
                                x = Date
                              ),
                              size = 4) +
  geom_line(col = "grey50") +
  geom_point(aes(size = Rats,
                 group = grid), stroke = 1.25) +
  
  scale_color_manual(name = "Stoat Control",
                     values = c("white", "black")) +
  
  scale_shape_manual(name = "Ecosystem",
                     values = c(24, 21)) +
  
  scale_size_manual(name = "Rat Control", values = c(4, 3)) +
  # manually define the fill colours
  
  scale_fill_manual(name = "Stoat Control",
                    values = c("cornflowerblue", "darkorange")) +
  # geom_abline(intercept = 5, slope = 0, size = 1) +
  # theme
  theme_new() +
  
  
  # labels
  # scale_y_discrete(labels = c("1","2","3","4"," ","1","2","3","4")) +
  # scale_x_date() +
  # defining size with 2 marginally different values
  
  # Remove fill legend and replace the fill legend using the newly created size
  guides(
    col = "none",
    size = "none",
    shape = guide_legend(override.aes = list(
      shape = c(24, 21), size = 4
    )),
    fill = guide_legend(override.aes = list(
      col = c("cornflowerblue", "darkorange"),shape = c("square"),
      size = 4
    ))
  ) +
  #   col = "none",
  #   # size = guide_legend(override.aes = list(shape = c(16, 1))),
  #   shape = guide_legend(override.aes = list(
  #     shape = c(24, 21), size = 4
  #   ))
  #   # fill = guide_legend(override.aes = list(
  #     # col = c("cornflowerblue", "darkorange"), size = 4
  #   # ))
  # ) +
  
  #   geom_hline(yintercept = 0,
#              lty = 5,
#              alpha = 0.7)  +
#
xlab(expression(paste("Time", "(", italic(t), ")"))) +
  
  ylab(expression(paste("Available seed ", "(", italic(Seed[jt]), ")")))

fig.3.plot.seed.sum



# Combine them ------------------------------------------------------------

#plot raw seed
fig.3.seed <- ggplot(p.design1,
                     aes(
                       y = cum.seed,
                       col = Rats,
                       shape = Valley,
                       fill = Control,
                       x = Date
                     )) +
  # geom_line(col = "grey50") +
  geom_point(aes(size = Rats,
                 group = grid),
             stroke = 1.25,
             alpha = 0.5) +
  
  scale_color_manual(name = "Stoat Control",
                     values = c("white", "black", "white")) +
  
  scale_shape_manual(name = "Ecosystem",
                     values = c(24, 21)) +
  
  scale_size_manual(name = "Rat Control", values = c(2.5, 3, 2.5)) +
  # manually define the fill colours
  
  scale_fill_manual(
    name = "Stoat Control",
    values = c("cornflowerblue", "darkorange", "cornflowerblue")
  ) +
  
  
  geom_line(
    data = p.design2,
    aes(y = cum.seed,
        x = Date),
    size = 0.95,
    col = "grey50"
  ) +
  
  geom_point(
    data = p.design2,
    aes(
      y = cum.seed,
      col = Rats,
      shape = Valley,
      fill = Control,
      x = Date
    ),
    size = 7
  ) +
  
  # Remove fill legend and replace the fill legend using the newly created size
  guides(
    col = "none",
    size = guide_legend(override.aes = list(
  shape = c(15,0),alpha = 1
    )),
    shape = guide_legend(override.aes = list(
      shape = c(24, 21), size = 4
    )),
    fill = guide_legend(override.aes = list(
      col = c("cornflowerblue", "darkorange"),shape = c("square"),
      size = 4
    ))
  ) +
  
  xlab(expression(paste("Timing of sample", "(", italic(t), ")"))) +
  
  ylab(expression(paste("Available seed ", "(", italic(Seed[jt]), ")")))

fig.3.seed

# export plot for example vignette
# jpeg("./figs/fig-3.1-study.jpeg")
# fig.3.seed
# dev.off()

```

# Saved datasets

I will save the final dataset for the analysis of the Beech foret data for the publication as so:


## Study design

```{r}
# study design plot
# march 2019
#anthony

# need the manuscript code to run before this
# data
# dataset 1
# summary by treatment
# plot.dat.sum <- abund.dat5 %>%
#     mutate(counter = 1) %>%
#       group_by(Conditions, valley, control) %>%
#         summarise(reps = sum(counter), 
#                   max.date = max(true.date),
#                   min.date = min(true.date))
# 
# plot.dat.sum1 <- plot.dat %>%
#           gather(key = limit, 
#                  value = true.date, 
#                  max.date:min.date) %>%
#   mutate(limit = factor(ifelse(limit == "max.date", "max", "min")),
#          treat.six = factor(paste(valley, control, Conditions))) %>%
#       ungroup()
# 
# #get all levels right
# levels(plot.dat.sum1$treat.six) <- c("hol no control rats.removed",
#                                  "hol control rats.present", 
#                                  "hol control rats.removed",
#                                  "egl control rats.present",
#                                  "egl control rats.removed" ,    
#                                  "hol no control rats.present")
# 
# names(plot.dat.sum1)
# 
# full replicates dataset (unique trips and grids)
plot.dat.all <- abund.dat5 %>%
  distinct(trip, grid, .keep_all = TRUE) 

# %>%
    # select(Conditions, valley, control, true.date,treat.six, grid, N, N.seed,cum.seed)

#get all levels right

levels(plot.dat.all$treat.six) <- c("hol no control rats.removed",
                                     "hol control rats.present",
                                     "hol control rats.removed",
                                     "egl control rats.present",
                                     "egl control rats.removed" ,
                                     "hol no control rats.present")


# saving data -------------------------------------------------------------
# csv the fuker!
# write.csv(plot.dat.all, "study_design_plot.csv")
# plot.study <- read.csv("study_design_plot.csv"

# plot labels
points.dat <- tibble(
  prediction = as.character(c("A", "B", "A")),
  valley = factor(c("egl", "hol", "hol")),
  true.date = as.Date(c("2000-08-01","2001-08-01","2003-08-01")))

# getting factor levels correct for once

plot.dat.all1 <-  plot.dat.all %>%
    mutate(Rats = factor(Conditions, labels = c("Full", "Reduced")),
           Control = factor(control, labels = c("Yes", "No")),
           Valley = factor(valley, labels = c("Eglinton", "Hollyford")),
           Date = as.Date(true.date), 
           Treatments = factor(treat.six, levels = c("hol no control rats.removed",
                                                             "hol control rats.present", 
                                                             "hol control rats.removed",
                                                             "egl control rats.present",
                                                             "egl control rats.removed" ,    
                                                             "hol no control rats.present")),
           Prediction = NA) %>%
      mutate(Prediction = ifelse(Date == "2000-08-01", "A", Prediction),
             Prediction = ifelse(Date == "2001-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" , "B", Prediction),
             Prediction = ifelse(Date == "2001-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" , "B", Prediction),
             Prediction = ifelse(Date == "2001-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" , "B", Prediction),
             Prediction = ifelse(Date == "2001-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" | 
                                   Date == "2003-08-01" , "B", Prediction))

# overall larger points
plot.dat.sum <- plot.dat.all1 %>%
    mutate(counter = 1) %>%
    group_by(Rats, Valley, Control) %>%
    summarise(reps = sum(counter), 
              max.date = max(Date),
              min.date = min(Date))
  
plot.dat.sum1 <- plot.dat.sum %>%
    gather(key = limit, 
           value = Date, 
           max.date:min.date) %>%
    mutate(limit = factor(ifelse(limit == "max.date", "max", "min")),
           treat = paste(Valley,Control, Rats)) %>%
    ungroup()

# table(plot.dat.sum1$Control)
# plot labels
#find in overall plot.dat by filtering on A?
#april 2019

labels.dat <- filter(plot.dat.all1, Prediction == "A" |
                       Prediction == "B") 

# %>% 
#   distinct(Prediction, .keep_all = TRUE) %>%
#     mutate(Valley = c("Hollyford", "Hollyford"))






# glimpse(plot.dat.all1$Rats)

# table(plot.dat.all1$Rats,plot.dat.all1$Control, plot.dat.all1$Valley)

p.design <- plot.dat.all1 %>%
  mutate(grid = as.numeric(factor(grid)))

# glimpse(plot.dat.all1)
p.design

# export study design data
write.csv(plot.dat.all1, "./Data/study-design-plot-input-data.csv")

```

## Seed data

```{r saving-mod-data}
# save csv file
# write.csv(dat.s, "C://GIT/beech-paper-private/manuscript/data/Seed_data_hol_egl_total.csv")
# tail(dat.s)
```

## Mice, rats and seed data

```{r writing-csvs, eval=FALSE, include=FALSE}
write.csv(dat.sFix, "C://GIT/beech-paper-private/manuscript/data/Seed_data_hol_egl_totalFix.csv")
```

## Plotting data

```{r}
# export study design data
write.csv(plot.dat.all1, "./Data/study-design-plot-input-data.csv")

```

## Parameter data

# Bug fixed!!

**THIS IS the error...** Over the past ... ages I have had issues with factors, characters and merging datasets. Here is where the biggest error in my analysis is found. I have worked through it below (to my shame!)

## ISSUE

In the raw and slightly modified seed datasete month looks like so...

```{r good-or}
# <!--     Aug      36 (25.0%)        -->
# <!--     Feb      28 (19.4%)        -->
# <!--     May      44 (30.6%)        -->
# <!--     Nov      36 (25.0%)        -->
```

And the merged dataset that includes the outputs of the capture-recapture model we are using looks like....

```{r bad-or}
# <!--     Feb 28 (19.4%)      -->
# <!--     May 44 (30.6%)      -->
# <!--     Aug 36 (25.0%)      -->
# <!--     Nov 36 (25.0%)      -->
```

## Solution!

I have manually fixed the manuscript code here when mering seed and N. **Above no-longer is an issue using the Tidyverse set of tools [@ross2017].**

# Descriptive Analysis

## Raw data modifications

```{r new-data}
# for raw estimates...
# read in the seed data
# seed <- read.csv("C://GIT/beech-paper-private/manuscript/data/Seed_data_hol_egl_total.csv", strip.white = T)
# glimpse(seed)

# this is no longer working
#seed to try me...

#model1
#total
total <- tapply(seed.paper.2$total, list(seed.paper.2$trip.no, seed.paper.2$grid), mean) +1

#model2
seedm2 <- tapply(seed.paper.2$seedm2, list(seed.paper.2$trip.no, seed.paper.2$grid), mean) +1

#model3
#cum.seed
cum.seed <- tapply(seed.paper.2$cum.seed, list(seed.paper.2$trip.no, seed.paper.2$grid), mean) +1

#model4
# log.cum.seed
log.cum.seed <- log10(tapply(seed.paper.2$cum.seed, list(seed.paper.2$trip.no, seed.paper.2$grid), mean) + 1)

#model5 - totalIR
IR <- rep(NA,length(seed.paper.2$seedm2))

for(i in 1:length(seed.paper.2$seedm2)) {IR[i] <- 1042.1 * (1 - exp(-(seed.paper.2$seedm2[i] * 0.00139)))}
IR_tseed <- tapply(IR, list(seed.paper.2$trip.no, seed.paper.2$grid), mean)


#model5 - totalIR
IR <- rep(NA,length(seed.paper.2$cum.seed))

for(i in 1:length(seed.paper.2$cum.seed)) {IR[i] <- 1042.1 * (1 - exp(-(seed.paper.2$cum.seed[i] * 0.00139)))}
IR_cseed <- tapply(IR, list(seed.paper.2$trip.no, seed.paper.2$grid), mean)

# not sure what this code
month <- apply(a, 1, function(x) which(x > 0))
valley <- c(1, 1, 1, 1, 2, 2, 2, 2)

labels <- c(M1 = "Grid one", M2 = "Grid two", MR1 = "Grid three",MR2 = "Grid four",R1 = "Grid five",R2 = "Grid six")
labels2 <- c(egl = "Eglinton valley", hol = "Hollyford valley")



##seed needs to be a list in same order as out.r

# ????

# filter(seed.paper.2, cum.seed > 3000)
write.csv(seed, "C://GIT/beech-paper-private/manuscript/data/Seed_data_hol_egl_Figure2_data.csv")
```

```{r model-input-vary}
# old skol
# seed.paper.1$month <- factor(seed.paper.1$month, levels = c("Feb", "May", "Aug", "Nov"))
# colnames(seed.paper.1)[2] <- "trip"
# fac tor(seed.paper.1$trip)
# names(seed.paper.1)

#need to reduce dataset to 144 not 147 reps

# seed.paper.1 data variations--------------------------------------------------------------------

#model1
#total
total <- tapply(seed.paper.2$total, list(seed.paper.2$trip.no, seed.paper.2$grid), mean) + 1

#model2
seedm2 <- tapply(seed.paper.2$seedm2, list(seed.paper.2$trip.no, seed.paper.2$grid), mean) + 1

#model3
#cum.seed
cum.seed <- tapply(seed.paper.2$cum.seed, list(seed.paper.2$trip.no, seed.paper.2$grid), mean) +1

#model4
# log.cum.seed
log.cum.seed <- log10(tapply(seed.paper.2$cum.seed, list(seed.paper.2$trip.no, seed.paper.2$grid), mean) + 1)

#model5 - totalIR
IR <- rep(NA,length(seed.paper.2$seedm2))
for(i in 1:length(seed.paper.2$seedm2)) {IR[i] <- 1042.1 * (1 - exp(-(seed.paper.2$seedm2[i] * 0.00139)))}
IR_tseed <- tapply(IR, list(seed.paper.2$trip.no, seed.paper.2$grid), mean)
```

## Model dataset

```{r table-0}
# modified seed file for analysis
seed.paper <- read_csv("C://GIT/beech-paper-private/manuscript/data/seedjoining-data.csv")

table1 <- head(seed.paper)
kable(table1)

# #must run in R console??
# compareGroups::cGroupsGUI(abund.dat5)
# 
# #doesnt work for some reason
# compareGroups::cGroupsGUI(seed.paper.2)

```

```{r year by month seed, eval=FALSE, fig.height=15, fig.width=12, message=FALSE, warning=FALSE, include=FALSE}
ggplot(seed.paper, aes(y = miseed.paper ,x = month, fill = valley)) +
  geom_point(stat = "identity", position=position_dodge()) +
  scale_fill_manual(values=c("#999999", "#E69F00")) +
  labs(x = "Month", y = "Total seed per m2??") +
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) +
  theme_bw()
```

## Simple GLMs

Fit model to the data we only have 4 measurements per grid across 4 years. This means that the data we are trying to fit is the average 

```{r beech_sim data, eval=FALSE, message=FALSE, warning=FALSE, include=FALSE}

###becch seed data--------------------------------------------------------
#import data
seed<-read.csv("seed_data_jan2017.csv")

# create a variable to distinguish each valley and each unique grid
seed <- mutate(seed, grid = paste(valley, grid.id))
seed <- mutate(seed, miseed.paper = red + silver + mountain)
seed.paper <- group_by(seed, valley,red,silver,mountain, grid.id, grid, trip.no,miseed.paper)
head(seed.paper)

monthscorr<-c("Feb", "May", "Aug", "Nov")
seed.paper <- transform(seed.paper, month = factor(month, levels = monthscorr))


#for ggplot of each relationship
#there are 12 grids, 5 years
#need a column for each time frame being separate (should be 240 seasons to test)


names(seed.paper)
seed.paper <- mutate(seed.paper, season = paste(grid,year))
seed.paper <- mutate(seed.paper, logseed = log(miseed.paper))

#changes NAs to zeros
#not a good thing I dont think
is.na(seed.paper$logseed) <- sapply(seed.paper$logseed, is.infinite)

#assuming that all very small numbers are zero seedfall.....
seed.paper$logseed  <- ifelse(is.na(seed.paper$logseed), 0, seed.paper$logseed)

#sort out factors?!?
  seed.paper <- seed.paper %>% mutate_each_(funs(factor(.)), names( .[,sapply(., is.factor)]))
  
  

#data for regression
sseed <- as.numeric(seed.paper$logseed)
syear <- as.factor(seed.paper$year)
smonth <- as.factor(seed.paper$month)
sseason <- as.factor(seed.paper$season)


#simple plot of model construction
ggplot(seed.paper, aes(x = month, y = logseed)) +
  geom_line(aes(group = season, colour = grid),lwd = 2) +
  facet_grid(~year) +
  theme_bw()

length(seed.paper$season)
length(unique(seed.paper$season))
```

Where we are trying to fit a line to each on of the 66 (out of all the possible trends...

```{r beech_sim classic, eval=FALSE, message=FALSE, warning=FALSE, include=FALSE}

model1 <- glm(sseed ~ smonth)
summary(model1)

model2 <- glm(sseed ~ smonth + syear)
summary(model2)

model3 <- glm(sseed ~ smonth + syear)
summary(model3)

ggplot(seed.paper, aes(y = logseed ,x = month, fill = valley)) +
  geom_bar(stat = "identity", position=position_dodge()) +
  scale_fill_manual(values=c("#999999", "#E69F00")) +
  labs(x = "Month", y = "Total seed per m2??") +
  theme(axis.text.x = element_text(angle = 90, hjust = 1)) +
  theme_bw()

```

To account for fixed and random effects it is easier to do this is a bayes framework as below. The model usedin is

```{r beech_sim bayes, eval=FALSE, message=FALSE, warning=FALSE, include=FALSE}

glimpse(seed.paper)
seed.paper$logseed

#how does season effect beechseed....

#model

sink ("modsim1.txt")
cat(" model {
    
    #likelihood
    
    for (i in 1:N){
    sseed[i] ~ dnorm(m[i])
    m[i]<-b0+b1*smonth[i]
    }  #N
    
    #priors
    b0~dnorm(0,0.0001)
    b1~dnorm(0,0.0001)
    }
    ")
sink()

modsim1 <-  jags(model = "modsim1.txt", 
             data = list(sseed=sseed, N = N, smonth=smonth),
             inits = function(){list(b0=rnorm(1),b1=rnorm(1))},
             param = c("b0","b1"),
             n.chains = 3, 
             n.burnin = 5000, 
             n.iter = 10000, 
             n.thin = 1,
             parallel = T)



```

## JAGS model

```{r Final results}
# ###convergance statistics---------------------------------------------
# par(mfrow=c(3,3))
# traceplot(mod3)
# 
# library(ggmcmc)
# library(car)
# library(coda)
# # makeS gorgeous compilation of plots saved as ggmcmc-output.pdf 
# # Produces density plots of the whole chain (black) with the density plot of only the latest part of the chain (green). By default, 
# # it uses the latest 10% of the chain as a comparison.
# 
# #only works with R2jags at mo
# detach("package:jagsUI", unload=TRUE)
# library("R2jags", lib.loc="C:/Program Files/R/R-3.3.1/library")
# 
# # fit.mcmc <- as.mcmc(mod3)  
# # gelman.plot(fit.mcmc) 
# # geweke.diag(fit.mcmc) 
# # raftery.diag(fit.mcmc) 
# # heidel.diag(fit.mcmc)
# # fit.gg <- ggs(fit.mcmc) 
# # ggs_density(fit.gg) 
# # ggs_traceplot(fit.gg) 
# #ggmcmc(fit.gg,file = "model1_int_seed_dens.pdf") 



```

# NOTES

There is NO red beech recorded in the Hollyford valley

There is larger peaks of overall food in the Eglinton Valley compared to the Hollyford

Questions still needing asked:

1. log of -inf needs to be replaced with zero before analysis?
2.

## References


## Appendix

#### Tree `~spp`

But there could be more to this because there are differences between the different types of seed and the two valley systems

```{r beech seed2, echo=FALSE}
# plot data
seed.p1 <- seed %>%
              mutate(grid = paste(valley,grid.id))
                
            
# plot
p1 <- ggplot(seed.p1, aes(y = red, x = trip.no, shape = valley, col = grid, group = grid)) +
           geom_point()+
    geom_line()+ 
  theme(legend.position = "none")

p2 <- ggplot(seed.p1, aes(y = silver, x = trip.no, shape = valley, col = grid, group = grid)) +
           geom_point()+
    geom_line()
    
p3 <- ggplot(seed.p1, aes(y = mountain, x = trip.no, shape = valley, col = grid, group = grid)) +
           geom_point()+
    geom_line() + 
  theme(legend.position = "none")

gridExtra::grid.arrange(p1, p2, p3)
  # seed <- tibble(seed)
# seed.table <- seed[1:3,]
# kable(seed.table)

```

## Spatial variation in seed

We have replicated spatial areas in two ways in our study. We have replicated ecosystems (Valleys) twice and replicated six grids within each one.

### `~valley`

There is a cool bit of code below of  dealing with vaibale plotting without having to use `gather`.

```{r beech seed3, echo=FALSE}
ggplot(seed, aes(y = red, x = trip.no)) +
  geom_point(aes(y = red,color="red"))+
  geom_point(aes(y = silver,color="silver"))+
  geom_point(aes(y = mountain,color="mountain"))+
  stat_summary(color="blue",fun.y="mean",geom="line")+
  facet_grid(~valley) +
  theme_bw()
```

This shows that infact there are differences in the forest composition of the two valleys that have differences in control of stoats.

This is important because differences or lack of differences in the two valleys may simply be due to the different forest compositions rather than the removal of stoats from one system.

### `~grid`

```{r beech seed4, echo=FALSE}
# has to be raw data
ggplot(seed, aes(y = red, x = trip.no)) +
  geom_point(aes(y = red,color="red"))+
  geom_point(aes(y = silver,color="silver"))+
  geom_point(aes(y = mountain,color="mountain"))+
  stat_summary(color="blue",fun.y="mean",geom="line")+
  facet_grid(~grid.id) +
  theme_bw()
```

#### From the finalised dataset

```{r}
ggplot(seed.paper.2, aes(y = seedm2, x = trip)) +
  geom_point()+
  facet_grid(valley~grid.id) +
  theme_bw() +
  ggtitle("Total seedfall")

ggplot(seed.paper.2, aes(y = cum.seed, x = trip)) +
  geom_point()+
  geom_line() +
  facet_grid(valley~grid.id) +
  theme_bw() +
  ggtitle("Total accumulative seedfall")

ggplot(seed.paper.2, aes(y = log.cum.seed, x = trip)) +
  geom_point()+
  geom_line() +
  facet_grid(valley~grid.id) +
  theme_bw() +
  ggtitle("log(cum.seed) seedfall")
```
