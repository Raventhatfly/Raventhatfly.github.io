# A Comparison of Imitation Learning Algorithms for Bimanual Manipulation论文精读

# Conecpts

### Behavior Cloning

{{&lt; raw &gt;}}
\begin{align*}
\mathbf{\hat{\theta}} = \argmax_{\theta} \mathbb{E}_{(\mathbf{s},\mathbf{a})\sim \mathbf{\tau_E}}[\log(\pi_{\theta}(\mathbf{a|s}))]
\end{align*}
{{&lt; /raw &gt;}}

The key idea of behavioural cloning is to maximize such policy $\pi_{\theta}(\mathbf{a}|\mathbf{s})$ where $\mathbf{s}$ and $\mathbf{a}$ is
the expert trajectory. 
### Action Chunking Transformer


### Implicit Behavior Cloning

{{&lt; raw &gt;}}
\begin{align*}
\mathbf{\hat{a}} = \argmin_{\mathbf{a}} E_{\theta}(\mathbf{s,a})
\end{align*}
{{&lt; /raw &gt;}}

## Methodology

&lt;!--more--&gt;


---

> Author:   
> URL: https://Raventhatfly.github.io/posts/814ef7b/  

