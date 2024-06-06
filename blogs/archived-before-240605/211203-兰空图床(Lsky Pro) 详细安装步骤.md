# 兰空图床(Lsky Pro) 详细安装步骤

<blockquote>
教程中的图床：圆子图床（<a href="http://img.yzitc.com/">https://www.yzitc.com</a>）免费开放给网友使用。
</blockquote>

之前一直用的是别人的图床，但最近不知道为什么接口突然无法使用了。

于是决定自己搭建一个图床，对比了多个图床程序后，最终选择了<a href="https://www.lsky.pro/">兰空图床(Lsky Pro)</a>

### 📌 优点主要有：
 - 支持第三方云储存，本地、阿里云 OSS、腾讯云 COS、七牛云、又拍云、FTP
  - 多图上传、拖拽上传、粘贴上传、上传预览、全屏预览、页面响应式布局
  - 简洁的图片管理功能，支持鼠标右键、单选多选、重命名等操作
  - 全局配置用户初始剩余储存空间、设置指定用户剩余储存空间
  - 一键复制图片外链、二维码扫描链接、图片鉴黄功能
  - 设置上传文件、文件夹路径命名规则、文件夹分类功能
  - 接口上传、图片软删除
  - OTA 在线升级系统
  - (Dark)暗黑主题
  - IP 封禁功能(支持通配符)
 -  自定义链接参数
 -  单用户模式
  - 图片广场(画廊)
  - 上传图片自动增加水印(支持图片或文字)

<h3>🛠 安装要求</h3>
<ul>
<li>PHP 版本 ≥ 5.6</li>
<li>mysql 版本 ≥ 5.5</li>
<li>PDO 拓展</li>
<li>ZipArchive 支持</li>
<li>fileinfo 拓展</li>
<li>curl 拓展</li>
</ul>
注：如果使用 FTP 功能，需要开启 PHP 的 FTP 拓展

<h2>那么具体怎么安装呢？</h2>

<strong>安装步骤：</strong>
我用的是宝塔面板进行安装的，接下来的步骤也都是用宝塔进行的。

1.

**首先安装必需的拓展**

打开PHP扩展管理找到PHP，点击设置，安装fileinfo拓展。
<a href="https://www.laa.one/image/Z6Fv"><img src="https://www.laa.one/images/2021/11/22/image8d08cf1705414f78.md.png" alt="image8d08cf1705414f78.md.png" border="0"></a>

**安装拓展后记得重启php，不然无法成功使用新的拓展！！**

2.

**新建网站，上传程序**

然后在宝塔面板左边，找到网站，点击添加站点。
设置站点目录，并新建数据库。
<img src="https://www.shejibiji.com/wp-content/uploads/2020/05/图002-1.jpg" alt="" class="alignnone size-full wp-image-1987" />

然后在宝塔面板左边，找到文件，找到新建的站点目录，上传兰空图床(Lsky Pro)压缩包到网站目录，并解压。

<a href="https://www.laa.one/image/Zitf"><img src="https://www.laa.one/images/2021/11/22/imaged336d6ee55e392cd.md.png" alt="imaged336d6ee55e392cd.md.png" border="0"></a>

3.

**设置运行目录为pubilic**

在网站设置中，设置网站目录>>运行目录为public。

<a href="https://www.laa.one/image/ZOXi"><img src="https://www.laa.one/images/2021/11/22/image7c7266c4740ef0c0.md.png" alt="image7c7266c4740ef0c0.md.png" border="0"></a>

4.

**设置伪静态**

Nginx：

````
location / {
    if (!-e $request_filename) {
    	rewrite ^(.*)$ /index.php?s=$1 last; break;
    }
}
````

Apache:
Apache 直接使用 .htaccess 即可

5.

**输入域名，成功访问**

完成搭建，现在输入域名即可成功访问兰空图床(Lsky Pro)了。

未安装自动跳转至安装页面，根据页面提示安装即可。

<a href="https://www.laa.one/image/ZuLh"><img src="https://www.laa.one/images/2021/11/22/imagecbb75befde006d90.md.png" alt="imagecbb75befde006d90.md.png" border="0"></a>

安装完成以后请设置 runtime 目录 0755 权限，如果你使用本地存储，public 目录也需要设置为 0755 权限
