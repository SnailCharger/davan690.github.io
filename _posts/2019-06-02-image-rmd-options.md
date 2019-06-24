---
title: image options
subtitle: Draft
layout: post
tags: ["phd", "invasive", "overview", "thesis", "tools", "general"]
image: /img/tools.jpg
bigimg: /img/tools.jpg
permlink: /image-options-current.html
---

Here is a simple step through of my issues with adding and working with images in RStudio and all the different options to get the correct images and code into a manuscript or website.

It is all about `paths`...and links... I think. And its taking me ages to get my head around it but here are my notes.

## This is what is working

Right now I have used...

```note the units for images are *always*`bmp``postscript``pdf``png``svg``jpeg``pictex``tiff``win.metafile``cairo_pdf``cairo_ps``CairoJPEG``CairoPNG``CairoPS``CairoPDF``CairoSVG``CairoTIFF``Cairo_pdf``Cairo_png``Cairo_ps``Cairo_svg``tikz``quartz``quartz_pdf``quartz_png``quartz_jpeg``quartz_tiff``quartz_gif``quartz_psd``quartz_bmp``quartz()`My notes```

So at the moment I do this:

- `dev.args`: (`NULL`) more arguments to be passed to the device, e.g. `dev.args=list(bg='yellow', pointsize=10)`; note this depends on the specific device (see the device documentation); when `dev` has multiple elements, `dev.args` can be a list of lists of arguments with each list of arguments to be passed to each single device, e.g. `<<dev=c('pdf', 'tiff'), dev.args=list(pdf = list(colormodel = 'cmyk', useDingats = TRUE), tiff = list(compression = 'lzw'))>>=`

- `fig.ext`: (`NULL`; character) file extension of the figure output (if `NULL`, it will be derived from the graphical device; see `knitr:::auto_exts` for details)

- `dpi`: (`72`; numeric) the DPI (dots per inch) for bitmap devices (`dpi * inches = pixels`)

- `fig.width`, `fig.height`: (both are `7`; numeric) width and height of the plot, to be used in the graphics device (in inches) and have to be numeric

- `fig.asp`: (`NULL`; numeric) the aspect ratio of the plot, i.e. the ratio of height/width; when `fig.asp` is specified, the height of a plot (the chunk option `fig.height`) is calculated from `fig.width * fig.asp`

- `fig.dim`: (`NULL`; numeric) if a numeric vector of length 2, it gives `fig.width` and `fig.height`, e.g., `fig.dim = c(5, 7)` is a shorthand of `fig.width = 5, fig.height = 7`; if both `fig.asp` and `fig.dim` are provided, `fig.asp` will be ignored (with a warning)

- ```
  out.width
  ```

  ,

   

  ```
  out.height
  ```

  : (

  ```
  NULL
  ```

  ; character) width and height of the plot in the final output file (can be different with its real

   

  ```
  fig.width
  ```

   

  and

   

  ```
  fig.height
  ```

  , i.e. plots can be scaled in the output document); depending on the output format, these two options can take flexible values, e.g. for LaTeX output, they can be

   

  ```
  .8\\linewidth
  ```

  ,

   

  ```
  3in
  ```

   

  or

   

  ```
  8cm
  ```

   

  and for HTML, they may be

   

  ```
  300px
  ```

   

  (do not have to be in inches like

   

  ```
  fig.width
  ```

   

  and

   

  ```
  fig.height
  ```

  ; backslashes must be escaped as

   

  ```
  \\
  ```

  ); for LaTeX output, the default value for

   

  ```
  out.width
  ```

   

  will be changed to

   

  ```
  \\maxwidth
  ```

   

  which is defined

   

  here

  - `out.width` can also be a percentage, e.g. `'40%'` will be translated to `0.4\linewidth` when the output format is LaTeX

- `out.extra`: (`NULL`; character) extra options for figures, e.g. `out.extra='angle=90'` in LaTeX output will rotate the figure by 90 degrees; it can be an arbitrary string, e.g. you can write multiple figure options in this option; it also applies to HTML images (extra options will be written into the `<img />` tag, e.g. `out.extra='style="display:block;"'`)

