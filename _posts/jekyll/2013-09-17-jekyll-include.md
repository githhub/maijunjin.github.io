---
layout: post
title: "jekyll include"
category: 
tags: [jekyll]
---

##  Includes

If you have small page fragments that you wish to include in multiple places on your site, you can use the include tag.  

    {% include footer.html %}

Jekyll expects all include files to be placed in an _includes directory at the root of your source directory. This will embed the contents of `<source>/_includes/footer.html` into the calling file.  

You can also pass parameters to an include:

    {% include footer.html param="value" %}

These parameters are available via Liquid in the include:

    {{ include.param }}

在研究过程中，发现include标签应该是不能够使用变量作为参数的，比如：
    
    {% assign pages_icons = site.categories.usage %}
    {% include pages_icons %}

刚开始看不明白，理解成为目录下面的所有文章都被包含进来，后来才明白，`{% include pages_icons %}`是包含了_include目录下面的pages_icons文件，里面需要用到pages_icons变量
