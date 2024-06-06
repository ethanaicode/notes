# 如何给PHP安装redis拓展并启用，多图详细步骤讲解

如何给PHP安装redis拓展，说实话，网上教程不少，可是看了半天，也没完全看明白。

折腾了半天，走了不少弯路，终于算是成功装上了。

所以特意详细记录下过程，多图讲解，希望能给讲明白了。

1.

首先通过`phpinfo`，找到自己的php文件夹：

![Ethan_2023-04-07_19-31-59](https://pic.shejibiji.com/i/2023/04/07/642fff56e8ca1.jpg)

2.

然后通过cd命令走到自己`bin`文件夹下，比如我的：

```bash
/Applications/MAMP/bin/php/php8.2.0/bin
```

在这里你可以看到`phpize`和`php-config`，这两个文件是我们待会要用到的。

**（这两步只是为了简化操作，并不一定完全要做！在这个文件夹下操作，可以少输入不少路径，不容易搞错。）**

![Ethan_2023-04-07_19-30-27](https://pic.shejibiji.com/i/2023/04/07/642ffedbed585.jpg)

3.

**下载phpredis插件。**

我这里直接克隆官方仓库的，使用命令：

```bash
git clone https://github.com/phpredis/phpredis.git
```

下载后，我们进入phpredis文件夹：

```bash
cd phpredis
```

如图：

![Ethan_2023-04-07_19-36-24](https://pic.shejibiji.com/i/2023/04/07/643000420bcf1.jpg)

4.

**执行phpize。**

使用命令：`../phpize`

（如果头2步没有和我一样，这里需要根据自己的phpize路径来填写）

> 这一步很重要，是PHP准备编译环境。如果出现无法找到“autoconf”的错误，可以看文末先解决报错。

![Ethan_2023-04-07_19-38-59](https://pic.shejibiji.com/i/2023/04/07/643000de71def.jpg)

5.

**执行php-config。**

使用命令：`./configure --with-php-config=../php-config`

（如果头2步没有和我一样，这里需要根据自己的php-config路径来修改）

![Ethan_2023-04-07_19-41-22](https://pic.shejibiji.com/i/2023/04/07/6430016aaaecf.jpg)

6.

**编译安装。**

使用命令：`sudo make && sudo make install`

![Ethan_2023-04-07_19-43-02](https://pic.shejibiji.com/i/2023/04/07/643001d0105b4.jpg)

7.

**编译完成后，可以选择删掉安装包。**

使用命令：`cd ../ && rm -rf phpredis`

![Ethan_2023-04-07_19-44-45](https://pic.shejibiji.com/i/2023/04/07/6430024732501.jpg)

8.

**修改php的配置文件。**

配置文件在bin文件夹上一层，conf文件夹下，名字为`php.in`。

你如果按照我说的步骤做的话，此时应该输入命令：`sudo vim ../conf/php.ini`

（看图吧，我已经尽力画清楚了）

![Ethan_2023-04-07_19-49-15](https://pic.shejibiji.com/i/2023/04/07/6430034c87758.jpg)

在配置文件中，加上redis拓展，命令为：`extension=redis.so`

![Ethan_2023-04-07_19-22-21](https://pic.shejibiji.com/i/2023/04/07/642ffcf9b4913.jpg)

然后保存退出。

退出后重启下php。

9.

**测试成功。**

再看下phpinfo的信息，搜索redis关键词，可以看到redis拓展名就表示安装拓展成功了。

![Ethan_2023-04-07_19-20-02](https://pic.shejibiji.com/i/2023/04/07/642ffc6e7efe8.jpg)

代码中可以测试下，设置redis键和值，然后用get获取下。

![Ethan_2023-04-07_19-24-09](https://pic.shejibiji.com/i/2023/04/07/642ffd653e833.jpg)

请求下接口，已经可以看到成功返回的测试数据了：

![Ethan_2023-04-07_19-24-51](https://pic.shejibiji.com/i/2023/04/07/642ffd8f8d9e9.jpg)

Enjoy！

有问题可以留言，我会尽力解答。



[补充：2023-12-04]

**如何解决无法找到autoconf的错误？**

执行`phpize`时，出现报错信息，无法找到**autoconf**：

```bash
Cannot find autoconf. Please check your autoconf installation and the
$PHP_AUTOCONF environment variable. Then, rerun this script.
```

解决办法就是安装**autoconf**即可。

最简单的办法是用**brew**安装：

```bash
brew install autoconf
```

其它系统可以参考这个：

For CentOS:

```bash
yum install autoconf
```

for Ubuntu :

```bash
apt-get install autoconf
```

for fedora 24-27:

```bash
dnf install autoconf
```