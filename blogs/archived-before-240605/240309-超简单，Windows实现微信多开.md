# 超简单，Windows实现微信多开

![超简单，Windows实现微信多开.jpg](https://img.shejibiji.com/2024/03/09/65ebfddf35ff9.jpg)

其实原理很简单，就是通过**同时**多次打开微信应用来实现。

最简单的就是通过鼠标连续点击微信图标或者回车键疯狂双击微信图标来实现多开，但作为一名程序员，对于这种不太好控制的情况，肯定是不推荐的。

这里主要推荐两种办法来实现：

1. 运行批量处理脚本文件`.bat`来实现；
2. 使用命令行运行命令来实现。

## 方法一，批处理脚本文件

首先新建一个批量处理脚本文件，如`WeChatMultiple.bat`。

然后右键使用记事本打开，输入下面命令：

```bash
@echo off

start "" "H:\Program Files\WeChat\WeChat.exe"

start "" "H:\Program Files\WeChat\WeChat.exe"

exit
```

要注意：`"H:\Program Files\WeChat\WeChat.exe"`这个为微信应用的启动路径，你需要修改成你自己的。

想多开几个，就复制几行`start`

保存后，再点击运行这个脚本即可。

## 方法二，启动应用命令

直接打开命令行工具（<kbd>Win</kbd>+<kbd>R</kbd>，输入`cmd`打开）

 然后使用 `cd` 命令访问到微信程序的安装目录，类似这样（记得替换应用的启动路径）：

```
cd H:\Program Files\WeChat
```

最后使用启动应用命令`start`，通过`&`号来分割，实现同时执行多个启动应用的目的：

```bash
start WeChat.exe&WeChat.exe
```

或者把两个操作合并下，直接使用这个命令，效果也是一样的：

```bash
start H:\Program Files\WeChat\WeChat.exe&H:\Program Files\WeChat\WeChat.exeWeChat.exe
```

Enjoy!