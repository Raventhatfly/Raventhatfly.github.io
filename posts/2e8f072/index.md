# Lecture3


# STM32基础

### 1. STM32简介


#### 基础知识
**单片机**

单片机（Single-chip microcomputer），是把中央处理器、存储器、定时/计数器（timer/counter）、各种输入输出接口等都集成在一块集成电路芯片上的微型计算机。与应用在个人计算机中的通用微处理器相比，它更强调自供应（不用外接硬件）和节约成本，集成程度更高，但因为规格已经包含，所能实现的功能也较专一。它的最大优点是体积小，可放在仪表内部，但存储量小，输入输出接口简单。由于其发展非常迅速，旧的定义已不能满足，所以在很多应用场合被称为范围更广的微控制器（microcontroller）。

**STM32**

STM32，是由意法半导体基于 ARM Cortex-M 研制和生产的一系列32位单片机。
单片机，即微处理器，微处理器（Microprocessor）通常指称一种可编程特殊集
成电路，其所有组件小型化至一块或数块集成电路内。

**其他概念**
* 计算机架构：计算机使用的指令集
    * 计算机常见架构：ARM架构、x86架构

* 外设：电子计算机中位于机箱之外、能够通电并可以不依赖计算机进行正常的独立或半独立运行的硬件。
例如STM32中的TIM定时器、通用输入输出（GPIO）、中断控制器等。在现代电脑中可以包括键盘鼠标等。

* 寄存器：
  寄存器（Register）是中央处理器内用来暂存指令、数据和地址的存储器。寄存器的存贮容量有限，读写速度非常快。在计算机体系结构里，寄存器存储在已知时间点所作计算的中间结果，通过快速地访问数据来加速计算机程序的执行。
#### 常见单片机
* 51系列单片机
* STM32
* ESP32

#### STM32组成
* ARM Cortex CPU
* 外设

**STM32实质上是由ARM提供中央处理器，意法半导体在此基础上设计外设所组成的微处理器。**

### 2. STM32型号与分类
![STM32](/figures/stm32_type.png)
{.custom-center}

STM32系列专为要求高性能、低成本、低功耗的嵌入式应用设计的ARM Cortex®-M0，M0&#43;，M3, M4和M7内核  。按内核架构分为不同产品：
主流产品（STM32F0、STM32F1、STM32F3）、超低功耗产品（STM32L0、STM32L1、STM32L4、STM32L4&#43;）、高性能产品（STM32F2、STM32F4、STM32F7、STM32H7）等。

STM32最常见型号：STM32F1系列和STM32F4系列。
RoboMaster A型开发板和C型开发板都属于STM32F4系列。C型开发板具体型号为STM32F407。


### 3. 常用开发工具

#### 开发软件
* Keil5
* STM32CubeMX
* Clion
* ARM GNU Toolchain (arm-none-eabi编译器)
* Eclipse

#### 开发软件库
* CMSIS
* STM32标准库
* STM32标准HAL库
* 实时操作系统(FreeRTOS, uCOS, ChibiOS)

#### 烧录器
* ST-Link
* JTAG

#### debug、烧录软件
* OpenOCD

### 4. STM32开发方法简述
对于裸机编程（不适用实时操作系统进行线程调度），主要使用三种方法编写代码：直接操作寄存器、
标准库函数编程（较老）、标准HAL（Hardware Abstraction Layer，硬件抽象层）库。如果
不采取裸机编程，那么将会使用到实时操作系统(RTOS)。

RTOS具有Linux等操作系统不具有的任务实时性响应机制，具体体现在线程调度机制等方面。

#### (a) Keil &#43; 标准库

#### (b) Keil &#43; STM32CubeMX &#43; 标准Hal库

#### (c) Keil &#43; STM32CubeMX &#43; 标准Hal库 &#43; FreeRTOS

#### (d) Clion &#43; ChibiOS &#43; ChibiOS HAL

### 5. Metaz战队工具链

工具链配置教程由Meta战队前项管刘子恺学长倾力打造。
因为这篇Wiki年代久远，其中有些链接内容可能已经发生错误或者失效。
在之前的文章中，我们已经安装过MinGW, git, cmake等工具，在根据教程安装工具链时，不要重复安装。

Meta战队工具链配置教程点击[此处](https://github.com/Meta-Team/Meta-Embedded/wiki/%E5%B7%A5%E5%85%B7%E9%93%BE-%E6%A6%82%E5%BF%B5%E4%BB%8B%E7%BB%8D)。

### 6. 课后作业

* 继续观看黑马程序员
* 按照第五部分教程链接完成工具链配置。
* （可选）自行学习STM32有关知识

###

---
{.awesome-hr}

&lt;!--more--&gt;


---

> Author: Feiyang Wu  
> URL: https://Raventhatfly.github.io/posts/2e8f072/  

