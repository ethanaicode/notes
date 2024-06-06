# 威联通NAS下载神器qbittorrent配置及使用教程

![R_22-10-10-09-24-50_80](https://pic.shejibiji.com/i/2022/10/10/6343746917866.jpg)

威联通NAS自带的Download Station其实很好用了，大多数时候无需再使用其他下载工具。

不过我最近就遇到Download Station无法下载的情况，添加的任务半天都没反应：

![R_22-10-07-19-56-08_80](https://pic.shejibiji.com/i/2022/10/10/63437279c3c07.jpg)

我尝试卸载再重新安装，就可以正常下载了。但是过一段时间再添加任务又是这样，就很费解。

所以最终决定，还是尝试下qbittorrent这款神器。

## 下载qbittorrent套件

直接在商店搜索是无法找到qbittorrent应用的，需要添加第三方的软件源头，具体可以看我之前写的这篇文章：[威联通NAS如何添加第三方软件源头](https://www.shejibiji.com/archives/8267)

在第三方软件源头商店就可以找到qbittorrent：

![R_22-10-10-09-23-07_80](https://pic.shejibiji.com/i/2022/10/10/6343740de19be.jpg)

点击安装就可以自动下载并安装了，安装后就可以在首页看到这款应用。

## 配置qbittorrent

1.

**打开qbittorrent并登录**

> 说起来我之前懒得折腾这款应用，就是因为它配置还挺繁琐的，并不是开箱即用，这可能就是国外程序员不喜欢加班导致的吧，用户体验做的有点差。

如果你直接点击应用打开，会发现**Unauthorized**，无法打开。

解决方法也很简单，只要在网址后面再加上一个`/`即可。

![R_22-10-10-09-30-27_80](https://pic.shejibiji.com/i/2022/10/10/634375bc9da33.jpg)

打开后需要输入账号和密码：

默认用户名为 **admin**，密码 **adminadmin**

输入后点击登录即可。

2.

**修改语言**

软件打开默认是英文，可以修改成中文。

我们在顶部菜单，找到**TOOLS**（工具），选择下面的**Options**（选项），即可打开设置菜单：

![R_22-10-10-09-34-29_80](https://pic.shejibiji.com/i/2022/10/10/634376aa37b98.jpg)

在打开的菜单中选择**Web UI**，在第一个选项中即可更改，可以直接选择**简体中文**。

![R_22-10-10-09-36-49_80](https://pic.shejibiji.com/i/2022/10/10/6343773dcc68b.jpg)

3.

**设置下载目录**

默认的下载目录是应用安装目录，显然是不合适的。我们可以自定义。

首先我们先在文件管理中新建一个共享文件夹**QtDs**：

![R_22-10-10-09-43-01_80](https://pic.shejibiji.com/i/2022/10/10/634378ad44091.jpg)

然后就是要获取这个文件夹路径。

由于是NAS系统，这个路径获取需要费点事，但其实可以大概推测出来，比如我的：

`/share/CACHEDEV4_DATA/DownStation/QtDS`

**/share/CACHEDEV4_DATA/：**这一段在威联通NAS中几乎一样的，只是`CACHEDEV4`后面这个数字，需要根据硬盘位置，来确定，我的因为是第四块，所以是`V4`。

再往下就是层级目录了。

> 如果是其他系统，或者不知道自己的硬盘是第几块，可以使用Winscp来获取：
>
> ![R_22-10-10-09-48-19_80](https://pic.shejibiji.com/i/2022/10/10/634379f55f669.jpg)
>
> 至于Winscp如何使用，可以自行搜索解决。如果有需要我也可以再单独写一篇教程。

获取到下载文件夹目录后，我们填入到`默认保存路径`。

![R_22-10-10-09-57-29_80](https://pic.shejibiji.com/i/2022/10/10/63437c0fb85ff.jpg)

现在就可以正式开始使用了！

我们只需要在菜单左上角，点击添加链接或者文件，即可开始下载：

![R_22-10-10-09-59-59_80](https://pic.shejibiji.com/i/2022/10/10/63437ca755395.jpg)

4.

**更多设置**

仅用于提供参考。

**→ BitTorrent**

![R_22-10-10-10-02-42_80](https://pic.shejibiji.com/i/2022/10/10/63437d49da552.jpg)

Trackerslist列表可以在这个仓库获取：https://github.com/ngosang/trackerslist

如果无法访问仓库，可以使用下面这20个精选trackers：

```html
udp://tracker.opentrackr.org:1337/announce
udp://9.rarbg.com:2810/announce
udp://tracker.openbittorrent.com:6969/announce
http://tracker.openbittorrent.com:80/announce
udp://opentracker.i2p.rocks:6969/announce
https://opentracker.i2p.rocks:443/announce
udp://open.stealth.si:80/announce
udp://tracker.torrent.eu.org:451/announce
udp://tracker2.dler.org:80/announce
udp://tracker.tiny-vps.com:6969/announce
udp://tracker.moeking.me:6969/announce
udp://tracker.dler.org:6969/announce
udp://public.tracker.vraphim.com:6969/announce
udp://p4p.arenabg.com:1337/announce
udp://open.demonii.com:1337/announce
udp://movies.zsw.ca:6969/announce
udp://ipv4.tracker.harry.lu:80/announce
udp://fe.dealclub.de:6969/announce
udp://explodie.org:6969/announce
udp://exodus.desync.com:6969/announce
```

更多设置，请自行摸索。