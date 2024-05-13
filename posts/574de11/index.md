# Lecture1

## META 战队电控培训【第一讲】讲义
### 1. 预习内容
C 语言：B站黑马程序员（不建议下载使用Visual Studio，我们将不会用到它。如果教程用到了Clion，可以先开始下载。这次不做要求。推荐使用 Vscode,我们前期将使用gcc编译器进行编译C语言代码。Vscode安装参见：https://code.visualstudio.com/）

第一讲大家请自行学习P1~P24有关章节的知识。

黑马程序员课程链接：https://www.bilibili.com/video/BV1Xa4y1k7LU?p=14&amp;vd_source=b710c0374cb950d2cc5713ef9df39177
### 2. Linux基本操作

##### (a) 终端
终端（Terminal）是一台电脑或者计算机系统，用来让用户输入数据，及显示其计算结果的机器，简而言之就是人类用户与计算机交互的设备。

Windows 终端（Powershell）: 按下Win徽标&#43;R，输入powershell。
Mac: 自行上网查阅如何打开终端。

##### (b) Linux命令基本用法
熟悉并掌握Linux常用指令的用法。
Linux指令语法结构：
`[tyang3@localhost Desktop]$ command [-options] [arguments]`

command 命令：表示命令的名称，如`cd` `ls` `mkdir`等，实质是一个可执行的二进制程序

options 选项：定义命令的执行特性，中刮号[]并不存在于实际的指令中，而加入选项设定时，通常选项前会带 - 号或--号，有两种长短选项

短选项：用-引导，后面跟单个字符，如 -a、-l、-h等

多个短选项可以组合使用，效果和几个短选项一样，如-a –l -h===-alh

长选项：用--引导，后面跟完整的单词，如—help

arguments 参数：表示命令的作用对象，可以有多个参数，通常情况可以是文件名、目录、或用户名。

来源：https://zhuanlan.zhihu.com/p/33331219

### 3. 环境变量和MinGW编译器安装
（Mac和Linux用户可忽略此步，因为Mac和Linux自带gcc编译器）

##### (a)环境变量
环境变量（environment variables）一般是指在操作系统中用来指定操作系统运行环境的一些参数，如：临时文件夹位置和系统文件夹位置等。

如果在终端输入一个命令（command），上面我们所说command实际上是一个二进制的可执行文件。那终端怎么知道这个二进制文件该去如何找到呢？

比如，现在打开windows终端，输入gcc, 按下回车，只会出现报错信息。但是当我将gcc.exe所在的文件夹加入环境变量之后，输入gcc之后终端就能运行gcc这个二进制可执行文件命令。

##### (b)MinGW编译器安装
接下来是windows MinGW编译器安装方法：
下载：https://sourceforge.net/projects/mingw/files/latest/download
安装完成之后，找到安装位置，我们发现里面有一个bin文件夹：

![图片](/figures/bin.png)

来源：https://baike.baidu.com/item/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F/1730949

在windows上搜索环境变量，打开后，点击环境变量：

![环境变量](/figures/环境变量.png)

点击环境变量中的Path:

![path](/figures/path.png)

点击新建，把刚才MinGW那个带bin的路径给输入进来：

![bin](/figures/bin2.png)

###### 注意：退出的时候两个窗口都要点击确定！不要直接把窗口叉掉！

bin是binary的缩写，也就是二进制文件。bin文件夹中包含我们将用到的大部分可执行二进制文件，包括gcc。现在这些可执行文件都能被终端找到了。

![bin](/figures/bin3.png)

Win&#43;R 输入powershell打开终端，输入gcc得到一下结果：

![bin](/figures/gcc-out.png)

证明结果正确（fatal error的原因只是因为没有待编译的c文件输入而已）。

##### (c) gcc编译C语言源文件
要编译单个.c文件，我们可以采取如下方法。
首先，找到.c文件的所在位置，使用终端的cd指令（不知道什么叫cd命令的去网上搜）。假设我想编译`prime.c`，那么Windows用户将输入：
`gcc prime.c -o prime.exe`
Mac\Linux用户请输入：
`gcc prime.c -o prime`
prime.c是告诉gcc我想编译哪个文件，-o指的是输出文件名。
![bin](/figures/teach1.png)

之后文件夹中会多出一个叫prime.exe的二进制可执行文件。
Windows运行该可执行文件只需输入：
`.\prime.exe`
Mac\Linux请输入：
`.\prime`
可执行文件即可被执行完成。由于prime.c的功能是输出1~100中所有的质数，被打印的质数将会在终端中显示。

![bin](/figures/prime.png)

### 4.  UIUC VPN安装
由于我们将用github管理仓库，而国内连接github并不稳定，请大家尽快安装UIUC　VPN。

### 5. C语言基础语法
自行查阅预习内容。应掌握的内容为：P1-P24
应掌握的概念：注释、常量、关键字、变量、字符类型、标识符、数据类型、if语句

&lt;!--more--&gt;


---

> Author:   
> URL: http://localhost:1313/posts/574de11/  

