---
title: macOS code for the jekyll programmer
layout: post
tags: ["phd", "tools", "reproducibility"]
---

I am just learning how to run Jekyll on my local computer for testing and have been unsuccessful over the past few weeks on my windows PC (uni computer). I have now installed and successfully build my github/jekyll site on my MAC and now have to do it again. 

Here are my short reminder steps:

Before these steps there are some issues I am having with `sudo install jekyll` most times and I think this is because I am saving gem files in the wrong locations. But for now its working with davids test account.

Pre.1 Install Jekyll: `sudo install jekyll`

1. Open `bash` terminal

2. Locate the file location of the website

`cd Desktop/`

3. Check the correct place

`pwd`

4. Load site

`bundle jekyll serve`

- if this does not work (with no jekyll found)

Then we need to build jekyll then serve....as so


And that should be it....

<-input image of this here->

## Tutorials and notes

There notes are directly taken from an online [Ucedmy]("") course that I did actually pay for after I couldn't make it work on windows. I would totally recommend this simple course in Jekyll to get on top of everything you can collect in bits over web searches.

The key commands at the moment for me are:

bundle exec jekyll build
bundle exec jekyll serve
bundle exec jekyll serve --watch
[cmd + c]