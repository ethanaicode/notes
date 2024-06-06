# [笔记01]ThinkPHP6入门到精通：安装TP6并开启调试

> 使用教程：[【李炎恢】【ThinkPHP6.x / PHP框架】](https://www.bilibili.com/video/BV12E411y7u8)

[本地链接](E:\BaiduNetdiskDownload\哔哩哔哩\小虫师兄\ThinkPHP6入门到精通)

![img](https://pic.shejibiji.com/i/2022/06/06/629dd7216f741.png)

`6.0`版本开始，必须通过`Composer`方式安装和更新，所以你无法通过`Git`下载安装。

## 本地安装部署ThinkPHP 6.x

### 安装Composer

[Composer官网](https://getcomposer.org/)，你可以自行前去下载，也可以直接下面链接下载：

[Composer-Setup.exe](https://getcomposer.org/Composer-Setup.exe)。

![2022-06-06_11-13-53](https://pic.shejibiji.com/i/2022/06/06/629d721c8848b.jpg)

![2022-06-06_11-15-01](https://pic.shejibiji.com/i/2022/06/06/629d720fb7d25.jpg)

接下来就是点击`Next`就可以完成安装。

**使用国内镜像（阿里云）**

由于众所周知的原因，国外的网站连接速度很慢。因此安装的时间可能会比较长，我们建议使用国内镜像（阿里云）。

打开命令行窗口（windows用户）或控制台（Linux、Mac 用户）并执行如下命令：

```c
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
```

![2022-06-06_11-28-26](https://pic.shejibiji.com/i/2022/06/06/629d745ea090c.jpg)

接下来就可以准备部署ThinkPHP 6.x

> 这个时候请先打开本地的php开发环境

### 安装ThinkPHP 6.x

首先我们需要进入我们要安装TP6.x的文件目录。

可以还是在命令行中操作。

通过使用`cd ..`来回到上一集目录；

通过使用`cd path`来访问目录。

访问到web根目录下面，执行下面命令即可开始安装：

```c
composer create-project topthink/think tp
```

这里的`tp`目录名你可以任意更改，这个目录就是我们后面会经常提到的应用根目录。

可以参考我的：

```c
C:\Users\Risen>cd ..

C:\Users>cd ..

C:\>cd wamp64\www

C:\wamp64\www>composer create-project topthink/think www_tp01
```

我们这里安装的是**稳定版**。

![2022-06-06_11-41-21](https://pic.shejibiji.com/i/2022/06/06/629d77d39d81f.jpg)

![2022-06-06_11-45-44](https://pic.shejibiji.com/i/2022/06/06/629d786f646cd.jpg)

如果有报错，或者你想升级版本，可以进入刚刚安装的web目录下，执行下面命令进行更新：

```c
composer update topthink/framework
```

### 访问ThinkPHP 6.x

现在我们就部署好了ThinkPHP 6.x。

接下来我们更改下网站目录为`public`，即可访问网站了。

我这里直接改下Apache的虚拟host，然后重启下Apache即可。

![2022-06-06_11-56-09](https://pic.shejibiji.com/i/2022/06/06/629d7ae012716.jpg)

改好配置，然后直接域名访问即可正确打开。

![2022-06-06_11-57-24](https://pic.shejibiji.com/i/2022/06/06/629d7b2a9fac8.jpg)

现在就完成了ThinkPHP的本地部署了。

## 开启调试模式

默认情况下，如果访问错误，是没有任何提示信息的。

就像下面这样：

![2022-06-06_12-05-13](https://pic.shejibiji.com/i/2022/06/06/629d7d0044225.jpg)

我们通过开启调试模式，来显示更多信息，方便我们找到问题，并做调整。

开启也特别简单，只要到网站目录下，找到`.env`的文件，把前面的`.example`删掉皆可。

![2022-06-06_12-06-52](https://pic.shejibiji.com/i/2022/06/06/629d7d7ec6f81.jpg)

删掉后，我们再访问刚才的错误页面，就可以看到完整的错误信息了：

![2022-06-06_12-08-05](https://pic.shejibiji.com/i/2022/06/06/629d7dbeceed7.jpg)

首页右下角也会显示ThinkPHP的标志：

![2022-06-06_12-09-31](https://pic.shejibiji.com/i/2022/06/06/629d7e128c80c.jpg)

此时就表示我们已经正确开启了调试模式。

如果需要关闭调试模式，只要打开`.env`文件，把第一句的`True`改成`false`即可。



事实上，在`config`下的很多`php`文件中，也可以看到`显示错误信息`的开关。

这个是可以显示简单的调试信息的。

> .env 环境变量仅用于本地开发测试，部署后会被忽略。
>
> 部署到服务器后，只会获取到config下的配置文件。
>
> （还蛮科学的！毕竟本地的数据库网站、域名都仅仅用于测试开发，和实际部署的信息会有很大的差异，这样每次部署都不用特意修改这些配置）
