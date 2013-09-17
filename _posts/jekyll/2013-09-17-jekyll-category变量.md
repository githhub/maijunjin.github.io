---
layout: post
title: "jekyll category变量"
category: jekyll 
description: "jekyll category变量的特性"
tags: [jekyll]
---
[原文](http://stackoverflow.com/questions/5672076/nested-liquid-loops-in-a-jekyll-archive-page-not-working-using-an-outer-loop-va)  

When you do for category in site.categories  

- category[0] will give you the category name  
- category[1] will give you the list of posts for that category.

That's the way Liquid handles iteration over hashes, I believe.  

So the code you are looking for is this one:  

    {% raw %}
    {% for category in site.categories %} 
        <h2 id="{{ category[0] }}-ref">{{ category[0] }}</h2>
            <ul>
               {% for post in category[1] %} 
                   <li><a href="{{ post.url }}">{{ post.title }}</a></li> 
               {% endfor %}
            </ul>
            <p><a href="#{{ category[0] }}-ref">&#8617;</a></p>
     {% endfor %}
     {% endraw %}

I've taken the liberty of fixing some markup issues - I've added `<ul>...</ul>` around the post link list, a `<p>` around the last link, a semi-colon after the 8617, and also fixed the id at the top (was missing the -ref part) 

