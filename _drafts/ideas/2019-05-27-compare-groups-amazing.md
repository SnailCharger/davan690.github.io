---
title: CompareGroups 
subtitle: A interface for creating summary tables
permalink: /comparegroups-package.html
layout: post
tags: ["phd", "general", "overview", "website"]
image: /img/compareGroups-gui-shot.jpg
---

The compareGroups package (Subirana, Sanz, and Vila 2014) allows users to create tables displaying results of univariate analyses, stratified or not by categorical variable groupings.

Tables can easily be exported to CSV, LaTeX, HTML, PDF, Word or Excel, or inserted in R-markdown files to generate reports automatically.

![image](/img/compareGroups-gui-shot.jpg)

This package can be used from the R prompt or from a user-friendly graphical user interface for non-R familiarized users.

The compareGroups package is available on CRAN repository. To load the package using the R prompt, enter:

`library(compareGroups)`

This document provides an overview of the usage of the compareGroups package with a real examples, both using the R syntax and the graphical user interface. It is structure as follows:

Introduction of the package (section 2) and the data used as example (section 3),
Instructions to perform descriptive tables and exploration plots using R syntax are explained (section 4), and
Usage of graphical user interface based on tcl-tk (section 5) and based on Shiny (section 6) are shown.

## Tutorials

There is a very good vignette for this package [here]("https://cran.r-project.org/web/packages/compareGroups/vignettes/compareGroups_vignette.html#launch-the-wui-application"). 

I have developed this slightly in my notes as function used for quick descriptive statistics using R and a GUI. For now these notes are on this page. At some stage I plan to move these to there own repository.

## My notes

Here I will put examples of using this package as it may be helpful for future projects.