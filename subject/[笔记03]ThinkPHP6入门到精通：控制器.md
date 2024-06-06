# [笔记03]ThinkPHP6入门到精通：控制器

> 使用教程：[【李炎恢】【ThinkPHP6.x / PHP框架】](https://www.bilibili.com/video/BV12E411y7u8)

[本地链接](E:\BaiduNetdiskDownload\哔哩哔哩\小虫师兄\ThinkPHP6入门到精通)

![img](https://pic.shejibiji.com/i/2022/06/06/629dd7216f741.png)

### 控制器的定义

1、控制器，即controller，控制器文件存放在controller目录下；

2、如果想改变控制器默认目录，可以在`config`下`route.php`配置；

3、类名和文件名大小写要保持一致，并采用驼峰式（首字母大写）

```php
namespace app\controller;
class Test{...}
```

4、从上面两段代码得知Test.php的实际位置为：`app\controller\Test.php`

5、在Test类创建两个方法index（默认）和hello，访问URL如下：

```php
http://localhost/test
http://localhost/test/hello
```

6、如果是双字母组合，比如`class HelloWorld`，访问URL如下：

```php
http://localhost/HelloWorld/hello
http://localhost/Hello_World/hello
```

### 渲染输出

1、ThinkPHP直接采用return返回的方式直接输出；

2、可以采用json函数，输出json；

3、不推荐使用包括`die`、`exit`在内的中断代码，推荐使用助手函数`halt()`。

`halt('中断测试');`

例如：

```php
public function arrayOut()
    {
        $data = ['a'=>1, 'b'=>2, 'c'=>3];
        halt('在这里暂停一下');
        return json($data);
    }
```
