# 详解macOS如何利用composer创建laravel项目

![Vida_2022-11-03_17-33-11](https://pic.shejibiji.com/i/2022/11/03/636390268f247.jpg)

有两种方式可以创建一个新的 Laravel 项目，这两种创建方式都是从命令行执行的：第一种是通过全局的 Laravel 安装器，另一种是通过 Composer 的 create-project 命令。

今天我们来用Composer创建一个新的 Laravel 项目。

## 具体步骤

1.

首先新建一个项目文件夹，然后鼠标右键，选择`新建位于文件夹位置的终端窗口`：

![Vida_2022-11-03_17-41-35](https://pic.shejibiji.com/i/2022/11/03/63639028d6889.jpg)

2.

然后输入下面命令创建 Laravel 项目：

```bash
composer create-project --prefer-dist laravel/laravel blog
```

> **命令解释：**
>
> composer：表示执行该程序；create-project ：创建项目；laravel/laravel：需要创建的项目名称；
>
> --prefer-dist：优先下载压缩包方式，而不是直接从GitHub上下载源码；
>
> blog：表示创建的项目目录名称。

![Vida_2022-11-03_17-30-50](https://pic.shejibiji.com/i/2022/11/03/6363902e5810b.jpg)

使用这个方式安装的一个好处是可以自由选择 Laravel 的版本。

比如要安装 5.6 版本的项目 `blog56` ，可以这么做：

```bash
composer create-project laravel/laravel blog56 5.6.* --prefer-dist
```

3.

最后看到这个就表示创建成功：

![Vida_2022-11-03_17-31-45](https://pic.shejibiji.com/i/2022/11/03/636390220bbab.jpg)

最后只需要访问laravel项目下的`public`目录，就可以看到默认的首页了：

![Vida_2022-11-03_17-33-05](https://pic.shejibiji.com/i/2022/11/03/6363901ab7949.jpg)

> **踩坑笔记：**
>
> 要注意php版本，laravel对php是有最低要求的，具体可以看这个：
>
> Laravel 5.1  PHP对应的版本>=5.5.9
>
> Laravel 5.2  PHP对应的版本>=5.5.9
>
> Laravel 5.3  PHP对应的版本>=5.6.4
>
> Laravel 5.4  PHP对应的版本>=5.6.4
>
> Laravel 5.5  PHP对应的版本>=7.0.0
>
> Laravel 5.6  PHP对应的版本>=7.1.3
>
> Laravel 5.7  PHP对应的版本>=7.1.3
>
> Laravel 5.8  PHP对应的版本>=7.1.3
>
> Laravel 6.x  PHP对应的版本>=7.2.0
>
> Laravel 7.x  PHP对应的版本>=7.2.5
>
> Laravel 8.x  PHP对应的版本>=7.3.0
>
> Laravel 9.x  PHP对应的版本>=8
>
> 我第一次安装就因为php版本太高，导致自动安装了laravel最新版本，结果mamp的免费版默认是php7.4
>
> 结果就怎么都跑不起来，报500错误，让我迷惑了一下午。