- `fig.retina`: (`1`; numeric) this option only applies to HTML output; for [Retina displays](http://en.wikipedia.org/wiki/Retina_Display), setting this option to a ratio (usually 2) will change the chunk option `dpi` to `dpi * fig.retina`, and `out.width` to `fig.width * dpi / fig.retina` internally; for example, the physical size of an image is doubled and its display size is halved when `fig.retina = 2`

- `resize.width`, `resize.height`: (`NULL`; character) the width and height to be used in `\resizebox{}{}` in LaTeX; these two options are not needed unless you want to resize tikz graphics because there is no natural way to do it; however, according to **tikzDevice** authors, tikz graphics is not meant to be resized to maintain consistency in style with other texts in LaTeX; if only one of them is `NULL`, `!` will be used (read the documentation of **graphicx** if you do not understand this)

- `fig.align`: (`'default'`; character) alignment of figures in the output document (possible values are `left`, `right` and `center`; default is not to make any alignment adjustments); note that for Markdown output, forcing figure alignments will lead to the HTML tag `<img />` instead of the original Markdown syntax `![]()`, because Markdown does not have native support for figure alignments (see [#611](https://github.com/yihui/knitr/issues/611))

- `fig.env`: (`'figure'`) the LaTeX environment for figures, e.g. set `fig.env='marginfigure'` to get `\begin{marginfigure}`

- `fig.cap`: (`NULL`; character) figure caption to be used in a figure environment in LaTeX (in `\caption{}`); if `NULL` or `NA`, it will be ignored, otherwise a figure environment will be used for the plots in the chunk (output in `\begin{figure}` and `\end{figure}`)

- `fig.scap`: (`NULL`; character) short caption; if `NULL`, all the words before `.`or `;` or `:` will be used as a short caption; if `NA`, it will be ignored

- `fig.lp`: (`'fig:'`; character) label prefix for the figure label to be used in `\label{}`; the actual label is made by concatenating this prefix and the chunk label, e.g. the figure label for `<<foo-plot>>=` will be `fig:foo-plot`by default

- `fig.pos`: (`''`; character) a character string for the figure position arrangement to be used in `\begin{figure}[fig.pos]`

- `fig.subcap`: (`NULL`) captions for subfigures; when there are multiple plots in a chunk, and neither `fig.subcap` nor `fig.cap` is NULL, `\subfloat{}`will be used for individual plots (you need to add `\usepackage{subfig}`in the preamble); see [067-graphics-options.Rnw](https://github.com/yihui/knitr-examples/blob/master/067-graphics-options.Rnw) for an example

- `fig.ncol`: (`NULL`; integer) the number of columns of subfigures; see [here](https://github.com/yihui/knitr/issues/1327#issuecomment-346242532)for examples (note that `fig.ncol` and `fig.sep` only work for LaTeX output)

- `fig.sep`: (`NULL`; character) a character vector of separators to be inserted among subfigures; when `fig.ncol` is specified, `fig.sep` defaults to a character vector of which every N-th element is `\newline` (where `N` is the number of columns), e.g., `fig.ncol = 2` means `fig.sep = c('', '', '\\newline', '', '', '\\newline', '', ...)`

- `fig.process`: (`NULL`) a function to post-process a figure file; it should take a filename, and return a character string as the new source of the figure to be inserted in the output

- `fig.showtext`: (`NULL`) if `TRUE`, call `showtext::showtext.begin()` before drawing plots; see the documentation of the [**showtext**](http://cran.rstudio.com/package=showtext) package for details

- `external`: (`TRUE`; logical) whether to externalize tikz graphics (pre-compile tikz graphics to PDF); it is only used for the `tikz()` device in the **tikzDevice** package (i.e., when `dev='tikz'`) and it can save time for LaTeX compilation

- `sanitize`: (`FALSE`; character) whether to sanitize tikz graphics (escape special LaTeX characters); see documentation in the **tikzDevice** package

Note any number of plots can be recorded in a single code chunk, and this package does not need to know how many plots are in a chunk in advance – it can figure out automatically, and name these images as `fig.path-label-i`where `i` is incremental from 1; if a code chunk does not actually produce any plots, **knitr** will not record anything either (the graphics device is open *only when plots are really produced*); in other words, it does not matter if `fig.keep='high'` but no plots were produced.

Low-level plotting commands include `lines()` and `points()`, etc. To better understand `fig.keep`, consider the following chunk:

```r
<<test-plot>>=
plot(1)         # high-level plot
abline(0, 1)    # low-level change
plot(rnorm(10)) # high-level plot
## many low-level changes in a loop (a single R expression)
for(i in 1:10) {
    abline(v = i, lty = 2)
}
@
```

Normally this produces 2 plots in the output (i.e. when `fig.keep='high'`); for `fig.keep='none'`, no plots will be saved; for `fig.keep='all'`, 4 plots are saved; for `fig.keep='first'`, the plot produced by `plot(1)` is saved, and for `fig.keep='last'`, the last plot with 10 vertical lines is saved.

#### options as simple as

| Step  | Bookdown                                                     |                          RMarkdown                           | Markdown github                                              | HTML                                        |
| ----- | ------------------------------------------------------------ | :----------------------------------------------------------: | ------------------------------------------------------------ | ------------------------------------------- |
| One   | `.Rmd` file to begin with `analysis` folder                  | Images can be managed using `knitr` (both globally and within each chunk) | Using a simple markdown code that uses squared brackets and rounded brakes. | Basic and old-school but allows image links |
| Two   | Use `.Rmd` files as reports for each `.R` script of importance |                ```# {r image-using-knitr}```                 | `![image](./_assets/img/compareGroups-gui-shot.jpg){ width=50% }` |                                             |
| Three | Render figures for overall manuscript to the main `/figs/` folder. (needs `../`) | Can be done with the plot data (summaries and reconstructions of the originally collected data) | This needs to be a a set size to begin with and then easy to “slightly” shift |                                             |

But now that I have rendered my first publication in `bookdown` [here](www.ssnhub.com/beech-forest-dynamics/) it has become much easier to manage manuscript figures for size using the same two steps above.