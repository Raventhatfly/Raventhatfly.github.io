# Hugo Setup

 # 本网站基于HUGO和github.io的建立教程

2024年5月的某一天，我和倪驰明讨论为我们在2024年下半年建立网站方便教学的有关事宜。
一开始我本来想自己手写html，但是倪驰明说，为什么不用hugo呢？

Hugo 是一个流行的静态网站生成器（Static Site Generator，SSG），它允许用户从简单的文本文件（如 Markdown 文件）
生成完整的静态网站，因此我们可以通过编写markdown快速部署网页而无需大量编写html。

从2024年5月12日开始，我致力于使用Hugo开发这个网站。由于我计划将这个网站部署到github.io，因此
我将同时通过这个架构来开发自己的个人主页。

## 1. 下载安装Hugo
首先进入官网，找到[安装](https://gohugo.io/installation/windows/)页面。根据官网的指示进行安装。
我的开发平台是Windows，其包管理工具没有像Linux和MacOS那么方便。那么我们可以直接找到[Prebuilt 
Binaries](https://github.com/gohugoio/hugo/releases/tag/v0.126.0)，由于我的电脑是AMD芯片，因此我选择hugo_extended_0.125.7_windows-amd64的版本进行
下载，解压，并安装。安装完成之后，将hugo所在的文件夹添加到Path环境变量。终端输入`hugo version`
，成功打印版本号，证明安装成功。

## 2. 选择心仪的Hugo主题
我们可以到[Hugo主题页面](https://themes.gohugo.io/)选择合适的主题。我最终挑选FixIt作为我的网站主题。
选择到合适的主题后即可根据Hugo官方教程或[FixIt官方教程](https://fixit.lruihao.cn/documentation/getting-started/quick-start/)进行安装。

```shell
hugo new site mySite
cd mySite
git init
git submodule add https://github.com/hugo-fixit/FixIt.git themes/FixIt
```
完成之后运行Hugo Server即可在localhost:1313测试网站。

## 3. Github 网站发布

参考了[博客文章](https://simumis.com/posts/deploy-to-github/#5%E5%8F%91%E5%B8%83%E7%BD%91%E7%AB%99)。

&lt;!--more--&gt;


---

> Author: Feiyang Wu  
> URL: https://Raventhatfly.github.io/posts/c9bea25/  

