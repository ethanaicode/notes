# [笔记02]ThinkPHP6入门到精通：连接数据库

> 使用教程：[【李炎恢】【ThinkPHP6.x / PHP框架】](https://www.bilibili.com/video/BV12E411y7u8)

[本地链接](E:\BaiduNetdiskDownload\哔哩哔哩\小虫师兄\ThinkPHP6入门到精通)

![img](https://pic.shejibiji.com/i/2022/06/06/629dd7216f741.png)

## 连接数据库

1. ThinkPHP 采用内置抽象层将不同的数据库操作进行封装处理；
2. 数据抽象层基与 **PDO** 模式，无须针对不同的数据库编写相应的代码；
3. 使用数据库的第一步，就是连接你的数据库；
4. 在根目录的 config 下的 database.php 可以设置数据库连接信息；
5. 大部分系统已经给了默认值，你只需要修改和填写需要的值即可；
6. ⭐ 本地测试，会优先采用`.env`的配置信息，我们和`database`配置对应上即可；
7. 可以通过删除修改`.env`的配置，或删除`.env`来验证database的执行优先级；
8. 在 database.php 配置中，default 表示设置默认的数据库连接；
9. connections 配置数据库连接信息，可以是多个数据库，便于切换；
10. 默认的数据库连接名称为：‘mysql’，再复制一组数据库连接信息：‘demo’切换；
11. 创建一个用于测试数据库连接的控制器：‘DataTest.php’;

### 测试数据库连接（对应上面5&6点）

我们在`app/controller`下新建一个`DataTest.php`，然后在其中输入以下代码，然后浏览器输入：`http://域名/datatest`，即可访问到数据库数据信息。

```php
<?php
namespace app\controller;

use think\facade\Db;

class DataTest{
    public function index()
    {
        $user = Db::table('tp_users')->select();
        return json($user);
    }
}
```

![2022-07-05_18-43-31](https://pic.shejibiji.com/i/2022/07/05/62c415d92f897.jpg)

### 多个数据库（对应上面第9点）

我们可以在`database.php`信息里面，放入多个数据库连接信息，比如这样：

![2022-07-05_19-00-26](https://pic.shejibiji.com/i/2022/07/05/62c419d7d7ff0.jpg)

然后我们在测试的文件中加一个function，名字为demo：

![2022-07-05_19-02-28](https://pic.shejibiji.com/i/2022/07/05/62c41a5f2fd4d.jpg)

浏览器输入：`http://域名/datatest/demo`，就可以连接到新的数据库了。

## 初探模型

模型就是和数据库直接打交道的一个类。

1、在app目录下，创建一个`model`目录，用于创建`User.php`的模型类：

```php
namespace app\model;
use think\Model;

class User extends Model
{
    protected $connection = 'mysql';
}
```

2、User继承模型基类，即可实现数据调用。

3、受保护的字段$connection，这是切换到demo数据库；

4、控制器端的调用方式如下：

```php
public function getUser()
{
    $user = User::select();
    return $user;
}
```

（测试没有成功，之后看学完模型是否可以解决）

具体原理后面会详解。
