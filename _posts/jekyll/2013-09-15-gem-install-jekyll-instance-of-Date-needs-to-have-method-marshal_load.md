---
layout: post
title: gem install jekyll报instance of Date needs to have method marshal_load 
description: gem install jekyll报instance of Date needs to have method marshal_load
keywords: [linux,jekyll]
category : jekyll
tags: [linux,jekyll]
---
    $ ruby -v
    ruby 1.8.7 (2011-06-30 patchlevel 352) [i686-linux]
    $ gem -v
    1.8.10


    $ gem install jekyll
    ERROR:  While executing gem ... (TypeError)
        instance of Date needs to have method `marshal_load'

解决办法：
<br/>升级 Ruby 到 1.9.3+
