# 解决Emby演员头像无法显示的问题，威联通修改HOST方法

![image-20220322193821947](https://ossimg.yzitc.com/2022/03/22/9a3ee0dda1d27.png)

 在威联通NAS中搭建好Emby影音库之后，配合tMM工具刮削，就可以看到电影墙了。

但是点开影片详情页之后却只有名称，无法正常显示演职人员的头像，对于强迫症的我来说，就比较难受。

![image-20220322194058613](https://ossimg.yzitc.com/2022/03/22/63575a3371fb8.png)

今天被隔离在家，闲着没事，就尝试解决下这个问题。

首先寻找问题，我打开tMM查看演员刮削的情况。

tMM刮削后，打开`编辑电影资料`，找到`演员和工作人员`，点击编辑，发现目前演员的头像资料都是tmdb的图片地址。

![image-20220322194701703](https://ossimg.yzitc.com/2022/03/22/d74a217d2c907.png)

推测无法在Emby中显示的原因是因为tmdb域名被污染无法访问导致的。

尝试直接访问tmdb的官网，果然是无法连接的。

那么解决这个问题就比较简单了。解决掉tmdb的DNS污染问题就好了，这种一般都是通过修改host文件即可。

### 解决方法

1.

**首先找到NAS的host文件**

（我的是威联通NAS，其他的方法类似）

我们利用Winscp工具，通过SFTP协议访问NAS根目录，在`/etc/`目录下，往下翻找到hosts文件。

（Winscp工具的使用方法可以自己搜索了解下，如果有需要之后可以考虑出个教程）

![image-20220322195628889](https://ossimg.yzitc.com/2022/03/22/72a02924be773.png)

2.

**修改hosts文件**

我们右键选择编辑，打开hosts文件。

在后面添加下面这段语句：

```text
13.224.161.90 api.themoviedb.org
104.16.61.155 image.themoviedb.org
13.35.67.86 api.themoviedb.org
54.192.151.79 www.themoviedb.org
13.225.89.239 api.thetvdb.com
13.249.175.212 api.thetvdb.com
13.35.161.120 api.thetvdb.com
13.226.238.76 api.themoviedb.org
13.35.7.102 api.themoviedb.org
13.225.103.26 api.themoviedb.org
13.226.191.85 api.themoviedb.org
13.225.103.110 api.themoviedb.org
52.85.79.89 api.themoviedb.org
13.225.41.40 api.themoviedb.org
13.226.251.88 api.themoviedb.org
```

点击保存并关闭，这样就修改好了，现在NAS应该就可以正常访问tmdb获取演员头像了。

3.

**刷新元数据，获取头像**

我们打开影片库，选择`刷新元数据`，稍微等待下Emby缓存演员头像，一会儿之后，刷新下页面就可以看到演员的头像了。


![image-20220322194225246](https://ossimg.yzitc.com/2022/03/22/5793ef86f75fb.png)

现在这样就比较舒适了。

### 拓展思维

发现是这个问题后，我就在想使用tMM刮削的时候，是不是就可以把演员头像一起给刮削了。

打开tMM的`设置`菜单，找到`电影`下面的`额外的图片`，可以看到有个选项`演员图片保存到.actors`目录下。

![image-20220322200307908](https://ossimg.yzitc.com/2022/03/22/d5d7a7368022f.png)

我们勾选上这个，应该就可以下载演员图片到电影目录了。

于是我测试了下，首先把电脑上的host文件修改下。

然后找部电影刮削一下，整理后，打开电影目录……

嗯……并没有用……还是没有演员的目录。

反正目前目的已经达到了，这个问题之后我们再折腾看看。



另外emby的演员头像是缓存在这个位置的：

`/share/CACHEDEV1_DATA/.qpkg/EmbyServer/programdata/metadata/people`



这是这次折腾，所获取的所有资料，希望可以给大家一点帮助。

以上。

