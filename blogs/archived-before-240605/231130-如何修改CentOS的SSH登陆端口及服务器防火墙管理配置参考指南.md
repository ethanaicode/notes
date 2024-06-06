# 如何修改CentOS的SSH登陆端口及服务器防火墙管理配置参考指南

在购买了新的服务器，装上CentOS系统后，大部分服务器都默认使用22端口进行SSH登陆。

但使用默认是不安全的，容易被暴力破解，推荐修改下默认的22登陆端口。

## 如何修改CentOS的SSH登陆端口

1.

**首先使用原来的SSH端口远程登录**

登录后使用下面命令修改配置：

（如果不会使用vim，请先参考其它教程了解下）

```bash
# 修改SSH配置
vim /etc/ssh/sshd_config
```

2.

**修改配置**

将端口号修改为你自己的，记得保存退出。

![Ethan_2023-11-30_10-49-26](https://pic.shejibiji.com/i/2023/11/30/65681ef542621.jpg)

3.

**重启SSH服务**

使用下面命令重启SSH服务即可。

```bash
# 重启SSHD
systemctl restart sshd.service
```

*一般情况下，现在就可以使用新的端口进行SSH登陆了。*

4.

**确认端口放行**

如果是阿里云或者其它服务器，不是所有的端口都默认放开的。

这个时候还需要去安全组那边开放一下端口：

![Ethan_2023-11-30_13-42-11](https://pic.shejibiji.com/i/2023/11/30/656820bc6bdad.jpg)

**这样就完成了更换默认的22登陆端口。**

5.

**无法远程连接？**

我有两台服务器，一台直接这样操作成功了。

但另外一台这样操作后，却导致无法远程连接，下面是阿里云自动反馈的结果：

![Ethan_2023-11-30_11-23-56](https://pic.shejibiji.com/i/2023/11/30/656821a2a8619.jpg)

**一般情况下，应该都是系统防火墙拦截了。**

如果使用VNC或者其它方式登录后，执行关闭防火墙就能用新的端口登录，那么就可以尝试把新的端口添加到防火墙规则中（开启新的端口），来彻底解决这个问题。

我是这样解决好的。可以用下列教程作为参考：

## 服务器防火墙管理

**这里还是以CentOS 7为例：**

- 查看防火墙运行状态

```bash
firewall-cmd --state
```

- 关闭防火墙

```bash
systemctl stop firewalld.service
```

- 开启防火墙

```bash
systemctl start firewalld.service
```

- 列出防火墙开放的端口

```bash
firewall-cmd --list-port
```

- 开启指定端口（三条命令，都需要执行下）

```bash
# 开启指定端口（80端口改为自己的）
firewall-cmd --zone=public --add-port=80/tcp --permanent
# --permanent 表示永久生效，没有这参数，重启后配置会失效

# 重新载入配置
firewall-cmd --reload

# 重启防火墙
systemctl restart firewalld.service
```

- 移除指定端口

 ```bash
 firewall-cmd --zone=public --remove-port=80/tcp --permanent
 ```

![Ethan_2023-11-30_14-02-15](https://pic.shejibiji.com/i/2023/11/30/656825775ffed.jpg)

其它的系统可以参考下阿里云的这个教程：

[开启或关闭Linux实例中的系统防火墙](https://help.aliyun.com/zh/ecs/enable-or-disable-the-system-firewall-function-for-linux-instances)