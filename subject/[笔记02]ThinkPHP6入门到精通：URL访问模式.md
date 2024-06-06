# [笔记02]ThinkPHP6入门到精通：URL访问模式

> 使用教程：[【李炎恢】【ThinkPHP6.x / PHP框架】](https://www.bilibili.com/video/BV12E411y7u8)

[本地链接](E:\BaiduNetdiskDownload\C03资 l 付费购买\0.thinkphp教程+实战\0.Thinkphp6 零基础入门教程-李炎恢tp6.0)

![img](https://pic.shejibiji.com/i/2022/06/06/629dd7216f741.png)

### URL解析

1、ThinkPHP框架非常多的操作都是通过URL来实现的；

2、多应用：`http://serverName/index.php/应用/控制器/操作/参数/值...`

3、单应用：`http://serverName/index.php/控制器/操作/参数/值...`

4、由于TP6.0默认是但应用模式，多应用需要作为扩展安装，避免混乱展示搁置；

5、index.php这个文件，是根目录下public/下的index.php(入口文件)；

6、**控制器：**app目录下有一个controller控制器目录下的Test.php（控制器），类名也必须是`class Test`，否则错误；

7、操作就是控制器类里面的方法，比如：`index`（默认面写）或hello（必写）；

例如：

![2022-07-15_17-40-07](https://pic.shejibiji.com/i/2022/07/15/62d135fbb8a6d.jpg)

就可以通过地址：

`http://你的域名/test`访问，并返回`index`

访问：`http://你的域名/test/hello/value/shejibiji`

返回：hello shejibiji

![2022-07-15_17-44-51](https://pic.shejibiji.com/i/2022/07/15/62d1371dc0d19.jpg)

**上面的操作省略掉了index.php**

如果不行，可能是因为服务器没有开启重写。

我们可以打开web服务器配置文件，开启`mod_rewrite.so`模块，并将`AllowOverride None`的`None`改为`All`皆可。
