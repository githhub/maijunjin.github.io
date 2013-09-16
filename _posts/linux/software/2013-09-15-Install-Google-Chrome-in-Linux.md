---
layout: post
title: Google Chrome 29 Released – Install on RHEL/CentOS 6 and Fedora 19/15
description: Install Google Chrome in Linux
keywords: [Chrome,linux]
category : linux
tags: [linux,Chrome]
---
[原文](http://www.tecmint.com/install-google-chrome-on-redhat-centos-fedora-linux/)
Google Chrome is a freeware web browser developed by Google Inc.
Google Chrome team finally announced the release of Google Chrome 29,
the actual version is 29.0.1547.57 for Linux, Mac and Windows operating systems. 
This new version bundled with some exciting features like a new API for high quality video and 
audio communication with minor security and bug fixes. 
If you would like to know more other cool features of this release, 
please visit at [Google’s Chrome Features](https://www.google.com/chrome/intl/en/more/features.html).


Install Google Chrome in Linux
Install Google Chrome in Linux

In our earlier articles we have shown you how to install latest released Opera Browser 12.00 and Firefox 21 versions. In this tutorial we will show you how we have practically installed Google Chrome 29 browser in one of our CentOS 6.4 server using Google’s own repository with Yum tool. By using repository you will keep your Chrome browser up-to-date. However, it should also work on RHEL 6.4/6.3/6.2/6.1/6.0, CentOS 6.4/6.3/6.2/6.1/6.0 and Fedora 19,18,17,16,15 versions as well.
Step 1: Enable Google YUM repository
Create a file called /etc/yum.repos.d/google-chrome.repo and add the following lines of code to it.
[google-chrome]
name=google-chrome
baseurl=http://dl.google.com/linux/chrome/rpm/stable/$basearch
enabled=1
gpgcheck=1
gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub
Step 2: Installing Chrome Web Browser
Download and Install Chrome Web Browser with yum command. It will automatically install all dependencies.
# yum install google-chrome-stable
Update : Sadly, the Google Chrome browser no longer supports the most famous commercial distribution Red Hat and its free clones such as CentOS and Scientific Linux.
Yes, they’ve discontinued support for RHEL 6.X version as of Google Chrome and on other side, latest Firefox and Opera browsers run successfully on the same platforms.
Luckily, there is a script developed by Richard Lloyd, that automatically download and install latest Google Chrome browser by picking libraries from a more recent released distro and put those libraries in (/opt/google/chrome/lib) directory and then you can able to run Google Chrome on CentOS 6.X version.
# wget http://chrome.richardlloyd.org.uk/install_chrome.sh
# chmod u+x install_chrome.sh
# ./install_chrome.sh
Sample Output
Google Chrome Installer 2.00 on the i686 platform
(C) Richard K. Lloyd 2013 <rklloyd@gmail.com>

*** Checking for an update to install_chrome.sh ...

--2013-07-18 17:27:02--  http://chrome.richardlloyd.org.uk/version.dat
Resolving chrome.richardlloyd.org.uk... 193.110.246.53
Connecting to chrome.richardlloyd.org.uk|193.110.246.53|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5 [text/plain]
Saving to: aversion.data

100%[===================================================================================================================>] 5           --.-K/s   in 0s

2013-07-18 17:27:02 (264 KB/s) - aversion.data

*** install_chrome.sh is already the latest version (2.00) - continuing ...

*** Determining latest Google Chrome version number ...
Step 3: Starting Chrome Web Browser
Starting browser with root user.
# google-chrome &
Google Chrome Startup Screen 
Google Chrome Startup Screen
Welcome screen of Chrome web browser.
Google Chrome Welcome Screen
Google Chrome Welcome Screen
Exploring www.tecmint.com with cool Chrome web browser.
Exploring www.tecmint.com in Google Chrome
Exploring www.tecmint.com in Google Chrome
That’s it, enjoy browsing with Chrome and do let me know your browsing experience with Chrome via comments.
Bio
Latest Posts

My Twitter profileMy Facebook profileMy Google+ profile
Narad Shrestha
He has over 10 years of rich IT experience which includes various Linux Distros, FOSS and Networking. Narad always believes sharing IT knowledge with others and adopts new technology with ease.

 
Linux Services & Free WordPress Setup

Our post is simply ‘DIY’ aka ‘Do It Yourself, still you may find difficulties and want us to help you out. We offer wide range of Linux and Web Hosting Solutions at fair minimum rates. Please submit your orders by Clicking Here.
Tweet


4
inShare
61
comments
Database Management Free work from home At home work
Distribution strategy in marketing Advertising Running Shoes
? PREVIOUS POST
A Command Line Web Browsing with Lynx and Links Tools
NEXT POST ?
Install Firefox 23 in RHEL/CentOS 6.4 & Fedora 19/18/17
Related Post(s):
Firefox 17 Released, Adds New Facebook Messenger – Install in Ubuntu 12.04/12.10, Xubuntu 12.10 and Linux Mint 14/13
Install Opera 12.11 (Browser) in RHEL/CentOS 6.3 and Fedora 17/16/15
Install Firefox 14 in RHEL – CentOS – Fedora
Install Firefox 23 in RHEL/CentOS 6.4 & Fedora 19/18/17
A Command Line Web Browsing with Lynx and Links Tools