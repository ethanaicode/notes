# 安装Wampserve搭建本地PHP学习环境，附EParseError错误的解决方法

之前本地的web环境一直都是使用的xampp套件，前面也有写过配置的教程：《[如何使用xampp在本地搭建虚拟服务器](https://www.shejibiji.com/archives/67)》

但是xampp有个很严重的问题，就是它默认安装的数据库MySQL版本太低了只有5.1还是多少，反正就是没法用。

我去网上搜了下升级的办法，比较麻烦，所以干脆，就直接重新换一个套件吧，刚好也可以对比看看。

目前主流的web本地套件就三个，xampp、wamp和phpstudy。

phpstudy之前的官网访问不了，我下载了安装包也没敢安装，怕官方不再支持了。不过今天打开看了下又可以访问了，地址改成了https://www.xp.cn，看了下介绍还是不错的，可以试一下。

我今天要安装的是wamp，原因无他，就是喜欢他们官网这个老头的形象：

![R_22-05-12-23-14-50_80](https://pic.shejibiji.com/i/2022/05/12/627d246fe8672.jpg)

他的官网对于套件所包含的内容也写的的很清楚：

```python
– Wampserver 3.2.6 64 bit x64 – Apache 2.4.51 – PHP 5.6.40/7.4.26/8.0.13/8.1.0 – MySQL 5.7.36|8.0.27 – MariaDB 10.5.13|10.6.5PhpMyAdmin 4.9.7 & 5.1.1 – Adminer 4.8.1 – PhpSysInfo 3.3.4 – En Option : PHP 7.0.33/7.1.33/7.2.34/7.3.30
```

MySQL和PHP都是支持多个版本可选安装的，非常方便！

那么开始安装吧！

## Wampserve安装教程

1.

**首先下载套件**

官方地址：https://www.wampserver.com/en/

打开后我们往下找到`DOWNLOADS`区域，按照自己的电脑选择版本，正常的都可以选择左边的64位系统：

![R_22-05-12-23-15-14_80](https://pic.shejibiji.com/i/2022/05/12/627d2487e24c8.jpg)

跳转下一页之后，我们选择直接下载：

![R_22-05-12-23-15-33_80](https://pic.shejibiji.com/i/2022/05/12/627d249e57245.jpg)

到达下载页面后，会自动开始下载，下载完成后就可以开始准备安装了。

2.

**安装套件**

我们双击下载的安装包，开始安装。

语言这块，默认`English`就好，因为也没有其它更好的选择：

![R_22-05-12-22-25-55_80](https://pic.shejibiji.com/i/2022/05/12/627d18f7b5724.jpg)

之后推荐默认选择即可：

![R_22-05-12-22-32-37_80](https://pic.shejibiji.com/i/2022/05/12/627d1a8bcd9f6.jpg)

中间会让选择浏览器和文本编辑器，可以点默认，也可以选择下其它的浏览器。

之后就会安装完成。

3.

**测试环境**

我们点击桌面上的Wamp图标，开始运行。

运行wamp后，在浏览器输入本地地址:http://127.0.0.1/，如果出现这个界面就表示安装完成了！

![R_22-05-13-11-24-33_80](https://pic.shejibiji.com/i/2022/05/13/627dcf84bc652.jpg)

没问题的就可以正常使用了。

控制面板是在右下角的任务栏上，我们可以在这里更改配置，重启服务等操作。

![R_22-05-13-11-40-38_80](https://pic.shejibiji.com/i/2022/05/13/627dd33fbe67d.jpg)

## 切换中文无法启动Wamp

在我尝试把Wamp语言改成中文后，悲剧发生了，Wamp无法启动了，提示：

![R_22-05-12-22-43-59_80](https://pic.shejibiji.com/i/2022/05/12/627d1d3839e94.jpg)

原文为：

```c++
the configuration file contains a syntax error on line 44:
[EParseError]Mismatched or misplaced quotes on parameter "PromptCaption"
```

去网上搜了下，似乎是官方提供的套件问题，已经有补丁了。

我想其实英文也能用，所以干脆就不装补丁了，能恢复使用就行。

思路也简单，就是把语言再切换回英文就好。

切换回英文需要修改Wamp的配置文件，我们打开Wamp的安装根目录，修改其中的两个文件：

`wampmanager.conf`和`wampmanager.ini`。

首先打开`wampmanager.conf`，把`chinese`改成`english`：

![R_22-05-12-22-55-16_80](https://pic.shejibiji.com/i/2022/05/12/627d1fdd0268b.jpg)

然后打开`wampmanager.ini`，删除**Variables**下的内容。

![R_22-05-12-23-11-43_80](https://pic.shejibiji.com/i/2022/05/12/627d23b99beff.jpg)

修改后，再尝试启动下Wamp，出现提示直接点确定，等待程序重新应用配置文件，就可以正常启动了。

