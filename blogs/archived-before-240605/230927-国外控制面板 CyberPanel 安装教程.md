# 国外控制面板 CyberPanel 安装教程

> 本笔记仅做记录，并不推荐
>
> 使用体验不好，已重新装机……（大部分管理功能都不能用，Root文件管理器都要收费，无语）

经济下行，个人钱包缩水，于是之前的好多服务器也不再续费了。

于是准备把一些服务应用迁移到一台服务器上去。

以前习惯安装**宝塔面板**来管理，操作熟悉且方便，但宝塔面板存在不确定性，而且会上传日志等，让人感觉不安。

于是这次准备换一个面板试试，最终决定使用国外的这款CyberPanel面板，看界面还是很清爽的：

![cyberpanel-features-hero-1920x1098](https://pic.shejibiji.com/i/2023/09/28/6514f59467fde.png)

这款面板看说明，唯一不好的就是网络服务器使用的是LiteSpeed Server，了解了下，和Nginx、Apache这些也差不多，于是选择忽略这一点，直接找一台空的服务器跑起来看看再说。

废话不多说，先安装跑起来再说：

## 安装CyberPanel

官方安装文档：https://community.cyberpanel.net/docs?topic=82

### CyberPanel 安装要求：

- 干净的服务器，系统为Ubuntu 20.04, Ubuntu 22.04, CloudLinux 7, CloudLinux 8, AlmaLinux 8

- 1G内存RAM或者更高

- 10G的磁盘空间

要注意：CyberPanel现在已经不支持**Centos**等其它系统，所以需要按照官方的需求来。

CyberPanel Ent是收费版，附带LiteSpeed Web Server Enterprise，并且对 1 个域免费。

免费用户安装CyberPanel就可以了，CyberPanel支持无限域。

### 安装步骤

1.

首先连接服务器，注意要是一台干净的服务器，然后输入下面的安装命令：

```bash
sh <(curl https://cyberpanel.net/install.sh || wget -O - https://cyberpanel.net/install.sh)
```

如果没有root权限，可以用这条命令：

```bash
sudo su - -c "sh <(curl https://cyberpanel.net/install.sh || wget -O - https://cyberpanel.net/install.sh)"
```

![Ethan_01](https://pic.shejibiji.com/i/2023/09/28/6514f56b5551f.jpg)

2.

**选择你想要的服务**

输入命令后，会让你选择，包括OpenLiteSpeed版本，service服务啥的，可以按照我下面的选项进行选择，或者一路回车，全部默认。

```bash
Initialized...

                CyberPanel Installer v2.3.4

1. Install CyberPanel.

2. Exit.


  Please enter the number[1-2]: 1

                CyberPanel Installer v2.3.4

RAM check : 147/1979MB (7.43%)

Disk check : 4/39GB (11%) (Minimal 10GB free space)

1. Install CyberPanel with OpenLiteSpeed.

2. Install Cyberpanel with LiteSpeed Enterprise.

3. Exit.


  Please enter the number[1-3]: 1


Install Full service for CyberPanel? This will include PowerDNS, Postfix and Pure-FTPd.

Full installation [Y/n]: Y

Full installation selected...

Do you want to setup Remote MySQL? (This will skip installation of local MySQL)

(Default = No) Remote MySQL [y/N]:  

Local MySQL selected...

Press Enter key to continue with latest version or Enter specific version such as: 1.9.4 , 2.0.1 , 2.0.2 ...etc

Branch name set to v2.3.4

Please choose to use default admin password 1234567, randomly generate one (recommended) or specify the admin password?
Choose [d]fault, [r]andom or [s]et password: [d/r/s] r

Admin password will be provided once installation is completed...


Do you wish to install Memcached process and its PHP extension?
Please select [Y/n]: n

Do you wish to install Redis process and its PHP extension?
Please select [Y/n]: Y

Install Redis process and its PHP extension set to Yes...


Would you like to set up a WatchDog (beta) for Web service and Database service ?
The watchdog script will be automatically started up after installation and server reboot
If you want to kill the watchdog , run watchdog kill
Please type Yes or no (with capital Y, default Yes): 


Install Watchdog set to Yes...
```

3.

**等待安装完成**

大概会花费10到15分钟，到达这个页面就表示成功了：

![Ethan_02](https://pic.shejibiji.com/i/2023/09/28/65150dde2656b.jpg)

输入图中的 Visit 后面的那个网址，也就是 <你的IP>:8090

然后输入面板账号和密码就可以登录了。

打开后界面就是这个样子：

![Ethan_05](https://pic.shejibiji.com/i/2023/09/28/65150ea795ff9.jpg)



创建站点后，就可以看到站点的管理，下面几乎都是全部的站点管理功能了，可以大概看下。

（真心有点少……）

![image-20230928133534049](https://pic.shejibiji.com/i/2023/09/28/651510a82926f.png)
