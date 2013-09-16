---
layout: post
title: INSTALLING RUBY, RUBYGEMS, RAILS, AND MONGREL ON MAC OS X 10.5 (LEOPARD) 
description: 在mac上源码安装RUBY,RUBYGEMS,RAILS,MONGEL
keywords: [ruby,rubygems,source,mac]
category : ruby
tags: [ruby,rubygems,source,mac]
---
[这篇文章的来源](http://hivelogic.com/articles/ruby-rails-leopard)<br/>

These are instructions for compiling and installing Ruby, Rubygems, Ruby on Rails, and Mongrel on Mac OS X 10.5 (Leopard).

If you already know why I write these tutorials, if you already have /usr/local in your path, if you’ve installed XCode installed 
already … in other words, if you’re an old-school Hivelogic reader, [just click here to jump right to the instructions](http://hivelogic.com/articles/ruby-rails-leopard#ruby).

<H1>THE FAQ (SORT OF)</H1>
Below I’ll walk you through getting your system ready for building and compiling open source software. But before I do, please allow 
me to answer of few of the questions I invariably(adv. 总是；不变地；一定地) get asked every time I release this type of do-it-yourself 
tutorials:

<H2>Why would I want to compile this stuff when it ships as part of Leopard?</H2>

Good question! Leopard ships with Ruby 1.8.6 and Rails 1.2.3 – both respectably(adv. 相当好地；体面地；可敬地) recent and stable versions.
And it’s easy enough to update to the latest version of Rails with a single command (sudo gem install rails if you’re curious).

Then why roll your own? I expand on(详述) the benefits of building your own open source utilities (like Ruby and Rails) and why where they live 
is important in my article entitled(题为) [Using /usr/local](http://hivelogic.com/articles/using_usr_local/), but here are a few of the 
reasons:

<li>You want to run the latest/greatest versions of available software and don’t want to wait (or hope) for Apple to release an update.</li>
<li>Your want to update, tweak([俚语]【计算机】对…稍作调整，对程序微调), and customize your own tools while keeping your system “stock” from Apple’s standpoint.<li>
<li>Apple may decide to modify these utilities during a system update, and doing so may break your stuff.</li>
<li>You can move or remove the /usr/local filesystem, or even transfer it to another machine in one step.</li>
<li>You’re used to, interested in, or curious about in the compile and build process.</li>
For some people, these reasons are enough to take a few minutes to build your own software.

<h1>Why wouldn’t I just use MacPorts or Fink?(MacPorts和Fink是两个开源项目)</H1>

Both MacPorts and Fink are great projects, and I wholeheartedly support their efforts. I’m also a longtime FreeBSD geek, and the FreeBSD ports
tree is something I’ve relied upon(依靠) for ages. So I really get what MacPorts and Fink are about.

On the other hand, I’m a geek at heart, I don’t mind compiling my own software, and I like the ability to build just what I need, right when I need it, without installing or waiting for any additional or externally-maintained software. If this method sounds like a headache to you, I know where you’re coming from. MacPorts and Fink provide most excellent alternatives. Tell them I sent you.

<H2>I used your instructions and I got the following error …</H2>

Please don’t email me about it but instead, post your question in the comments. I try and read and respond as often as I can. When I can’t, other Hivelogic readers often step in and try to help (they’re a great bunch), and usually we can figure it out together.

<H1>PREREQUISITES</H1>
You will need:

<LI>Mac OS X 10.5 (Leopard)</LI>
<LI>Xcode 3.0 or newer</LI>
<LI>Familiarity with (or willingness to use) the Mac OS X Terminal application</LI>
Note: You will probably need to install Xcode from the Mac OS X install DVD/CD (in the Optional Installs → Xcode folder). You can also download 
it from [Apple’s Developer Connection](https://developer.apple.com/) free of charge.

Another Note: These instructions are written for people using the default Mac OS X shell, bash. If you haven’t manually(adv. 手动地；用手) changed your shell 
from bash, and you didn’t upgrade to Leopard from something older than Tiger, then you don’t have anything to worry about. If you’ve taken 
specific steps to change the default shell to something other than bash (like tcsh), then you’ll need to figure out equivalent syntax to 
use when setting paths and environment variables, or just switch back to bash, because we just roll with bash here. Sorry.

<H1>JUST IN CASE</H1>
While it’s unlikely that any of these steps might damage your system somehow, it’s probably a good idea to have a current backup of 
everything, just in case(以防万一) (I recommend SuperDuper! for this by the way(顺便说说，顺便问一下), awesome product). So you’re following 
these instructions at your own risk, and I’m not liable(adj. 有责任的) for anything that happens.

<H1>A NOTE ABOUT SUDO</H1>
With great power comes great responsibility, so Mac OS X may prompt you for your password prior to(在……之前；居先) executing some of the commands 
you’ll be typing. It may do this only once, or several times throughout this process. Just re-enter your password as needed.

<H1>USING TERMINAL</H1>
You’ll need to launch the Terminal application. It can be found in the /Applications/Utilities folder.

Each of the lines below appearing in monospaced type(等宽字体) should be entered into Terminal, and be followed by the Return key.

<H1>PATHS</H1>
<H2>Don’t skip this step!</H2>

Mac OS X, like other UNIX systems, uses something called a path to determine where it should look for applications on the command 
line (that is, when you’re using the Terminal app). The path is actually an environment variable, set by a special file that’s automatically
 executed when you open a new Terminal window.

We need to make sure that our path is set to look for files in /usr/local (the place where we’ll be installing the tools) before looking 
anywhere else. This is important.

To see if the path has been set properly, we can check the contents of the .profile file (the special file hidden in our home folder) for 
a PATH line using a text editor. TextMate, TextWrangler, BBEdit, and vi are all perfectly good options. To open the file with TextMate, 
for example, we can type:

     mate ~/.profile

This will open the file if it already exists, or open a blank file if it doesn’t. Add the following line at the very end of the file:

     export PATH="/usr/local/bin:/usr/local/sbin:/usr/local/mysql/bin:$PATH" 
Now save and close the file.

It doesn’t matter how many other lines there are in the file, or what they say or do. Just make sure that this line comes last and you 
should be fine.

To make sure the changes are picked up correctly, we now need to execute the file with the following command:

    . ~/.profile
It’s likely there will be no response from the shell here, just the prompt, but that’s OK, the changes have been picked up and we’re ready 
to move on.

You can also close your Terminal and open a new one instead if you’d like.

Note: You may have noticed that I’ve added MySQL to the path in the line above. That’s because most users will be installing MySQL later 
in this tutorial. If you’re the type to want to use something like SQLite or PostGreSQL as your database instead of MySQL, you can feel 
free to omit the /usr/local/mysql/bin: bit from the line above, and replace it with the path to the database of your choice. If this note 
doesn’t make sense to you, even if you don’t plan to install MySQL later, just keep on going … the extra bit in the path statement won’t 
affect you at all.

<H1>SETTING UP</H1>
I like to create a folder to contain all of the downloaded files and their respective build folders. I tend to keep this folder around 
indefinitely. Source code doesn’t take up much space, and it’s useful to refer back to later to remind yourself of previous installation 
details or techniques, installed versions, for a fast install at a later time, or in case you want to uninstall something.

For these examples, we’ll create a folder called src in the /usr/local section of the filesystem, and change directories into that folder. 
It will be our workspace for everything we do here:

    sudo mkdir -p /usr/local/src
    sudo chgrp admin /usr/local/src
    sudo chmod -R 775 /usr/local/src
    cd /usr/local/src
You’ll download and compile everything in this new folder.

<H1>RUBY</H1>
Ok, let’s get started. Unlike previous versions of Mac OS X, Leopard has everything you’ll need to compile Ruby. You don’t need to install 
any prerequisites. Take these commands and type or paste them into Terminal:

    curl -O ftp://ftp.ruby-lang.org/pub/ruby/1.8/ruby-1.8.7-p72.tar.gz
    tar xzvf ruby-1.8.7-p72.tar.gz
    cd ruby-1.8.7-p72
    ./configure --enable-shared --enable-pthread CFLAGS=-D_XOPEN_SOURCE=1
    make
    sudo make install
    cd ..
    
我安装的是最新的：

    curl -O http://cache.ruby-lang.org/pub/ruby/2.0/ruby-2.0.0-p247.tar.gz
    tar xzvf ruby-2.0.0-p247.tar.gz
    cd ruby-2.0.0-p247
    ./configure --enable-shared --enable-pthread CFLAGS=-D_XOPEN_SOURCE=1
    make
    sudo make install(这里需要输入密码，不知道为什么是我自己的密码,而不是超级管理员的密码)


To verify that Ruby is installed and in your path, just type:

    which ruby
或者是这样：
    USERtekiiMac-3:src user$ which ruby
    /usr/local/bin/ruby
    USERtekiiMac-3:src user$ ruby --version
    ruby 1.8.7 (2012-02-08 patchlevel 358) [universal-darwin12.0](系统自带的版本)
    USERtekiiMac-3:src user$ /usr/local/bin/ruby --version
    ruby 2.0.0p247 (2013-06-27 revision 41674) [x86_64-darwin12.1.0]
You should see:

    /usr/local/bin/ruby
If you don’t, you haven’t set your path correctly.

<h1>RUBYGEMS</H1>
With Ruby installed, we can move on to RubyGems. Same routine:

    curl -O http://rubyforge.iasi.roedu.net/files/rubygems/rubygems-1.3.1.tgz
    tar xzvf rubygems-1.3.1.tgz
    cd rubygems-1.3.1
    sudo /usr/local/bin/ruby setup.rb
    cd ..
    
我自己的：

    curl -O  http://rubyforge.org/frs/download.php/76729/rubygems-1.8.25.tgz（下载不了，只好用浏览器下载之后拷贝过来）
    tar xzvf rubygems-1.8.25.tgz
    cd rubygems-1.8.25
    sudo /usr/local/bin/ruby setup.rb
    cd ..
    
<H1>RUBY ON RAILS</H1>
At last, we’re ready to install Rails. RubyGems will handle this for us:
    su root(输入密码)
    gem install rails
Mongrel and Capistrano get installed the same way:

    sudo gem install mongrel
    sudo gem install capistrano
There are a handful(n. 少数；一把；棘手事) of other gems you’ll undoubtedly want, and you can install them one at a time, or all on one line 
(if you have a list) like this:

    sudo gem install RedCloth termios rspec sake
<H1>THE MYSQL GEM</H1>
As of(自……起) Rails 2.0, the default database system is is now SQLite, which also ships with Leopard.

Many of us still run MySQL locally though, and want to install the MySQL gem for better Rails integration. If you followed my MySQL for 
Mac OS X installation instructions or used one of the official MySQL distributions, your MySQL lives in /usr/local/mysql. You can install 
the gem using the following command:

    sudo gem install mysql -- --with-mysql-dir=/usr/local/mysql
<H1>WE’RE DONE</H1>
Congratulations, you now have a custom-built, properly installed Ruby on Rails system! You might also like to build your own Subversion 
client or run your own MySQL server too.
