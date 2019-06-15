---
layout: post
title: "Rendering outputs"
subtitle: "Summary of the different rendering options for blogs and collaborations"
image: /img/filing.jpg
bigimg: /img/first-image1.png
tags: ["compile", "r", "rmd", "RStudio", "tools", "general"]
permalink: simple-outputs.html
---

My outputs from first thoughts about how to quickly input reports from `RStudio` to my `jekyll` blog. 

## Online outputs

At some point I will have a simple workflow here but for now these are the resources I have been working though.

### In main folder

`davan690.github.io`

If I simply copy and paste the rendered file from my `RStudio` working directory to my website by putting the file in the main folder (same location as `index.html`) . When I do this I can access the full `html` file in a the `github` format of html with no headers or other content rendered when the website is built.

##### nb.html format

However when I compile website this is what it looks like... I did not have any plots and rendering with random `.css` I think??

![1560479033428](C:\GIT\davan690.github.io\img\no-plots-rmd.png)

And the back end is baaaad

![1560478977097](C:\GIT\davan690.github.io\img\tag-issues-render-md.png)

So from here I decided to try and render the .html within my `jekyll` build by creating a post and merging the post with my `.rmd` html output file. The attempts are below.

### In posts folder

`_posts`

In the ideal world I think that I just want to end up with a simple post with all the info attached however there are actually a million (maybe over exaggerating here) options on how and where to put the files depending on the rendering.

#### html formats

with these outputs we can actually render `html` files with the `rmarkdown` package in RStudio as a range of different outputs:

- `rmarkdown::hml_document`

- `html_github`
- `html_vigette`
- etc etc...

##### nb.html format

If I simply copy and paste the rendered `nb.html` file from my RStudio working directory to my website folder as:

```{% include Davidson1.html %}```

*And the current output is*

- `'full file name'` = in the post file nothing happens
- `'file name` `nb.html` = 
- `'file name'` `.html` = 
- `yyyy-mm-dd-` `'file name'` `.html` = 

##### html_github

If I simply copy and paste the rendered with the `rmarkdown` package in RStudio as `html_github?` file from my RStudio and inserted into `_posts` folder:

- `'full file name'` = 
- `'file name` `nb.html` = 
- `'file name'` `.html` = 
- `yyyy-mm-dd-` `'file name'` `.html` = 

##### html_vignette

If I simply copy and paste the rendered with the `rmarkdown` package in RStudio as `html_github?` file from my RStudio and inserted into `_posts` folder:

- `'full file name'` = 
- `'file name` `nb.html` = 
- `'file name'` `.html` = 
- `yyyy-mm-dd-` `'file name'` `.html` = 



## My Notes

As I get better at coding and web-development I will create a simple workflow but I have slowly worked through what is running currently.

P.S. I wrote this using `typora`