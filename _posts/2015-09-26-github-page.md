---
layout: post
title: "开始搞下github pages"
author: cfool
description: ""
category: github
tags: []
---

花费了几天时间搞了下github pages，搭建了本地的jekyll环境，github上创建了对应的repository。然后下载jquery,bootstrap，开始搞自己的Blog模板。记录一下自己的开发过程。


### 创建github page对应的repository
注册github账号的过程就不说了。注册完成后，登录进去，[创建](https://github.com/new)一个新的repository。Repository name一定要填写 username.github.io，username就是自己在github上的用户名，比如我自己就是cfool.github.io。
创建完成后，git clone到本地，就可以开始创建自己的模板，写自己的Blog了。
不喜欢自己写模板的话，可以在网上下载个自己喜欢的jekyll模板，然后自己只需要写自己的Blog就好了。

### 本地安装配置jekyll开发环境
大致分为以下几个步骤：

* 安装ruby
* 安装jekyll

#### 安装ruby
开始搞github pages的时候，电脑上的ruby已经安装好了，忘了什么时候安装的了，也忘了是系统自带还是自己安装的了= =!,这个步骤可以在网上搜一下算了。。（Mac下的安装步骤可以参考[此处](http://www.cnblogs.com/daguo/p/4097263.html)）。

*安装完后记得修改ruby的软件源，通常都是建议修改为淘宝的源。*

#### 安装jekyll

```language-shell
sudo gem install jekyll
sudo gem install rdiscount
```

#### 运行jekyll
    
在你的代码库下执行

```language-shell
jekyll s
```

------------------------------
待续......    
参考资料：

* Jekyll文档 <http://jekyll.bootcss.com/>
* liquid用法 <http://blog.csdn.net/dont27/article/details/38097581>
* Markdown语法说明 <http://www.appinn.com/markdown/>