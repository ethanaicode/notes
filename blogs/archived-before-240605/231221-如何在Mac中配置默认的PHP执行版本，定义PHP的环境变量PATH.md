# 如何在Mac中配置默认的PHP执行版本，定义PHP的环境变量PATH

最近升级了Mac的系统，从 11 直接升级到了 13 macOS Ventura，不得不说颜值确实提升了不少。

![Ethan_2023-12-21_11-12-11](https://pic.shejibiji.com/i/2023/12/21/6583ad22013dd.jpg)

但使用后发现了一个问题，新版本不默认带PHP了，如果直接执行PHP命令就会无效。

按照以前使用Windows的习惯，就知道这个时候应该配置下**环境变量**。

MAC中定义环境变量的主要有两个地方：`~/.bash_profile` 和 `/etc/profile`。

看路径也知道，带`~`的是表示当前用户的配置，`/etc`下面的配置一般都是全局配置。

我们只需要修改用户的配置即可。



那么直接开始配置吧。

## 配置步骤

1.

**首先找到PHP的目录**

可以通过`phpinfo`查看，因为我用的MAMP，我知道它的目录肯定是在安装目录下。

也就是：`/Applications/MAMP/bin/php`，在这个下面可以看到所有已安装的PHP版本。

![Ethan_2023-12-21_11-29-08](https://pic.shejibiji.com/i/2023/12/21/6583b128e0ef9.jpg)

我们选择最新的8.2，找到其`/bin`目录，得到完整的文件路径：

```bash
/Applications/MAMP/bin/php/php8.2.0/bin
```

2.

**增加环境配置**

我们打开命令行工具`Terminal`，运行命令`vim ~/.bash_profile`

输入<kbd>i</kbd>，然后复制下面命令到文件顶部（路径改为自己的）：

```bash
 export PATH=/Applications/MAMP/bin/php/php8.2.0/bin:$PATH
```

然后按<kbd>ESC</kbd>，输入`:wq`，按<kbd>Enter</kbd>保存并退出。

**然后执行修改**，在`Terminal`，运行命令`source ~/.bash_profile`

3.

**配置成功**

现在应该就成功配置了。

你可以通过输入`which php`，来查看PHP的新路径，如果成功返回正确的目录，则表示成功了。

![SCR-20231221-kqwq](https://pic.shejibiji.com/i/2023/12/21/6583b5e83f45e.png)

## 重启Mac电脑，配置失效问题解决

如果发现重启Mac电脑，配置就会失效。

这是由于Mac默认环境改成了`zsh`导致的，它只会默认加载`~/.zshrc`文件。

解决办法就是在这个文件后面加上这句；

```bash
source ~/.bash_profile
```

这样重启电脑，这个配置就不会失效了。
