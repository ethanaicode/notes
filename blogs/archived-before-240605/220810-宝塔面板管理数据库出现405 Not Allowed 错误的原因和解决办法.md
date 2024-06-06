# 宝塔面板管理数据库出现405 Not Allowed 错误的原因和解决办法

![2022-08-10_10-55-20](https://pic.shejibiji.com/i/2022/08/10/62f31e1e350c6.jpg)

今天在测试时，通过宝塔面板点击数据库管理提示“405 Not Allowed”。

这个在我的建站过程中还是第一次遇见，到底是哪里出现问题了呢。

## 什么是405 Not Allowed

状态码 405 Not Allowed 表明服务器禁止了使用当前 HTTP 方法的请求。

这个解释有点语焉不详，不过实际上原因就是PHP版本和phpmyadmin版本有冲突，找到了原因，自然就有了解决办法。

## 405 not allowed 解决办法

宝塔面板出现访问phpMyAdmin报405 not allowed错误通常是因为php和phpmyadmin版本不对导致的，我们只要把现有的phpmyadmin卸载掉，再重新安装一个符合要求的版本即可。

在软件管理 – 搜索phpmyadmin – 卸载 – 重新安装一个新版本。

![2022-08-10_10-52-53](https://pic.shejibiji.com/i/2022/08/10/62f31d8b23649.jpg)

## phpMyAdmin与PHP版本匹配说明

PHP 5.2版本，可安装phpMyAdmin 4.0；

PHP 5.3到7.0版本，可安装phpMyAdmin 4.4；

PHP 5.5到7.3版本，可安装phpMyAdmin 4.9；

PHP 7.4到8.0版本，可安装phpMyAdmin 5.0。