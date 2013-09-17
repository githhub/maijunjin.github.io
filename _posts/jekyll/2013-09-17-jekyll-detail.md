---
layout: post
title: "jekyll细节笔记"
category: 
tags: [jekyll]
---
{% assign openTag = '{%' %}
## h1 to h6 tag
一行以#号开头，可以被解析称H1到H6标签,`#`表示`<H1></H1>`,`##`表示`<H2></H2>`以此类推。
## li标签
**空一行**，新行开头`- `表示`li`标签
##文字高亮

    {% raw %}
    {% highlight text %}
    {% endhighlight %}
    {% endraw %}

##Liquid不要解析
就像我上面的代码一样，把代码包围在`{% raw %}{% raw %}{% endraw%}{{ openTag }} endraw %}`中,[raw的结束标签怎么输出来是技术活](/jekyll/2013/09/18/如何在jekyll中输出%7B%25-endraw-%25%7D.html)

##代码格式化
行首四个空格

##加上代码的样式
<div>使用`code`</div>  
这也是输出html标签的一种方式
##Markdown不要解析
Markdown won't process anything in block-level HTML tag，所以就加上`<div></div>`就可以了

##换行
在行的结尾加上两个空格
##输出文章的地址

    {% raw %}[Last time]({% post_url 2013-06-09-writing-about-jekyll-in-jekyll %}){% endraw %}
