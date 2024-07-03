# Spatial Temporal Backpropagation


&lt;!--more--&gt;

## 1. SNN

深度神经网络在近年来取得了非常好的效果。和现存的深度神经网络相比，脉冲神经网络（SNN）有两个主要特点：
**(1)** 脉冲编码方式本质上同时拥有空间域和时间域的信息，而深度神经网络通常缺乏这种动态的时域信息。
**(2)** SNN的事件驱动模式让它对硬件更友好。但总体来说由于SNN的不可导的特性使反向传播变得较为困难。

## 2. Leaky Integrate &amp; Fire


{{&lt; raw &gt;}}
膜电位更新公式：
\[\tau \frac{du}{dt} = -u &#43; I, \ u &lt; V_{th}\]
脉冲激发：
\[u=u_{reset}, \ u \geq V_{th}\]
{{&lt; /raw &gt;}}

LIF模型：

![LIF Model](/figures/stbp/lif.png)
{.custom-center}

写出其可遍历表达式：
{{&lt; raw &gt;}}

\[u^{t&#43;1} = (1-\frac{dt}{\tau}) u^t &#43; \frac{dt}{\tau}I\]

{{&lt; /raw &gt;}}
{{&lt; raw &gt;}}我们将\((1-\frac{dt}{\tau})\)用衰减系数\(k_{\tau 1}\)表示，并且在神经网络中
\(I=\sum_j W_j o(j)\)。其中系数\(j\)代表前突触脉冲的索引值，\(o(j)\)代表后突触脉冲的二元数值（0和1）。系数
\(\frac{dt}{\tau}\)可以被突触矩阵\(W\)吸收。因此化简之后我们可以得到：{{&lt; /raw &gt;}}

{{&lt; raw &gt;}}
\[u^t = k_{\tau 1}u^{t&#43;1} &#43; \sum_j W_j o(j)\]

{{&lt; /raw &gt;}}

[//]: # ({{&lt; raw &gt;}}行内公式：\&amp;#40;\mathbf{E}=\sum_{i} \mathbf{E}_{i}=\mathbf{E}_{1}&#43;\mathbf{E}_{2}&#43;\mathbf{E}_{3}&#43;\cdots\&amp;#41;{{&lt; /raw &gt;}})

[//]: # ()
[//]: # ({{&lt; raw &gt;}})

[//]: # (公式块：)

[//]: # (\[ a=b&#43;c \\ d&#43;e=f \])

[//]: # ({{&lt; /raw &gt;}})



---

> Author: Feiyang Wu  
> URL: https://Raventhatfly.github.io/posts/9858afc/  

