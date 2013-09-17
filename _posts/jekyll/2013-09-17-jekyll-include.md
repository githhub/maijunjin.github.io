---
layout: post
title: "jekyll include"
category: 
tags: [jekyll]
---

##  Includes

###  If you have small page fragments that you wish to include in multiple places on your site, you can use the include tag.

{% include footer.html %}
####  Jekyll expects all include files to be placed in an _includes directory at the root of your source directory. This will embed the contents of <source>/_includes/footer.html into the calling file.

######You can also pass parameters to an include:

######{% include footer.html param="value" %}
#######These parameters are available via Liquid in the include:

{{ include.param }}
