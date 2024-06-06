# 如何安装 Ubuntu Linux，分步详解

> 官方镜像下载地址：https://ubuntu.com/download/desktop
>
> ETCHER软件下载：https://etcher.balena.io/#download-etcher

![Ethan_2023-10-10_15-47-00](https://pic.shejibiji.com/i/2023/10/10/652501831adbd.jpg)

## 1、概述 (Overview)

Ubuntu是一个开源的操作系统，适用于桌面、服务器和云端环境。

这个教程将指导你如何安装Ubuntu桌面版。

准备开始前：

   - 确保你的电脑满足最低系统要求（最少25G存储）。

   - 准备一个USB闪存驱动器或DVD（12G或者更大）。

## 2、下载Ubuntu镜像 (Download Ubuntu Image)

首先需要下载 Ubuntu 镜像。

官方镜像下载地址：https://ubuntu.com/download/desktop

打开后推荐选择 LTS 的版本，也就是长期服务版，我们这里下载 22.04.3

![image-20231010150315960](https://pic.shejibiji.com/i/2023/10/10/6524f7354542b.png)

注意：不同的版本，安装界面可能有区别，但大体流程应该是类似的。

## 3、创建系统安装U盘 (Create a bootable USB stick)

有了镜像后，我们还需要制作一个系统安装U盘，用来引导安装系统。

官方推荐的是 **balenaEtcher** 这个工具，我看了下操作比较傻瓜，而且多平台支持的。

所以这里也将会用这个工具。

打开[ balenaEtcher ](https://etcher.balena.io/#download-etcher)官网，会看到这样的界面，我们点击`Download Etcher`：

![image-20231010142437166](https://pic.shejibiji.com/i/2023/10/10/6524ee2761d1d.png)

然后选择自己合适的系统版本进行下载：

![image-20231010142552169](https://pic.shejibiji.com/i/2023/10/10/6524ee716f1d9.png)

下载后打开该软件，先选择你下载好的Ubuntu系统镜像，然后选择U盘，就可以立即开始制作系统安装引导盘。

![222_1](https://pic.shejibiji.com/i/2023/10/10/65250210cdd1a.jpg)

![222_2](https://pic.shejibiji.com/i/2023/10/10/6525021c517f9.jpg)

## 4、从U盘启动开始安装Ubuntu (Install Ubuntu)

准备好系统U盘后，就可以开始准备安装了。

1.

**这里要注意确保 BIOS 设置为 UEFI**

*(这一步可以忽视，可以直接跳到第3步，如果发现U盘启动不了再说)*

这个各个主板操作会有区别，这里以Dell为例：

重启后按<kbd>F2</kbd>进入Dell电脑的BIOS设置，

1）首先关闭安全启动引导

![ka06P000000HRbyQAG_zh_CN_9](https://pic.shejibiji.com/i/2023/10/10/6524f44890fde.jpeg)

2）然后选择 禁用 传统 选项 ROMS

![ka06P000000HRbyQAG_zh_CN_8](https://pic.shejibiji.com/i/2023/10/10/6524f47b0a95c.jpeg)

3）确保  BIOS 设置为 UEFI

![ka06P000000HRbyQAG_zh_CN_7](https://pic.shejibiji.com/i/2023/10/10/6524f550b4ba9.jpeg)

2.

**选择U盘启动**

插入U盘，按<kbd>F12</kbd>进入启动选项界面，选择 UEFI 启动。

![Ethan_2023-10-10_15-14-29](https://pic.shejibiji.com/i/2023/10/10/6524f9ded2583.jpg)

看到这个界面就表示启动成功了：

![Ethan_2023-10-10_15-14-01](https://pic.shejibiji.com/i/2023/10/10/6524f9c3c6055.jpg)

3.

**正式开始安装系统吧**

先选择语言。支持中文，我这里选择英语。

如果第一次用可以选择<kbd>Try Ubuntu</kbd>，可以用这个查看一下是否硬件都被正确识别了。

![Ethan_2023-10-10_15-13-19](https://pic.shejibiji.com/i/2023/10/10/6524f9a8acb87.jpg)

选择先尝试后，就会进入 Ubuntu 的桌面。

没问题后可以选择右下角的 **安装Ubuntu**。 

![Ethan_2023-10-10_15-18-14](https://pic.shejibiji.com/i/2023/10/10/6524fac39bbbb.jpg)

之后会回到安装界面，选择 继续（continue）。

接下来会进入一堆选项，可以看图作为参考：

![1](https://pic.shejibiji.com/i/2023/10/10/6524fcbb4502c.jpg)

![2](https://pic.shejibiji.com/i/2023/10/10/6524fcc431c6d.jpg)

![3](https://pic.shejibiji.com/i/2023/10/10/6524fccaa8b8e.jpg)

![4](https://pic.shejibiji.com/i/2023/10/10/6524fcd1581fe.jpg)

![Ethan_2023-10-10_15-24-30](https://pic.shejibiji.com/i/2023/10/10/6524fcdb9231f.jpg)

![Ethan_2023-10-10_15-24-51](https://pic.shejibiji.com/i/2023/10/10/6524fce10df5b.jpg)

这一步创建登录用户信息，输入你的名字、电脑的名字、用户名和密码。

名字可以自己写一个，之后大多数地方显示设备都将会这个名字。

![Ethan_2023-10-10_15-25-17](https://pic.shejibiji.com/i/2023/10/10/6524fce580782.jpg)

之后就可以安静等待安装完成了。

![Ethan_2023-10-10_15-25-42](https://pic.shejibiji.com/i/2023/10/10/6524fceb5e27a.jpg)

**安装完成后，重启电脑并移除USB闪存驱动器。**

4

**首次启动，登录并开始使用Ubuntu**

**不要忘记更新！ 确保系统处于最新状态。**

最简单的方法是通过“Software Updater”应用程序来进行更新。

也可以使用终端来更新Ubuntu。

按下<kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>T</kbd>以打开终端窗口（或者点击侧边栏中的终端图标）。

输入以下内容：

```bash
sudo apt update
```

系统会提示您输入登录密码。

这将检查是否有可用的更新，并告诉您是否需要应用它们。

要应用任何更新，请输入：

```bash
sudo apt upgrade
```

输入Y，然后按ENTER确认以完成更新过程。

### 本文参考

> [如何在戴尔计算机上安装 Ubuntu Linux](https://www.dell.com/support/kbdoc/zh-cn/000131655/%E5%A6%82%E4%BD%95%E5%AE%89%E8%A3%85-ubuntu-linux-on-your-dell-pc)
>
> [Install Ubuntu desktop](https://ubuntu.com/tutorials/install-ubuntu-desktop#11-dont-forget-to-update)