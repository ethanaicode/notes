# 如何解决 Adobe 2023 Mac by RID 安装包Damaged损坏的问题

![image-20230822100839816](https://pic.shejibiji.com/i/2023/08/22/64e41c63b1d10.png)

虽然不做设计了，但开发中还是会经常有做图的需求。

于是就想在开发电脑上也安装下PS、AI啥的，于是下载了安装包（国内依旧推荐@vposy大神的，可以站内搜索找到他的官方地址）。

但是安装时总报错，让我都开始怀疑MAC系统好坏的问题了。

今天本来想，再找找Adobe老版本试试，不过发现网上资源并不多，而且国外网站套路也很多，想着我之前安装包都下载了，要不再试试……

其实提供的安装包里面都有说明文件的，我一直也是按照上面走的，但都失败了。

这一次，我查看说明文件时，意外注意到了一句话，就是这句：

> Bypass Install.app "Damaged" error:
>
> - Right-click Install.app and select "Open Package Contents" from the context menu
> - Navigate to Contents > MacOS then double-click the "Install" file

如果安装包损坏错误，右键单击 ` Install.app` 选择 `打开包内容` ，找到 `MacOS` 文件夹，再双击安装！

这……我不就是我要的答案吗？

接下来正式讲一下具体的安装步骤：

### 安装步骤

官方英文说明：

> Photoshop 24.0 U2B AIO [RiD]
>
> 1. Install AntiCC or Adobe CC Desktop app [skip if already installed]
> 2. Run Install.app in INSTALLER DMG to install app
> 3. Run PATCH PKG file to patch app

翻译成中文，图示就是这个（[设计笔记](https://www.shejibiji.com/) 制图）：

![image-20230822101305398](https://pic.shejibiji.com/i/2023/08/22/64e41c6a5e8d7.png)

1.

先安装 **AntiCC**

如果双击**AntiCC**没有打开的选项，可以右键图标，选择打开，就可以看到 打开 的按钮了。

![image-20230822101335002](https://pic.shejibiji.com/i/2023/08/22/64e42126e203c.png)

2.

安装 **Photoshop**

这是官方提供的说明：

> Photoshop 24.0 U2B INSTALLER [RiD]
>
> - AntiCC or Adobe CC Desktop app must be installed prior to running installer
> - Error 501 = AntiCC or Adobe CC Desktop requirement not met
>
> Bypass Install.app "Damaged" error:
> - Right-click Install.app and select "Open Package Contents" from the context menu
> - Navigate to Contents > MacOS then double-click the "Install" file

如果打开显示包损坏，请安装下图进行操作：

（右键，选择**打开包内容**，找到**MacOS**文件夹，双击**Install**）

![image-20230822101124454](https://pic.shejibiji.com/i/2023/08/22/64e42130e3c1b.png)

3.

运行 **PATCH**

运行完成后，就完成破解了。

接下来就可以开始使用了。

成功运行！

![image-20230822101541825](https://pic.shejibiji.com/i/2023/08/22/64e421330a563.png)