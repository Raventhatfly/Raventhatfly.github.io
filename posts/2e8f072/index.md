# Lecture3


# STM32基础

### 1. STM32简介

STM32，是由意法半导体基于 ARM Cortex-M 研制和生产的一系列32位单片机。
单片机，即微处理器，微处理器（Microprocessor）通常指称一种可编程特殊集
成电路，其所有组件小型化至一块或数块集成电路内。

#### 基础知识

* 计算机架构：计算机使用的指令集
    * 计算机常见架构：ARM架构、x86架构

* 外设：电子计算机中位于机箱之外、能够通电并可以不依赖计算机进行正常的独立或半独立运行的硬件。
例如STM32中的TIM定时器、通用输入输出（GPIO）、中断控制器等。在现代电脑中可以包括键盘鼠标等。

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


### 3. STM32 外设

### 4. STM32 编程
对于裸机编程（不适用实时操作系统进行线程调度），主要使用三种方法编写代码：直接操作寄存器、
标准库函数编程（较老）、标准HAL（Hardware Abstraction Layer，硬件抽象层）库。

### 5. STM32 

### 6. 课后作业

---
{.awesome-hr}

&lt;!--more--&gt;


---

> Author: Feiyang Wu  
> URL: https://Raventhatfly.github.io/posts/2e8f072/  

