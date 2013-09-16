---
layout: post
title: 在安装rdiscount的报错
description: 在安装rdiscount的报错
keywords: [ruby,rdiscount,mac]
category : ruby
tags: [ruby,rdiscount,mac]
---
[source](https://github.com/brianmario/mysql2/issues/371)

    gem install rdiscount

<H1>results:</H1>
<H2>The following warning/error:</H2>

    Parsing documentation for rdiscount-2.0.7.2
    unable to convert "\xCF" from ASCII-8BIT to UTF-8 for lib/rdiscount.bundle, skipping


<H2>Full output:</H2>
		
    mes-MacBook-Pro:~ me$ gem install rdiscount
    Fetching: rdiscount-2.0.7.2.gem (100%)
    Building native extensions.  This could take a while...
    Successfully installed rdiscount-2.0.7.2
    Parsing documentation for rdiscount-2.0.7.2
    unable to convert "\xCF" from ASCII-8BIT to UTF-8 for lib/rdiscount.bundle, skipping
    Installing ri documentation for rdiscount-2.0.7.2
    1 gem installed
    mes-MacBook-Pro:~ me$

<H1>解决方法：</H1>
must install rdoc 4.0.1 or higher