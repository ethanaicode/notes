# 解决redis错误：ERR Client sent AUTH, but no password is set

![Ethan_2023-04-12_14-44-48](https://pic.shejibiji.com/i/2023/04/12/6436536985a11.jpg)

此错误表示您的 redis 实例中没有设置密码。 

如果您从您的代码中发送身份验证信息（auth方法），就可能会收到此消息。

推荐还是设置下redis的用户密码来解决这个问题，有两种方法可以解决。

## 第一种，修改redis配置文件

首先打开redis的配置文件

``` bash
sudo nano /etc/redis/redis.conf
```

取消掉注释的密码行，并设置新密码

```bash
# requirepass yourpassword
```

然后重启redis即可。

## 第二种，命令行终端修改

首先打开terminal终端并连接redis-cli

```bash
redis-cli
```

设置密码

```bahs
CONFIG SET requirepass "yourpassword"
```

这样就设置成功了，你可以测试下

```bash
AUTH yourpassword 
```

