# Lecture2

# C / C&#43;&#43; 编译原理

### 需要提前掌握的基础知识
* 比特和字节的关系，8bit = 1B
* 十六进制数的表达方式以及十六进制数和二进制数的转换
    * 例子：0x2f = 00101111

### 预习内容

### 1. 中央处理器（CPU）架构
##### 内存

内存是计算机的存储空间。

对于很多没有接触过计算机的人来说，内存=硬盘。其实这种理解是错误的。内存掉电会丢失内容，而
硬盘在掉电之后信息不会丢失。但是内存的访问速度比硬盘快，因此实际上在电脑启动时操作系统的代码
会从硬盘上搬迁到内存里。平时打开的文件也是如此。

内存地址的基本单位是字节。一个字节=8比特。对于32位计算机，其寻址能力为32位，意思是有2^32个
地址。大部分计算机是字节寻址，即一个地址对应一个字节的数据（ECE120涉及的LC3是16位机，但是
一个地址对应2B两个字节的数据）。

##### 其他
交给ECE120去学吧。

### 2. 编译流程
#### 常见概念
头文件`.h`包含了函数声明、宏定义等。在C&#43;&#43;当中还会存放类。`.c`文件中存放源代码。

#### 具体流程
##### (a)预处理阶段
预处理阶段，其实用朴素的话语来讲就是对宏（Macro）进行文本替换或展开。例如：
```C
#include &lt;stdio.h&gt;
```
在预处理完成之后，这段代码会被直接替换位`stdio.h`头文件包含的内容。
再例如：
```C
#define GPIO_DEVICE_ID 1
```
代码里所有出现的`GPIO_DEVICE_ID`将被替换为1。

{{&lt; admonition type=tip title=&#34;注意&#34; open=true &gt;}}
当使用`#include`之后，就可以使用头文件里的宏。除非是编译器定义的宏，否则可能会无法被找到。
{{&lt; /admonition &gt;}}

##### (b)编译阶段
将所有预处理之后的C/C&#43;&#43;代码翻译成汇编语言(汇编文件一般以`.s`,`.asm`为后缀，将会在ECE120
后期课程涉及)。

##### (c)汇编阶段

将汇编语言翻译成计算机可执行的二进制文件(生成若干`.o`，`.obj`文件)。每个独立的二进制文件
由于不知道相互之间的关系，现在还无法独立运行。

##### (d)链接阶段
这个阶段是最令人头大阶段。链接过程将多个目标文以及所需的库文件(.so等)链接成最终的可执行文件
(executable file)。该过程较为复杂，希望详细了解可以阅读[知乎文章](https://zhuanlan.zhihu.com/p/88255667)。
通俗易懂的讲法，就是把每个C/C&#43;&#43;文件生成的二进制文件，或者一些厂商（例如Windows）提供的
二进制文件（即静态与动态链接库，常见后缀`.so`，`.lib`，`.a`）组装在一起。

**静态链接库**：当要使用时，连接器(linker)会找出程序所需的函数，然后将它们拷贝到执行文件，
由于这种拷贝是完整的，所以一旦连接成功，静态程序库也就不再需要了。

**动态库链接库**：某个程序在运行中要调用某个动态链接库函数的时候，操作系统首先会查看所有正在运行的程序，看在内存里是否已有此库函数的拷贝了。
如果有，则让其共享那一个拷贝；只有没有才链接载入

**常见错误**：

如果使用一个函数但没有定义它（大部分时候有可能是函数单纯打错了）：
{{&lt; admonition failure &gt;}}
link_example.c:(.text&#43;0xe): undefined reference to `foo&#39;
collect2.exe: error: ld returned 1 exit status
{{&lt; /admonition &gt;}}

如果链接器发现了两个不同的二进制文件中有相同的全局变量或函数，连接器会这么报错：
{{&lt; admonition failure &gt;}}
/tmp/ccIa32rv.o:(.bss&#43;0x0): multiple definition of `head&#39;/tmp/ccAvumDO.o:(.bss&#43;0x0): first defined here
/tmp/ccuVImET.o:(.bss&#43;0x0): multiple definition of `head&#39;
/tmp/ccAvumDO.o:(.bss&#43;0x0): first defined here
collect2: error: ld returned 1 exit status
{{&lt; /admonition &gt;}}


### 3. 编译脚本

脚本(sript)就是把一些命令放在一个文件里，这样在执行的时候不需要一条条手动输入而是一次性
全部执行的一个文件。

编程语言也主要分为两种：编译语言与脚本语言。脚本语言的每一条代码逐条投喂至解释器，并理解
翻译成二进制代码供CPU执行。而编译语言将全部代码全部翻译为二进制代码之后才能供CPU执行。
最常见的脚本语言是Python。最典型的编译语言即为C和C&#43;&#43;。

#### Makefile
Makefile 是一个用于管理项目构建的文件，通常用于编译和链接程序，特别是在大型项目中。
它通过定义一系列规则和目标，自动化了编译和构建过程，从而避免了手动输入复杂的编译命令。
```Makefile
# 定义变量
CC = gcc
CFLAGS = -Wall -g

# 定义目标文件
TARGET = myprogram

# 定义依赖关系和规则
$(TARGET): main.o utils.o
    $(CC) $(CFLAGS) -o $(TARGET) main.o utils.o

main.o: main.c
    $(CC) $(CFLAGS) -c main.c

utils.o: utils.c
    $(CC) $(CFLAGS) -c utils.c

# 伪目标，用于清理构建文件
.PHONY: clean
clean:
    rm -f $(TARGET) *.o
```
找到项目的Makefile文件，打开终端输入：
```shell
make
```
`make`将根据Makefile生成`gcc`指令。例如上述代码的运行路径为中的文件有：
```shell
my_project/
├── Makefile
├── main.c
└── utils.c
```
$(CC)会被翻译成gcc，$(CFLAGS)会被翻译成-Wall -g。-o 我们在之前介绍过，是输出的意思。
所以如果输入`make myprogram`实际上相当于输入了以下的gcc指令：
```shell
gcc -Wall -g -c main.c # 将main.c编译为main.o
gcc -Wall -g -c utils.c
gcc -Wall -g -o myprogram main.o utils.o # 通过.o文件生成myprogram可执行文件
```
#### CMake

CMake 是一个跨台的构建系统，它用于管理项目的编译过程，生成特定于平台的构建文件（如 
Makefile、Visual Studio 项目文件等）。CMake 通过一种高级脚本语言来描述构建过程，
能够更好地处理复杂的构建需求，并且在不同平台之间保持一致性。在我们的项目中我们一般使用
Cmake来生成Makefile。

假设现在我们的项目文件夹为：
```shell
my_project/
├── CMakeLists.txt
├── main.cpp
└── utils.cpp
```
`CMakeLists.txt`：
```cmake
cmake_minimum_required(VERSION 3.10)

# 项目信息
project(MyProject)

# 设置 C&#43;&#43; 标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 添加可执行文件
add_executable(MyProject main.cpp utils.cpp)
```
 然后运行：
```shell
mkdir build
cd build
cmake ..  # .. 表示上一级目录，这里的意思是Cmakelists.txt在上一级目录
```
然后我们就能在build文件夹中找到Makefile了。此时我们就能运行：
```shell
make
```
我们就能得到想要的二进制可执行文件了。

### 课后作业
* 使用Makefile和Cmake成功编译文件。
* 继续观看黑马程序员教学视频。

---
{.awesome-hr}
&lt;!--more--&gt;


---

> Author: Feiyang Wu  
> URL: https://Raventhatfly.github.io/posts/bd7db78/  

