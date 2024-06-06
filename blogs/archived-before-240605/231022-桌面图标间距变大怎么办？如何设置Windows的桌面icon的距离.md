# 桌面图标间距变大怎么办？如何设置Windows的桌面icon的距离

![1697972497417.jpg](https://img.shejibiji.com/2023/10/22/653501130ce0c.jpg)

今天开机后突然发现桌面图标的间距变得异常的大，不管是缩放图标尺寸，都不影响这个间距，看着实在难受。

网上查阅了下资料，原因可能和接了副屏有关，应该是属于系统BUG了。

**那么该如何调整桌面图标间距呢？**

其实图标间距这个信息是存在注册表（regedit）的，所以可以通过直接修改注册表达到这个目的，修改的位置为：

```bash
HKEY_CURRENT_USER\Control Panel\Desktop\WindowMetrics
```

里面`IconSpacing `、`IconVerticalSpacing `的值就是图标间距了。

`IconSpacing `表示图标水平的值，

`IconVerticalSpacing `表示图标垂直的值。

推荐改为-1125，这是官方默认的初始值。

如果不喜欢也可以按照自己喜好进行修改，总之负的值越大，间距也就越大。

## 高阶玩法

如果系统总莫名其妙给你调大桌面图标间距，每次手动注册表，来恢复Windows图标间距，未免麻烦了点。

这里就可以考虑通过`bat`批处理脚本，一键运行实现这个目的。

我们直接新建一个文件：`modify_icon_spacing.bat`（可以用记事本建立，保存格式为bat）

然后输入下列命令：

```bat
@echo off

:: Set the values for IconSpacing and IconVerticalSpacing to -1125
reg add "HKEY_CURRENT_USER\Control Panel\Desktop\WindowMetrics" /v IconSpacing /t REG_SZ /d "-1125" /f
reg add "HKEY_CURRENT_USER\Control Panel\Desktop\WindowMetrics" /v IconVerticalSpacing /t REG_SZ /d "-1125" /f

:: Log off and log back in to apply the changes
shutdown /l

```

保存好这个文件。

然后每次只要双击这个`modify_icon_spacing.bat`就可以快速恢复图标间距了。其中的-1125就是我们希望恢复的值，你需要修改为别的值也可以更改这个值即可。

注意，最后的命令：**shutdown /l** 是退出当前用户，目的是为了重新登录立即看到图标间距的改变。

如果你不需要立即看到改变的效果，也可以删除这条命令，这样就不会自动注销计算机了，不过效果的改变需要重新登录后才可以看到。

如果不知道如何创建这个自动化脚本工具，也可以直接下载我们写好的脚本，下载后直接运行即可。

## 下载地址

[modify_icon_spacing.bat](https://shejibiji.lanzoul.com/i8cae1cjsfja)
