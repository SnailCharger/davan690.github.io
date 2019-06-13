---
layout: post
title: "Code chunks"
subtitle: "Trying to link RMarkdown to Jekyll"
tags: ["test", "tools","rmd", "rstudio","home"]
image: /img/testing-image.jpg
permlink: /markdown-chunks.html
---

## Option 1

~~~
var foo = function(x) {
  return(x + 5);
}
foo(3)
~~~

## Option 2

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```

## Option 3

And here is the same code yet again but with line numbers:

{% highlight javascript linenos %}
var foo = function(x) {
  return(x + 5);
}
foo(3)
{% endhighlight %}

## Boxes
You can add notification, warning and error boxes like this:

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.