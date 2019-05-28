---
title: "pocket-data-conversion"
author: "Anthony Davidson"
date: "28/05/2019"
output: html_document
---



Pocket is a tool I use to record webpages, blogs and other dynmics html content that I want to be able to access at a later date. When I choose to use `pocket` over other tools it was for the ability to easily export `html` lists of these saved pages. I have now got the code and data to see if this is possible below. I have used a series of blogs [here](") to start this process.

## Get format in correct structure


```r
# Parse HTML and convert attributes to data frame
library(XML)

file <- "./data/ril_export-zot-tags.html"

doc = htmlParse(file)
nodeset <- getNodeSet(doc, "//a")

# Create data frame
href <- sapply(nodeset, xmlGetAttr, "href")
time_added <- sapply(nodeset, xmlGetAttr, "time_added")
time <- as.POSIXct(as.numeric(time_added), origin="1970-01-01")
tags <- sapply(nodeset, xmlGetAttr, "tags")
tags[tags==""] <- "none"
data <- data.frame(href, time, tags)

# Find unique tags
taglist <- sort(unique(unlist(strsplit(as.character(tags), ","))))

# # Create matrix
tagmatrix <- matrix(0, length(tags), length(taglist))

# Create the tag matrix and transform into a data frame (classification)
for (i in 1:length(taglist)) {
  tagmatrix[grep(paste("\\b", taglist[i], "\\b", sep=""), tags), i] <- 1
}

tagframe <- data.frame(tagmatrix)
names(tagframe) <- taglist

# Concatenate to original data frame and output
data <- data.frame(data, tagframe)
write.table(data, "./data/ril_output.csv", sep=";", col.names=TRUE, row.names=FALSE)
```


```r
# kableExtra::kable(head(data))
```

## Removing tag columns for now


```r
#already saved
taglist
```

```
##   [1] "#matt"                     "#powerhouse"              
##   [3] "#teaching"                 "activites"                
##   [5] "admin"                     "api"                      
##   [7] "arts"                      "bayes"                    
##   [9] "bayesian"                  "bayesian model"           
##  [11] "beech forest"              "blog"                     
##  [13] "books"                     "briefing"                 
##  [15] "business"                  "business day"             
##  [17] "cannabis research"         "capture recapture"        
##  [19] "climate"                   "computers"                
##  [21] "conservation"              "contacts"                 
##  [23] "content"                   "correlation"              
##  [25] "dark science"              "data"                     
##  [27] "data science"              "database"                 
##  [29] "dog"                       "ecology"                  
##  [31] "ecology : nature.com subj" "ecology global network"   
##  [33] "education"                 "fashion"                  
##  [35] "fashion & style"           "figures"                  
##  [37] "fiji"                      "finance"                  
##  [39] "find publication"          "food"                     
##  [41] "fush"                      "gaum"                     
##  [43] "general"                   "genetics"                 
##  [45] "gis"                       "good figures"             
##  [47] "google password hack"      "graduate support dogs"    
##  [49] "gtd"                       "hadleysr"                 
##  [51] "hard drives"               "health"                   
##  [53] "health statistics"         "hunting"                  
##  [55] "iae"                       "ifttt"                    
##  [57] "internet"                  "invasive species"         
##  [59] "investment"                "jags"                     
##  [61] "journals"                  "kids"                     
##  [63] "lens"                      "life"                     
##  [65] "logo_ideas"                "magazine"                 
##  [67] "mapping"                   "marine biology"           
##  [69] "mice"                      "money"                    
##  [71] "movies"                    "mpd_data"                 
##  [73] "multimedia/photos"         "national science foundati"
##  [75] "nature communications - c" "nature pubs"              
##  [77] "naturecomm1"               "naturecomms1"             
##  [79] "network"                   "new york"                 
##  [81] "none"                      "nyt"                      
##  [83] "nz"                        "obituaries"               
##  [85] "open_data"                 "opinion"                  
##  [87] "opportunities"             "osf"                      
##  [89] "personal growth"           "personal interest"        
##  [91] "pest"                      "pest control"             
##  [93] "pfnz"                      "ph"                       
##  [95] "phd"                       "phd_notes"                
##  [97] "pigs"                      "plants"                   
##  [99] "plos one: sortorder=date_" "podcasts"                 
## [101] "politics"                  "population dynamics"      
## [103] "posion"                    "predators"                
## [105] "publication"               "publishing"               
## [107] "r bugs"                    "random"                   
## [109] "rcode"                     "read"                     
## [111] "reader center"             "reading"                  
## [113] "real estate"               "regression"               
## [115] "rmardown templates"        "rmarkdown"                
## [117] "rr"                        "salary"                   
## [119] "scholars"                  "scholarship options"      
## [121] "science"                   "searching"                
## [123] "shiny"                     "slack"                    
## [125] "small mammals"             "smarter living"           
## [127] "social modelling"          "sport"                    
## [129] "sports"                    "srws"                     
## [131] "stat"                      "statistic_network"        
## [133] "statistics"                "style"                    
## [135] "sunday review"             "surfing"                  
## [137] "t magazine"                "tax"                      
## [139] "teach"                     "teaching"                 
## [141] "teachomg"                  "technology"               
## [143] "textmining"                "the upshot"               
## [145] "the weekly"                "theater"                  
## [147] "theme"                     "times insider"            
## [149] "traits"                    "travel"                   
## [151] "trends in ecology & evolu" "twitter"                  
## [153] "u.s."                      "uc"                       
## [155] "university"                "van"                      
## [157] "vc"                        "watching"                 
## [159] "webs"                      "website"                  
## [161] "website issues"            "well"                     
## [163] "wikipedia"                 "work"                     
## [165] "world"                     "writing"                  
## [167] "your money"                "zotero"
```

```r
# names(data)

dat1 <- data %>%
          select(href, time, tags)
```

## Selecting important tags

### For this example I want to extract all the websites I have tagged as zotero


```r
dat2 <- dat1 %>%
          filter(tags == "zotero") %>%
            transmute(webpage = href,
                   access.date = as.Date(time),
                   tags = tags)
```

## My question

How do I search all of the entries to find anything containing the word "zotero"?

*For now my solution is to manually add a "zotero" tag to each entry using the online webpage*

There are now 24 "zotero" records I hacve saved. I will now export them as a csv and add the the `rmd` file as a csv that then can be converted to a `md` post as below.


```r
kableExtra::kable(dat2, format = "markdown")
```



|webpage                                                                                                                  |access.date |tags   |
|:------------------------------------------------------------------------------------------------------------------------|:-----------|:------|
|https://nakhmani.wordpress.com/2011/02/02/mendeley-vs-zotero-comparison/                                                 |2019-05-23  |zotero |
|https://retorque.re/zotero-better-bibtex/                                                                                |2019-05-21  |zotero |
|https://pastebin.com/BNyUf2xN                                                                                            |2019-05-15  |zotero |
|http://guides.library.illinois.edu/c.php?g=627765&p=4379758                                                              |2019-05-11  |zotero |
|https://pvanb.wordpress.com/2010/03/13/sharing-libraries-in-zotero/                                                      |2019-05-11  |zotero |
|https://forums.zotero.org/discussion/65588/is-there-an-open-and-free-endpoint-for-researchers-bibliographical-references |2019-05-09  |zotero |
|https://www.ragazziconsulting.com/?p=592                                                                                 |2019-05-07  |zotero |
|https://blog.rockarch.org/using-zotero-to-create-collaborative-share-able-export-able-bibliographies                     |2019-05-07  |zotero |
|https://www.zotero.org/support/kb/files_not_syncing                                                                      |2019-02-26  |zotero |
|https://www.zotero.org/support/sync#alternative_syncing_solutions                                                        |2019-02-25  |zotero |
|https://zotero-manual.github.io/adding-files/                                                                            |2019-02-25  |zotero |
|https://www.zotero.org/support/kb/webdav_services                                                                        |2019-02-25  |zotero |
|https://libguides.caltech.edu/c.php?g=512725&p=6401109                                                                   |2019-02-12  |zotero |
|https://www.lib.umn.edu/pim/citation/zotero                                                                              |2019-02-12  |zotero |
|https://www.zotero.org/support/kb/mendeley_import                                                                        |2018-11-27  |zotero |
|https://www.resilio.com/blog/sync-stories-zotero-sync-for-academia-anywhere-access                                       |2018-11-24  |zotero |
|https://www.zotero.org/support/dev/web_api/v3/syncing                                                                    |2018-11-24  |zotero |
|https://www.zotero.org/support/quick_start_guide                                                                         |2018-11-23  |zotero |
|https://www.youtube.com/watch?v=5UV6Ce3evUY                                                                              |2018-11-23  |zotero |
|https://www.youtube.com/watch?v=K2MY7Mb-hMQ                                                                              |2018-11-23  |zotero |
|http://libguides.mq.edu.au/referencing-software/zotero                                                                   |2018-11-23  |zotero |
|https://www.zotero.org/support/screencast_tutorials/zotero_tour                                                          |2018-08-05  |zotero |
|https://www.zotero.org/support/sync                                                                                      |2018-08-03  |zotero |
|https://www.zotero.org/support/preferences/advanced#linked_attachment_base_directory                                     |2018-08-03  |zotero |

```r
#save csv
write.csv(dat2, "./data/zotero-hyper-links.csv")
```




