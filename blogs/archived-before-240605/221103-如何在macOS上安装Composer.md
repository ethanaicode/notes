# 如何在macOS上安装Composer



![Vida_2022-11-03_14-13-33](https://pic.shejibiji.com/i/2022/11/03/63635c2547c24.jpg)

如果是搞PHP开发的，应该很难避开Composer这个包管理工具，只需要简单的命令就可以实现包的添加、升级或者移除。

那么在macOS上该如何安装这个Composer呢？

## 通过Brew安装

最简单的做法当然是用Brew，不过有的新电脑可能还没有装这个，没有关系，之后我也会安排出一个教程。

先假设我们都有了Brew，然后我们打开命令行工具，直接输入：

```bash
brew install composer
```

不出意外的话，稍微等一会儿，就可以安装完成了，具体可以看下图：

![Vida_2022-11-03_13-50-04](https://pic.shejibiji.com/i/2022/11/03/63635b839f535.png)

安装完成后，输入：`composer --version`

如果出现下面这一段版本信息，就表示安装成功了。

![Vida_2022-11-03_13-51-42](https://pic.shejibiji.com/i/2022/11/03/63635b8d29c1f.png)

## 直接下载安装

首先我们直接点击后面的网址，下载最新的Composer安装包：https://getcomposer.org/composer.phar

然后我们打开终端，输入下面命令：

```bash
php ~/Downloads/composer.phar --version
```

这样就可以用了。

不过也不能每次想用的时候都输入上面这个命令对吧，所有我们可以考虑把这个应用放到启动目录下。

可以通过下面的命令移动位置并启动Composer：

```bash
cp ~/Downloads/composer.phar /usr/local/bin/composer
sudo chmod +x /usr/local/bin/composer
```

这样就不用每次手动启动了，尝试输入一下命令看看是否成功了：

```bash
composer --version
```



另外也可以用docker安装，我还没搞懂docker，也就不再这里瞎说了。

## 常用命令

Composer的命令还是很多的，这里仅仅几个基础的：

安装新框架： `composer install`

Composer升级：`composer update`

载入新的包：`composer require`

移除旧的包：`composer remove`



> 原文地址：[设计笔记](https://www.shejibiji.com/archives/9319)
