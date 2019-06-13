---
layout: post
title: "Small data project outputs"
image: /img/hello_world.jpeg
bigimg: /img/first-image1.png
permalink: small-project-formats.html
---

I have been looking for a quick work-around for compiling my static site ([jekyll](https://jekyllrb.com/)). I thought that this would be a `nb.html` output produced for `RStudio`. THis is what I found...

**Quick fact == it wasn't fast...**

## Tutorials

## My notes

I found two work-arounds on the comment feed of GIThub [here](https://github.com/rstudio/rmarkdown/issues/1020).

#### Someone in the feed even said

"@bkeepers It would be awesome if we could get R Notebooks to render on GitHub the same way that Jupyter notebooks currently render. This should be very straightforward as R Notebooks are actually valid HTML files that can be rendered as-is (see http://rmarkdown.rstudio.com/r_notebooks.html#notebook_file)."

### Option 1

Here's a simple example: https://github.com/karthik/rmarkdown-notebook/blob/master/test.nb.html

### Option 2

```
Agree with @RaoOfPhysics, perhaps this issue belongs to github (unless @yihui can come up with a way to generate a symlink when rendering the notebook, but I am sure there are many reasons not to).

I didn't want to use a first page and then divide by topics, since I just wanted to have a single topic within my repo. On Windows 10, I did it like this:

1. Open a cmd prompt as administrator
Navigate to your repo `cd "C:\Users\MyName\Documents\GitHub\MyRepo"`

2. Generate a symlink with mklink. This is used as mklink "linkfile" "to_this_file". In this case:
mklink "index.html" "index.nb.html"

3. Commit and push to your repo
Here is a site working like this
```

### Option 3

```This would be up to GitHub to render the .nb.html files here. Not sure RStudio can do much about it.

My solution is to use GitHub Pages to render my notebooks. I create directories named after specific notebooks (say, topic), and then have an index.Rmd file that generates the index.nb.html file. I then create a symlink called index.html pointing to index.nb.html so that you can view the content by simply going to ../notebooks/topic rather than ../notebooks/topic/index.nb.html.

You'll need to create the symlinks on a *NIX system and then push it to GitHub, though, as far as I can tell -- I might be wrong!

e.g. repo: https://github.com/RaoOfPhysics/phd-notebooks
The individual notebooks (in their respective directories) are rendered here: https://raoofphysics.github.io/phd-notebooks/
Example notebook: https://raoofphysics.github.io/phd-notebooks/benefits/
The index.html file in that directory points to https://raoofphysics.github.io/phd-notebooks/benefits/index.nb.html
The .Rmd file can be grabbed here: https://raoofphysics.github.io/phd-notebooks/benefits/index.nb.html https://raoofphysics.github.io/phd-notebooks/benefits/index.Rmd
You can also use ggplotly() to make the plots you render interactive. I've not done so for these notebooks, although I have tested it.
```

### Option 4

[Test .Rmd notebooks within Jupyter using online mybinder.org service ](https://github.com/mwouts/jupytext/issues/19)

### Option 5

[GIThub documents](https://rmarkdown.rstudio.com/github_document_format.html)

### Option 6

[Python](https://www.nbinteract.com/)
- In partiuclar convert to markdown [here](https://nbconvert.readthedocs.io/en/latest/usage.html#convert-markdown)

### Option 7

JUST USE `bookdown` or suchlike