# GD Library Error错误，WP主题无法显示缩略图的解决方法

今天在本地测试WordPress主题，发现文章的缩略图都无法显示：

![image-20220329180350604](https://ossimg.yzitc.com/2022/03/29/c30b5241c7f38.png)

复制了下图片地址，发现是引入了`timthumb.php`，打开地址显示错误：

![image-20220329180323527](https://ossimg.yzitc.com/2022/03/29/27e1e14adf7c9.png)

重点是这句：

`GD Library Error: imagecreatetruecolor does not exist - please contact your webhost and ask them to install the GD library`

翻译过来大概知道是因为PHP的GD库没安装导致的。

因为我是在本地使用xampp搭建的php环境，推测是xampp没有打开GD2绘图扩展。

我们打开php的配置文件，位置在`php/php.ini`

在最后加上一句：

```
;GD2库
extension=php_gd.dll
```

然后重启下Apache。

刷新下网页，缩略图都成功打开了。

![image-20220329181248170](https://ossimg.yzitc.com/2022/03/29/b113ef89dc10f.png)



另外使用这个`timthumb.php`的，如果需要添加外链，格式应该是类似这样的：

```php+HTML
if(! isset($ALLOWED_SITES)){
    $ALLOWED_SITES = array (
	'shejibiji.com',
	);
}
```