# 网站维护


## 1. 如何发布一篇新的帖子
以要新发布一篇名为maintain.md的帖子为例：
```shell
hugo new content /posts/maintain.md
```
该文件会被加入`content/posts`文件夹中。新的网页文件会被渲染。

通过修改参数可以更改网页配置，具体信息查阅FixIt文档。
```markdown
---
title: 网站维护
subtitle: 介绍维护该网站的常用方法
date: 2024-05-14T20:58:28-05:00
slug: b7b4b1f
draft: true
author:
name: Feiyang Wu
link:
email:
avatar: /avatar_img/avatar.jpg
description:
keywords:
license:
comment: false
weight: 0
tags:
- 网站维护
categories:
- 网站维护
hiddenFromHomePage: false
hiddenFromSearch: false
hiddenFromRss: false
hiddenFromRelated: false
summary:
resources:
- name: featured-image
src: featured-image.jpg
- name: featured-image-preview
src: featured-image-preview.jpg
toc: true
math: false
lightgallery: false
password:
message:
repost:
enable: true
url:

# See details front matter: https://fixit.lruihao.cn/documentation/content-management/introduction/#front-matter
---
```
以上是本页面的配置信息。如果要渲染该页面，需要将`draft`值从默认的`true`改为`false`。

## 2. 添加菜单内容
找到hugo设置文件`hugo.toml`，加入菜单设置：
```toml
[menu]
    [[menu.main]]
        identifier = &#34;archives&#34;
        parent = &#34;&#34;
        # you can add extra information before the name (HTML format is supported), such as icons
        pre = &#34;&#34;
        # you can add extra information after the name (HTML format is supported), such as icons
        post = &#34;&#34;
        name = &#34;Archives&#34;
        url = &#34;/archives/&#34;
        # title will be shown when you hover on this menu link
        title = &#34;&#34;
        weight = 1
        # FixIt 0.2.14 | NEW add user-defined content to menu items
        [menu.main.params]
            # add css class to a specific menu item
            class = &#34;&#34;
            # whether set as a draft menu item whose function is similar to a draft post/page
            draft = false
            # FixIt 0.2.16 | NEW add fontawesome icon to a specific menu item
            icon = &#34;fa-solid fa-archive&#34;
            # FixIt 0.2.16 | NEW set menu item type, optional values: [&#34;mobile&#34;, &#34;desktop&#34;]
        type = &#34;&#34;
```
具体用法详见FixIt文档。

## 3. 添加静态页面
做法类似添加一个新帖子。直接将markdowm文件加入`content`文件夹即可：
```shell
hugo new content mian.md
```
如果该页面无法通过菜单直接找到，可以在markdown最开始的配置区域加上url，例如：
```markdown
&#43;&#43;&#43;
title = &#39;RoboMaster Meta战队&#39;
subtitle = &#39;2024电控教学主页&#39;
date = 2024-05-14T14:17:45-05:00
draft = false
url = &#39;/meta-teaching/main&#39;
&#43;&#43;&#43;
```
该静态页面就会显示在网站/meta-teaching/main页面。

## 4. 添加图片和资源
将所有的图片和资源放入`assets`文件夹。资源和文件将以该文件夹为根目录进行寻址。

## 5. 更多其他功能
更多其他功能请查阅FixIt文档。本文档仅介绍基础维护方法。

---
{.awesome-hr}
&lt;!--more--&gt;


---

> Author: Feiyang Wu  
> URL: https://Raventhatfly.github.io/posts/b7b4b1f/  

