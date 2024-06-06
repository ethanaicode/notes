# 如何在Typora中利用PicGo.APP实现粘贴图片快速上传到阿里云OSS

![image-20211201165730331](https://ossimg.yzitc.com/2021/12/01/80d43c8ce5b03.png)

[Typora](https://www.typora.io/)是我一直在使用的Markdown 编辑器，编辑起来就很舒服。也可以自定义主题，获得远超记事本的文字编辑快乐。

所以我现在所有的博客文章都是先在Typora编辑器里面写好，然后再使用Typora的`复制为HTML代码`，粘贴到博客上。

不过这个时候就有一个问题了，图片该怎么办。

因为本地图片插入到Typora里面，默认的图片地址是本地路径，直接粘贴到博客中是无法显示的。

这个时候就需要把图片都上传到云端，而Typora编辑器就支持多个上传工具，这样就很方便了。

我这里使用的[PicGo](https://github.com/Molunerfinn/PicGo)，一款将图片上传到图床的工具，支持目前主流的图床和对象存储(阿里云 OSS、腾讯云 COS等)。

和 Typora 搭配使用，可以将本地截图的直接复制到 Typora 后自动上传图床，返回图床图片链接，免除保存本地图片、路径错误等问题的烦恼。

那么该如何设置的呢？

## 设置步骤

1.

**下载PicGo**

可以在这个地址下载最新的PicGo：[https://github.com/Molunerfinn/PicGo/releases](https://github.com/Molunerfinn/PicGo/releases)

官方提供了多个版本，我们直接下载Windows的安装包即可。

![image-20211201154442218](https://ossimg.yzitc.com/2021/12/01/ba26c4a396280.png)

下载后安装，即可以打开了。

2.

**配置阿里云OSS**

我们在右下角找到PicGo的小图标，右键，选择打开详细窗口。

![image-20211201154651481](https://ossimg.yzitc.com/2021/12/01/f3286a16d631d.png)

然后找到图床设置，找到阿里云OSS，填入信息即可。

**这里注意存储区域一栏，只要填入类似下图的一段即可。**

（我自作多情，填了完整的Endpoint地域节点，结果导致一直配置失败，尴尬……）

![1638341070226.png](https://ossimg.yzitc.com/2021/12/01/88ec1c850085a.png)

下方存储路径自定义域名可以不填，也可以根据需要填写。

这样就完成了PicGo.APP配置阿里云OSS的操作。

3.

**Typora内设置**

Typora本身支持PicGo的，所以我们只需要在设置里面简单设置下即可。

打开Typora偏好设置，找到图像，在上传服务那里，选择<kbd>PicGo(app)</kbd>，然后配置好PicGO的程序安装路径，即可完成配置。

![image-20211201164055900](https://ossimg.yzitc.com/2021/12/01/129127b830c8f.png)

现在插入Typora的图片就会自动通过PicGo上传到阿里云OSS了。

## 没有阿里云OSS的情况

那么如果没有阿里云OSS，又该怎么办呢？

其实有更加方便的方法，就是利用图床。



这里要重点推荐下我之前搭建的[圆子图床](https://img.yzitc.com/)了，已开放API接口，可以搭配PicGo，快速完成设置。

### 配置步骤

其他步骤和上面类似，只是在PicGo配置那步，我们不选择阿里云OSS，换另外一个即可。

1.

首先在[圆子图床](https://img.yzitc.com/)注册一个账号，登录用户后台，就可以看到自己的`Token`。

![image-20211201164931535](https://ossimg.yzitc.com/2021/12/01/23f319326ccc7.png)

2.

**PicGo下载插件**

在插件设置里面，搜索Lsky插件，点击安装。

![image-20211201145748926](https://ossimg.yzitc.com/Goimg/image-20211201145748926.png)

然后输入自己的`Token`，并在Url那一栏填入` https://img.yzitc.com/api/upload`，即可完成配置。

是不是超级简单！！

![image-20211201165230061](https://ossimg.yzitc.com/2021/12/01/6d4e533d07f86.png)

之后简单配置下Typora，就可以实现同样的效果了。