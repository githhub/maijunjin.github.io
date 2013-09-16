---
layout: post
title: 载入 jQuery 库的最佳方法
description: 载入 jQuery 库的最佳方法
keywords: [jQuery]
category : jQuery
tags: [jQuery]
---
[原文](http://lightcss.com/best-way-to-include-jquery/)
在网站开发的项目中使用Google CDN的jQuery库虽然加载速度很快，但调用本地服务器的库才可以确保万无一失。

<H1>使用方法</H1>
使用下面的代码可以在Google CDN库获取失败时载入本地jQuery库：

    <script type="text/javascript" src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
    <script type="text/javascript">window.jQuery || document.write('<script type="text/javascript" src="/js/libs/jquery.min.js"><\/script>')</script>
在WordPress主题中使用的方法为：

<script type="text/javascript" src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
<script type="text/javascript">window.jQuery || document.write('<script type="text/javascript" src="<?php echo get_template_directory_uri(); ?>/jquery.min.js"><\/script>')</script>
注意事项

因为开头提到的原因，所以建议下载一份 jQuery 官方的 min 库 放到 WordPress 当前使用的主题目录下调用，不要使用 wp-includes 里面的库。
Google CDN 库的地址采用了协议相对路径，它可以很好的解决 https 引起的一些问题，具体可以看 Paul Irish 的介绍，当然你依旧可以使用带「http:」的路径。
许多网站都采用 Google CDN 提供的 jQuery 库，使用它可以得到出色的缓存效果。
把 jQuery 代码统统放到页面底部可以提高载入速度。
使用 HTML5 重构的页面可省略掉 type="text/javascript"。
使用SAE开发者资源

由于 Google 服务在国内缺乏稳定性，为了稳妥，使用 SAE 的开发者资源是个省流量又提高速度的好方法。SAE 为新浪为其应用提供的开发者资源，其中就有 jQuery 库。使用的话非常简单，只要到 SAE 开发者中心 找到合适的地址并替换掉上面代码的 Google CDN 地址即可。例如：

<script type="text/javascript" src="//lib.sinaapp.com/js/jquery/1.9.0/jquery.min.js"></script>
<script type="text/javascript">window.jQuery || document.write('<script type="text/javascript" src="/js/libs/jquery.min.js"><\/script>')</script>
2011.05.25：由于目前 Google 的不稳定，而国内没有好的同类服务，故这已不是最优方案。当然，你把 Google 库路径换成国内稳定且快速的路径（如果存在），依然可以受用此方法带来的各种好处。
2011.06.23：根据 LOO2K 提醒，更新了 SAE 方案。