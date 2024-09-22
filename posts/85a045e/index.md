# Xshell使用


由于希望使用Linux服务器上的可视化工具，使用X11对Linux服务器的GUI进行转发。

参考博客：[https://www.cnblogs.com/tsfh/p/9022170.html](https://www.cnblogs.com/tsfh/p/9022170.html)

[https://www.cnblogs.com/xuyaowen/p/ssh-X11forward.html](https://www.cnblogs.com/xuyaowen/p/ssh-X11forward.html)

### Step 1.
服务器： sudo vim /etc/ssh/sshd_config 修改以下配置，如果在配置文件里面没有找到，就直接添加到文件末尾即可，最后保存退出:wq
```shell
X11Forwarding yes

X11DisplayOffset 10

X11UseLocalhost yes
```
服务器端修改完成后需要执行命令重启sshd服务
```shell
sudo systemctl restart sshd.service
```

### Step 2.
Windows上安装Putty和Xming。启动 XLaunch之后，记住display number，默认值为0。
之后打开putty，点击Connection-&gt;SHH-&gt;AUTH-&gt;X11，勾选enbale X11，`x display location`
填写`localhost:&lt;Display Number&gt;`，例如`localhost:0`。

### Step 3.
使用ssh通过putty连接服务器。尝试`xclock`，之后出现时钟图标。
&lt;!--more--&gt;


---

> Author: Feiyang Wu  
> URL: https://Raventhatfly.github.io/posts/85a045e/  

