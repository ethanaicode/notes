# wampServer 安装 Redis 扩展

![1662099770546.png](https://img.shejibiji.com/2022/09/02/6311a13f54cf8.png)

最近在自己学习开发，涉及到验证码的存储问题，目前解决方案推荐的是用Redis，于是就想在本地搭建的环境中安装这个扩展。

那么具体怎么安装呢？

> **REmote DIctionary Server(Redis)** 是一个由Salvatore Sanfilippo写的key-value存储系统。
>
> Redis是一个开源的使用ANSI C语言编写、遵守BSD协议、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。
>
> 它通常被称为数据结构服务器，因为值（value）可以是 字符串(String)，哈希(Map)， 列表(list)， 集合(sets) 和 有序集合(sorted sets)等类型。

### 一、查看PHP版本信息

使用 phpinfo() 函数查看 PHP 的版本信息（用于选择扩展包）

![2022-09-02_13-57-16](https://pic.shejibiji.com/i/2022/09/02/63119b4709cdc.jpg)<font>↑ PHP版本 7.4，编译器版本 Visual C++ 2017，CPU架构 x64</font>

### 二、根据版本选择扩展包

> 如果以前没装过Redis，还需要先安装Redis，并启动服务端。
>
> Redis下载地址：https://github.com/tporadowski/redis/releases

php_redis.dll 下载地址：

[https://windows.php.net/downloads/pecl/snaps/redis/](https://windows.php.net/downloads/pecl/snaps/redis/)

php_igbinary.dll 下载地址：

[https://windows.php.net/downloads/pecl/releases/igbinary/](https://windows.php.net/downloads/pecl/releases/igbinary/)

可以根据自己的配置，找到适合的对应版本！

![2022-09-02_14-45-30](https://pic.shejibiji.com/i/2022/09/02/6311a69162cb4.jpg)

![2022-09-02_14-43-58](https://pic.shejibiji.com/i/2022/09/02/6311a636f1e69.jpg)<font>↑ redis和igbinary都有标注需要的php版本（看压缩包名)</font>

### 三、安装Redis扩展

解压 zip 文件，只保留 **php_redis.dll** 和 **php_igbinary.dll** 文件

![img](https://pic.shejibiji.com/i/2022/09/02/631196d727945.png)

将这两个文件拷贝至 wamp64 安装目录中（wamp64\bin\php\php7.x.x\ext\）

![2022-09-02_14-48-08](https://pic.shejibiji.com/i/2022/09/02/6311a72f0fb48.jpg)

### 四、修改 php.ini 配置

![img](https://pic.shejibiji.com/i/2022/09/02/631196dcc1cad.png)<font>↑ wampserver 并不会读取 php 目录下的 php.ini，而是调用的 /apache/bin 目录下的 php.ini 文件</font>

修改 php.ini 在文件中添加：

```
[redis]
; php_redis
extension=php_igbinary.dll
extension=php_redis.dll
```

![img](https://pic.shejibiji.com/i/2022/09/02/631196e2cfbdb.png)

注意：php_igbinary.dll 一定要位于 php_redis.dll 之前

### 五、查看安装结果

**重启 wampserver（restart all server）**，使用 phpinfo() 函数查看扩展是否安装

![2022-09-02_14-51-06](https://pic.shejibiji.com/i/2022/09/02/6311a7e339109.jpg)<font>↑ 能看到redis字样表示安装成功</font>

新建一个 php 文件测试 redis 扩展是否可用

```
<?php

$redis = new Redis();
$redis->connect('127.0.0.1', 6379);
echo '<h3>Redis Server Connect Success</h3>';
$redis->set('test', 'Hello Redis');
echo $redis->get('test');
```

![img](https://pic.shejibiji.com/i/2022/09/02/631197022683b.png)<font>↑ wampserver redis 扩展安装成功</font>

## 更多操作

### 错误解决

我按照教程进行了测试，结果报**Uncaught RedisException**错误。

![2022-09-02_15-16-46](https://pic.shejibiji.com/i/2022/09/02/6311adf6060f4.jpg)

看到这个我突然很好奇，我都没有安装Redis，这就可以使用啦，而且还用到端口，似乎不科学。

所以我去官网下载了Redis最新压缩包，解压后双击redis-server.exe启动服务端。

刷新网页即可成功显示测试的内容了。

Redis下载地址：https://github.com/tporadowski/redis/releases

### 关闭Redis服务

打开window命令行，运行：`redis-server &`

如果需要更换redis端口，运行：`redis-server -port port number of your redis &`

### 卸载Redis服务

打开window命令行，运行：`redis-server -service-uninstall`

## Redis 数据库可视化工具推荐

[![img](https://pic.shejibiji.com/i/2022/09/02/631196ed6294d.png)](https://redisdesktop.com/)

