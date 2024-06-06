# Mac上Typora如何配置图片上传到图床，PicGo命令行CLI该怎么用？

![Ethan_2023-03-22_00-51-02](https://pic.shejibiji.com/i/2023/03/22/6419e08cb3d71.jpg)

我印象中以前`Typora`是支持`picgo.app`的。

安装好应用，配置好就可以直接使用了，我还写过教程：
[《如何搭配PicGo实现快速上传图片到个人图床》](https://www.shejibiji.com/archives/8411)

但是，我今天在一台Mac上试图参考教程，利用Picgo上传图片，却发现不能用了，图片选项中也没有了`picgo.app`，只能使用命令行模式了。

![Ethan_2023-03-22_00-49-02](https://pic.shejibiji.com/i/2023/03/22/6419e011e354e.jpg)

一番搜索无果后，被迫开始学习PicGo-Core的CLI命令，并配置好了Typora图片上传模块。

以下我将分享下具体的步骤。

主要分为三步：

1. 安装PicGo-Core核心；
2. 配置PicGo-Core核心；
3. 配置Typora图片上传模块。

我们来一步步讲：

## 一、安装PicGo-Core核心

可以参考官方教程：[PicGo-Core 快速上手](https://picgo.github.io/PicGo-Core-Doc/zh/guide/getting-started.html#%E5%85%A8%E5%B1%80%E5%AE%89%E8%A3%85)

我这里使用`npm`安装，需要先在本机安装`node.js`，然后才可以使用npm命令。

打开Mac的`Terminal`，输入以下命令全局安装PicGo：

``` bash
npm install picgo -g
```

安装好还不可以用，需要配置图床。

因为我一直使用的是自己搭建的兰空图床，所以将会以这个为例。

如果要利用别的图床，也可以参考这个步骤，都是一样的。

## 二、配置PicGo

1.

首先需要下载一个拓展：`lankong`，我们使用以下命令来安装拓展：

```bash
picgo install lankong
```

如图：

![Ethan_2023-03-22_01-05-22](https://pic.shejibiji.com/i/2023/03/22/6419e3dd03c4d.jpg)

2.

配置lankong拓展。

我们使用以下命令来设置：

```bash
picgo set uploader
```

然后安装步骤选择自己想要图床，并输入配置即可。如图：

![Ethan_2023-03-22_01-08-34](https://pic.shejibiji.com/i/2023/03/22/6419e49bcafd8.jpg)

这样就配置好了lankong拓展。

3.

选择默认上传的图床。

虽然设置好了扩展，但还要将其作为默认上传的图床才可以，我们修改下PicGo的配置文件。

我们使用vim打开PicGo的配置文件，一般为这个：

``` bash
vim ~/.picgo/config.json
```

我们修改其中`uploader`和`current`的值为我们自己想要的图床名称，即可保存退出。（vim如何使用可以站内搜教程）

![Ethan_2023-03-22_01-15-18](https://pic.shejibiji.com/i/2023/03/22/6419e62da4c46.jpg)

现在就可以测试是否可以上传图片了，使用下面命令：

```bash
# 上传具体路径图片
picgo upload /xxx/xxx.jpg
```

如图：

![Ethan_2023-03-22_01-18-05](https://pic.shejibiji.com/i/2023/03/22/6419e70e82b55.jpg)

## 三、配置Typora

如果以上都完成了，测试也没问题的话，Typora这边就简单了。

只需要打开Typora的设置：

![Ethan_2023-03-22_01-20-40](https://pic.shejibiji.com/i/2023/03/22/6419e775514a3.jpg)

然后找到图片设置，在图片上传那块，选择`自定义命令`，然后在命令行那里输入`picgo upload`即可完成配置。

![Ethan_2023-03-22_01-22-03](https://pic.shejibiji.com/i/2023/03/22/6419e7c46be12.jpg)

现在应该就可以直接在Typora中直接上传图片到图床了。

如果有问题可以评论留言，我看到会回复。（第一次站内留言不会立即显示，需要审核）。