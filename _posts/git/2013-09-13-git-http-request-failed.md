---
layout: post
title: git push时候出现HTTP request failed
description: 在Centos6.4 64位系统下， git push时候出现HTTP request failed
keywords: [centos,git]
category : git
tags: [centos,git]
---
<h1>问题如下：</h1>
git的版本

    [user@localhost test]$ git --version
    git version 1.7.1

在Centos6.4 64位系统下，当我使用git push的时候会出现如下的问题：

    [user@localhost test]$ git push
        error: The requested URL returned error: 403 Forbidden while accessing https://github.com/username/repositoryname.git/info/refs
    fatal: HTTP request failed
   [user@localhost test]$ git remote -v
   origin	https://github.com/username/repositoryname.git (fetch)
   origin	https://github.com/username/repositoryname.git (push)
<h1>解决方法：</h1>

    [user@localhost test]$ git remote set-url origin https://username@github.com/username/repositoryname.git
    [user@localhost test]$ git push
    Counting objects: 10, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (5/5), done.
    Writing objects: 100% (6/6), 685 bytes, done.
    Total 6 (delta 2), reused 0 (delta 0)
    To https://username@github.com/username/repositoryname.git
    9e89c81..2a28518  gh-pages -> gh-pages

<br/>另外也可以设置称ssh提交方式，这样在命令行就不用每次都输入讨厌的密码
