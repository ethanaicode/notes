# 如何关闭Mac上的Microsoft AutoUpdate微软自动更新弹窗提示

MacOS安装Microsoft Office for Mac之后，会弹出Microsoft Auto Update应用自动更新工具。

就像下面这样：

![Ethan_2023-03-27_15-12-35](https://pic.shejibiji.com/i/2023/03/27/642141f6be498.jpg)

关闭之后，过一会又会弹出来，真的是有点烦人！

得益于Mac的安全机制，我们可以轻易关闭它：

## 方法一、取消应用权限

我们可以直接关闭这个Microsoft AutoUpdate的启动权限，来阻止它执行。

打开Mac上的terminal终端，输入下面命令：

```bash
cd /Library/Application\ Support/Microsoft/MAU2.0 
```

打开微软的应用文件夹，然后输入下面命令：

```bash
sudo chmod 000 Microsoft\ AutoUpdate.app 
```

关闭这个应用的所有权限，这样它就不会再被自动执行了。

![Ethan_2023-03-27_15-14-23](https://pic.shejibiji.com/i/2023/03/27/6421425c926cc.jpg)

## 方法二：删除这个应用

简单粗暴，不需要利用命令行，直接手动删除……（不推荐）

直接按快捷键`command（⌘）+⇧+G`，打开`前往文件夹`，然后输入下面这个路径：

`/Library/Application Support/Microsoft/MAU2.0`

![Ethan_2023-03-27_15-22-32](https://pic.shejibiji.com/i/2023/03/27/6421445363320.jpg)

删除里面的应用即可。