# pip error: ProtocolError('Connection aborted.', FileNotFoundError(2, 'No such file or directory'))

![Ethan_2024-06-21_14-03-29](https://pic.shejibiji.com/i/2024/06/21/6675187411773.jpg)

> 本文记录了我解决问题的尝试及思路，所以会比较啰嗦，如果只是为了寻找解决答案的，可以直接跳到最后一段查看。
>
> This document records my attempts and thought process in solving the problem, so it may be somewhat verbose. If you are just looking for the solution, you can skip directly to the last section.

## 出现问题

昨天还能愉快的使用`pip`安装依赖，今天就突然都不行了，全部都提示连接错误。尝试更新`pip`依然如此。

![Ethan_2024-06-21_13-55-46](https://pic.shejibiji.com/i/2024/06/21/6675165550ba0.jpg)

```bash
WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ProtocolError('Connection aborted.', FileNotFoundError(2, 'No such file or directory'))': /simple/beautifulsoup4/
```

## 找出问题

网上搜了一圈，挺多人提出这个问题的，但都没有很好的解决方法。

以为是国内特殊网路环境原因导致的，于是换回百度搜索，尝试配置使用了国内镜像源，依然有问题。

意外的是，在尝试的过程中，一条使用了阿里家的镜像命令，竟然可以正常下载：

```bash
install requests -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
```

于是对比网上那些使用了清华，豆瓣镜像源的命令，发现这条命令多了个参数`--trusted-host`

**这是不是意味着只需要把其它镜像源加入到信任的host就可以了？**

添加配置可以通过`config set`命令，于是我尝试把**pypi**的镜像源加入信任：

```bash
pip config set global.trusted-host "pypi.org files.pythonhosted.org pypi.python.org"
```

再次尝试安装，失败……

难道是源头的问题，换成豆瓣试试：

```bash
pip install requests -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
```

失败……

这也就意味着不仅仅是``--trusted-host``这个配置的问题了。

于是我尝试使用**阿里源**但不加这个配置：

```bash
pip install selenium -i http://mirrors.aliyun.com/pypi/simple/  
```

依然报错了，但不是提示网络错误了，而是新的错误：

![Ethan_2024-06-21_14-35-01](https://pic.shejibiji.com/i/2024/06/21/66751f2f853f8.jpg)

注意最后一行，显示错误：文件或者目录没找到。

这个文件路径我熟悉啊，昨天用`wireshark`调试时，曾经用过这个文件，通过设置环境变量`SSLKEYLOGFILE`，来获取 SSL 证书的密钥，以监控 SSL 的内容，后面`wireshark`总是特别卡我就把这个文件及目录删了。

原来是这里出了问题呀，难怪今天突然不行了，最后发现，还真是自己的锅。

## 解决问题 Solving

如果你也定义了`SSLKEYLOGFILE`环境变量，请确保该环境变量的目录及文件存在，你可以通过`env`命令查看是否有该环境变量。

如果你不需要`SSLKEYLOGFILE`这个环境变量，只需要通过下列命令就可以去掉：

```bash
unset SSLKEYLOGFILE
```

你可以删掉，或者正确配置环境变量`SSLKEYLOGFILE`，之后就可以正常使用`pip` 下载依赖包了。

If you have also defined the `SSLKEYLOGFILE` environment variable, please ensure that the directory and file specified by this environment variable exist. You can check if this environment variable is set by using the `env` command.

If you do not need the `SSLKEYLOGFILE` environment variable, you can remove it with the following command:

```bash
unset SSLKEYLOGFILE
```

after which you should be able to use `pip` to download dependencies without any issues.