# Multiplex LIF


&lt;!--more--&gt;

### 1. 为什么要使用复用方案
金教授对脉冲神经网络的复用非常感兴趣。首先，在人类大脑中，神经信号的编码方式通常有多种，例如速率编码，延时编码等。
这些编码包含大量信息，甚至可以在时域上进行复用。但是对于SNN这一领域中，复用的方案确很少出现。这几天我冥思苦想了
非常多的方案，最终思考出了一种可能可以进行复用的方案。目前我只完成了前向传播，还没有推导反向传播的公式，至于这种
复用方案是否能成功以及其有效性，可能还有待研究。

### 2. 奇偶时间戳编码
在常规的SNN当中，通常我们对于每个单位时刻，采用伯努利分布产生脉冲（对于连续时间来说这一过程就是泊松分布）。这种
方式产生的编码就是速率编码。现在需要研究的问题是，我们需要采取某种方式，将两个信道的速率编码只通过单个LIF，然后
通过某种方式解码，重新变为两个信道。当然，我们很关心这两个信道之间的串扰，并且我们需要在反向传播中将这种干扰给修
正。那么其实从直观上来讲，奇偶时间戳编码是最容易理解的编码方式。对于信道一，我们取样偶数索引的脉冲；而对于信道二，
我们取样奇数索引的脉冲。将两个信道直接叠加在一起，通过LIF，然后再用将得到的一系列脉冲信号，再将其偶数索引的信号
加载到信道一上，将奇数索引的信号放到信道二上。当然，这中做法非常奇怪，我一开始也觉得这样不一定能做成。

![img.png](/figures/stbp/two_sikes.png)
{.custom-center}

后来我在Python中做了模拟。我将信道一的伯努利分布的概率设为0.1，信道二设置为0.9。我通过上述方式进行了编码和解码，
最后得到了如下的结果。

![lif-decode.png](/figures/stbp/lif-decode.png)
{.custom-center}

途中蓝色表示分离后的信道一，橙色表示分离后的信道二。虽然我目前还没有从数学上证明这种解码是成功的，但是从模拟结果来看，
高频信道和低频信道似乎被成功分离了！因此我开始 相信也许这种方法是有效的。

### 3. 基于NewBP和STBP算法的复用LIF
NewBP是实验室之前的以为硕士学长提出的一个架构。那么模仿newBP中的神经网络架构，我从github直接克隆了STBP的代码，并
将网络结构更改为和NewBP一样，也就是784个输入层，60个隐藏层，10个输出层。在MNIST数据集中我跑了三到四个epoch，取得
了96左右的训练和测试准确率。

接下来就是比较重要的信道分离操作了。我一开始用inplace的方法进行信道分离。这种方法类似这样：
```python
spike_odd = spike[:,1::2]
spike_even = spike[:,::2]
```
{{&lt; raw &gt;}}但是后来发现这种方法会导致pytorch求导错误。于是我就对我的方法进行了修正。由于tensor是\(
100 \times 60\)的(100是batchsize), 而奇偶信道复用之后就会缩减为\( 100 \times 30\)。因此我可以通过如下方式构造矩阵：
{{&lt; /raw &gt;}}
```python
self.mask_hidden_odd = torch.zeros((60,30), device=device, requires_grad=False)
self.mask_hidden_even = torch.zeros((60,30), device=device, requires_grad=False)
self.mask_hidden_odd[1::2,:] = torch.eye(30).clone()
self.mask_hidden_even[::2,:] = torch.eye(30).clone()

self.mask_out_odd = torch.zeros((10,5), device=device, requires_grad=False)
self.mask_out_even = torch.zeros((10,5), device=device, requires_grad=False)
self.mask_out_odd[1::2,:] = torch.eye(5).clone()
self.mask_out_even[::2,:] = torch.eye(5).clone()

```
{{&lt; raw &gt;}} 对于矩阵A(\(100\times60\))我想取出偶数列（从0开始索引）变成\(100\times30\)的矩阵，我只要乘上矩阵\(w\):{{&lt; /raw &gt;}}
{{&lt; raw &gt;}}
\[ w =

\begin{bmatrix}
1 &amp; 0 &amp; 0 &amp; \dots 0 \\
0 &amp; 0 &amp; 0 &amp; \dots 0 \\
0 &amp; 1 &amp; 0 &amp; \dots 0 \\
0 &amp; 0 &amp; 0 &amp; \dots 0 \\
0 &amp; 0 &amp; 1 &amp; \dots 0 \\
\vdots &amp; \vdots &amp; \vdots &amp; \ddots &amp; 0 \\
0 &amp; 0 &amp; 0 &amp; \dots 1 \\
0 &amp; 0 &amp; 0 &amp; \dots 0 \\
\end{bmatrix}


\]
{{&lt; /raw &gt;}}

{{&lt; raw &gt;}} 对于矩阵B(\(100\times30\))我变成\(100\times60\)的矩阵的偶数列，在奇数列补0，我只要乘上矩阵\(w\)的转置\(w^T\)即可。{{&lt; /raw &gt;}}
这个方法可以成功解决Pytorch对inplace操作不可反向传播的报错。

---

> Author: Feiyang Wu  
> URL: https://Raventhatfly.github.io/posts/08503b5/  

