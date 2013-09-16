---
layout: post
title: jekyll server报cannot load such file -- posix_spawn_ext (LoadError) 
description: jekyll server报没有 posix_spawn_ext
keywords: [linux,jekyll]
category : jekyll
tags: [linux,jekyll]
---
想要git clone [realjenius](https://github.com/realjenius/realjenius.com)的jekyll项目来研究研究，但是jekyll server的时候报如下的错误：

    [user@localhost realjenius.com]$ jekyll server
    Configuration file: /home/user/mycode/jekyll/realjenius.com/_config.yml
            Source: /home/user/mycode/jekyll/realjenius.com
       Destination: /home/user/jekyll/realjenius.com/_site
      Generating...   Liquid Exception: cannot load such file -- posix_spawn_ext in _posts/java/2009-09-10-brackets-in-java-annotation-parameters.md
    /usr/local/lib/ruby/site_ruby/2.0.0/rubygems/core_ext/kernel_require.rb:53:in `require': cannot load such file -- posix_spawn_ext (LoadError)
	from /usr/local/lib/ruby/site_ruby/2.0.0/rubygems/core_ext/kernel_require.rb:53:in `require'

测试一下是不是真的没有这个posix_spawn_ext文件，结果：

    [user@localhost realjenius.com]$ ruby -e "require 'posix-spawn'"
    /usr/local/lib/ruby/site_ruby/2.0.0/rubygems/core_ext/kernel_require.rb:53:in `require': cannot load such file -- posix_spawn_ext (LoadError)
	from /usr/local/lib/ruby/site_ruby/2.0.0/rubygems/core_ext/kernel_require.rb:53:in `require'

果然是
<br/>
再查看一下是否真的没有：

    [root@localhost test]# gem uninstall posix-spawn
        You have requested to uninstall the gem:
	    posix-spawn-0.3.6

        pygments.rb-0.5.2 depends on posix-spawn (~> 0.3.6)
        If you remove this gem, these dependencies will not be met.
        Continue with Uninstall? [yN]  

有安装posix-spawn,算了，重新安装：

    [root@localhost test]# gem install posix-spawn -V

安装成功之后，测试一下:
    [user@localhost test]$ ruby -e "require 'posix-spawn'"
    [user@localhost test]$ 

其他类似错误：

    /usr/local/lib/ruby/site_ruby/2.0.0/rubygems/core_ext/kernel_require.rb:53:in `require': cannot load such file -- yajl/yajl (LoadError)

    [user@localhost test]# gem install yajl-ruby -V

