---
layout: post
title: "Rendering outputs"
subtitle: "Summary of the different rendering options for blogs and collaborations"
image: /img/filing.jpg
bigimg: /img/first-image1.png
permalink: simple-outputs.html
---

My outputs from first thoughts about how to quickly input reports from `RStudio` to my `jekyll` blog. 

## Online outputs

At some point I will have a simple workflow here but for now these are the resources I have been working though.

### In main folder

`davan690.github.io`

If I simply copy and paste the rendered file from my RStudio working directory to my website by putting the file in the `_includes` folder and calling it from the post using jekyll liquid templating as so:

`{% include' ' file name' '.nb.html %}`

However when I compile website this is what it looks like:

` bla image`

And the back end is baaaad

` bla image`

### In posts folder

`_posts`

In the ideal world I think that I just want to end up with a simple post with all the info attached however there are actually a million (maybe over exagerating here) options on how and where to put the files depending on the rendering.

### html formats

with these outputs we can actually render `html` files with the `rmarkdown` package in RStudio as a range of different outputs:

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