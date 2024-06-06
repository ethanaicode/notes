# 在Windows上安装Node.js详细步骤教程

<a href="https://www.laa.one/image/ZyFo"><img src="https://www.laa.one/images/2021/11/24/imagead4dc80da928fbaf.png" alt="imagead4dc80da928fbaf.png" border="0"></a>

最近白捡了一个服务器，不知道能做点啥，于是决定尝试下VuePress。

因为经常有客户想要一个内部在线文档的需求，而这个VuePress简直就是为这个需求而存在的。

但是这玩意直接在linux上安装好像不是很方便，在网上搜了一圈教程也没有完全解决。

虽然宝塔面板上也可以直接安装Node.Js，甚至也可以选择vuepress，但是配置的时候总是报错，入口文件也经常找不到，而网上教程都是本地搭建，然后再同步到服务器的。

那我就老老实实也按照教程，在本地先搭建看看吧。刚好可以熟悉下配合git库完成web工作。

那首先就是要有一个Node.js，具体怎么安装呢？

## 安装步骤

1.

**下载安装包**

打开Node.js官网https://nodejs.org/，找到DOWNLOADS目录，直接下载Windows版本。

<a href="https://www.laa.one/image/ZGZA"><img src="https://www.laa.one/images/2021/11/24/image.md.png" alt="image.md.png" border="0"></a>

2.

**安装**

打开下载包，选择文件目录，正常安装就好。

<a href="https://www.laa.one/image/ZsDR"><img src="https://www.laa.one/images/2021/11/24/01.png" alt="01.png" border="0"></a>我都是默认选项，一般不用管。

安装结束后，可以测试下安装时候成功了。

按住WIN+R，输入CMD，打开命令行。

输入``node -v`和`npm -v`，可以查看node和npm的版本号。

<a href="https://www.laa.one/image/ZHzF"><img src="https://www.laa.one/images/2021/11/24/image4b3178cf08b8418f.png" alt="image4b3178cf08b8418f.png" border="0"></a>

到这一步就算完成了！

3.

**更改模块安装和缓存路径（不推荐）**

（不熟悉系统的话，可跳过这一步）

因为在执行例如npm install webpack -g等命令全局安装的时候，默认会将模块安装在C:\Users\用户名\AppData\Roaming路径下的npm和npm_cache中，不方便管理且占用C盘空间。

我们可以自定义目录。

可以现在node.js根目录下，新建文件夹node_g和node_cache。

<a href="https://www.laa.one/image/ZLPX"><img src="https://www.laa.one/images/2021/11/24/imagecff3b40cb8aabde3.png" alt="imagecff3b40cb8aabde3.png" border="0"></a>

然后在命令行里，执行以下命令：

```
npm config set prefix "D:\NodeJs\node_g"

npm config set cache "D:\NodeJs\nodejs\node_cache"
```

执行完不会有成功提示。

然后也要相应的改一下系统的环境变量。



**配置环境变量**

Win10电脑下，搜索“环境变量”，打开编辑系统环境变量。

![image-20211124150748916](C:\Users\Risen\AppData\Roaming\Typora\typora-user-images\image-20211124150748916.png)



在“环境变量” -> “系统变量”：新建一个变量名为 “**NODE_PATH**”， 值为**“D:\NodeJs\node_g\node_modules”**；

“环境变量” -> “用户变量”：编辑用户变量里的**Path**，将相应npm的路径（“C:\Users\用户名\AppData\Roaming\npm”）改为：**“D:\NodeJs\node_g”**。

<a href="https://www.laa.one/image/ZT1m"><img src="https://www.laa.one/images/2021/11/24/imaged13e7f82f96c49fe.md.png" alt="imaged13e7f82f96c49fe.md.png" border="0"></a>

这样配置就完成了。

**另外要记得把NodeJs文件夹的写入权限打开，不然会报错。**





