---
layout: post
title: git revert (reset) a single file
description: git复原单个文件
keywords: [git]
category : git
tags: [git]
---
[原文](http://www.norbauer.com/rails-consulting/notes/git-revert-reset-a-single-file.html)  

This one is hard to find out there so here it is. If you have an uncommitted change (its only in your working copy) that you wish to revert (in SVN terms) to the copy in your latest commit, do the following:

    git checkout filename

This will checkout the file from HEAD, overwriting your change. This command is also used to checkout branches, and you could happen to have a file with the same name as a branch. All is not lost, you will simply need to type:

    git checkout -- filename

You can also do this with files from other branches, and such. man git-checkout has the details.  

The rest of the Internet will tell you to use git reset --hard, but this resets all uncommitted changes you’ve made in your working copy. Type this with care(小心点).
