---
title: "Staticman-comments"
subtitle: "For Static site generators"
permalink: /staticman-comms.html
layout: post
---

Very advanced: Local development
Beautiful Jekyll is meant to be so simple to use that you can do it all within the browser. However, if you’d like to develop locally on your own machine, that’s possible too if you’re comfortable with command line. Follow these simple steps to do that with Vagrant:

Install VirtualBox and Vagrant
Clone your fork git clone git@github.com:yourusername/yourusername.github.io.git
Inside your repository folder, run vagrant up
View your website at http://0.0.0.0:4000 on *nix or http://127.0.0.1:4000 on Windows.
Commit any changes and push everything to the master branch of your GitHub repository. GitHub Pages will then rebuild and serve your website automatically.
Disclaimer: I personally am NOT using local development so I don’t know much about running Jekyll locally. If you follow this route, please don’t ask me questions because unfortunately I honestly won’t be able to help!

Additionally, if you choose to deploy Jekyll using a local ruby installation, you can tell Jekyll to automatically categorize your blog posts by tags. You just need to set link-tags: true in _config.yml. Jekyll will then generate a new page for each unique tag which lists all of the posts that belong to that tag.

**BEautiful template notes** [here](https://w4ngatang.github.io/template-instructions/#basic-features)
## Tutorials




## My notes