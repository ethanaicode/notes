# 解决多个WordPress站点使用Redis对象缓存插件数据冲突的问题

![Redis对象缓存插件](https://www.shejibiji.com/wp-content/uploads/2021/03/43b6f-ThumbnailCover_.jpg)

今天悲剧了，一个服务器两个wordpress网站，都使用了Redis缓存，结果第二个网站一启用Redis，整个站就没了，打开都是第一个站的数据，该怎么办呢？

## 问题解析

服务器安装Redis扩展后，默认创建16个Redis数据库（序号0-15），WordPress插件`Redis Object Cache`中没有选择指定数据库序号的选项，只能使用Redis的第一个库。

一台服务器如果有多个WordPress站点并且都安装使用Redis对象缓存插件，就会导致其中一个站点的数据是另一个站点的数据。

## 解决办法

一、打开第**二**个站点的`/wp-content/plugins/redis-cache/includes/object-cache.php`

![R_22-11-27-15-05-35_80](https://pic.shejibiji.com/i/2022/11/27/63830c4a3ed10.jpg)

二、搜索：database，大概在第617行，把“0”改成1-15的任意数。

![R_22-11-27-15-06-21_80](https://pic.shejibiji.com/i/2022/11/27/63830c7629f09.jpg)

**三、如果Redis数据库中已有冲突数据无法进入后台。**

可以进入服务器目录，把`wp-content`下面的这个缓存文件`object-cache.php`删掉，就可以恢复访问后台了。

![R_22-11-27-15-07-59_80](https://pic.shejibiji.com/i/2022/11/27/63830cd9394d9.jpg)

现在再去启用插件就不会出问题了。

![R_22-11-27-15-11-52_80](https://pic.shejibiji.com/i/2022/11/27/63830dd755368.jpg)
