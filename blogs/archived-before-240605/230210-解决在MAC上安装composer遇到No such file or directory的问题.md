# 解决在MAC上安装composer遇到No such file or directory的问题

最近在一台新的MAC上安装composer时，一直无法成功，提示错误No such file or directory，没有这个文件或者目录，以前安装没遇到过啊，当时就觉得奇怪了。

搞得我还跑到那个目录去看了下，结果在`usr`下看到了`bin`目录，差点以为是我的电脑目录结构不一样，于是准备把compser文件复制到这个目录下了，幸好系统阻止了我。

[![1675967720222.png](https://img.shejibiji.com/2023/02/10/63e53cec9ab58.png)](https://img.shejibiji.com/2023/02/10/63e53cec9ab58.png)

后面查资料才知道，没有目录自己建一个就好了，不过要注意需要配置权限，可以使用下面命令建一个目录：

```bash
sudo mkdir -p -m 775 /usr/local/bin
```

可能会让你输入密码，正确输入即可。

然后再次在**composer.phar所在的目录**执行：

```bash
sudo mv composer.phar /usr/local/bin/composer
```

现在应该就可以了，我们可以测试下，输入：

```bash
composer --version
```

如果显示一堆信息，就表示成功了，具体可以看下图：

<img src="https://img.shejibiji.com/2023/02/10/63e53f94688a5.png" alt="1675968377891.png" title="1675968377891.png" />