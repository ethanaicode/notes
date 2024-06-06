# [笔记07]ThinkPHP6入门到精通：链式查询方法

> 使用教程：[【李炎恢】【ThinkPHP6.x / PHP框架】](https://www.bilibili.com/video/BV12E411y7u8)

[本地链接](E:\BaiduNetdiskDownload\C03资 l 付费购买\0.thinkphp教程+实战\0.Thinkphp6 零基础入门教程-李炎恢tp6.0)

![img](https://pic.shejibiji.com/i/2022/06/06/629dd7216f741.png)

主要包括：where、field、

## where

1、表达式查询，就是`where()`方法的基础查询方式；

```php
public function link01()
    {
        $subQuery = Db::name('users');
        $user = $subQuery->where('id', '<', 6)->select();
        return json($user);
    }
```

2、关联数组查询，通过键值对来数组键值对匹配的查询方式；

```php
$user = $subQuery->where([
'user_registered' => '2020-01-05 02:08:53'
])->select();
```

3、索引数组查询，通过数组里的数组拼装方式来查询；

```php
$user = $subQuery->where([
            ['user_registered', '=', '2020-01-05 02:08:53'] //支持更多模糊匹配
        ])->select();
```

4、将复杂的数组组装后，通过变量传递，将增加可读性；

```php
$map = ['user_registered', '=', '2020-01-05 02:08:53'];
        $user = $subQuery->where([$map])->select();
```

5、字符串形式传递，简单粗暴的查询方式，`whereRaw()`支持复杂字符串格式；

```php
$user = $subQuery->whereRaw('user_registered="2020-01-05 02:08:53"')->select();
```

6、如果SQL查询采用了预处理模式，比如`id=:id`，也能够支持；

```php
$user = $subQuery->whereRaw('id=:id', ['id'=>2])->select();
```

## field

1、使用`field()`方法，可以指定要查询的字段；

```php
public function link02()
    {
        $subQuery = Db::name('users');
        $user = $subQuery->where('id', '<', '10')->field('id,user_registered')->select();
        return json($user);
    }
```

2、使用`field()`方法，给指定的字段设置别名；

```php
$user = $subQuery->where('id', '<', '10')->field(['id', 'user_registered'=>'time'])->select();
// 记得要加中括号[]
```

3、使用`withoutField()`方法中字段，可以屏蔽要想要不显示的字段；

4、在`fieldRaw()`方法里，可以直接给字段设置**MySQL函数**；

5、使用`field(true)`的布尔参数，可以显式的查询获取所有字段，而不是`*`；

6、使用`field()`方法在新增时，验证字段的合法性；

```php
Db::table('user')->field('title,email,content')->insert($data);
```

即表示表单中的合法字段只有`title`,`email`和`content`字段，无论用户通过什么手段更改或者添加了浏览器的提交字段，都会直接屏蔽。因为，其他所有字段我们都不希望由用户提交来决定，你可以通过自动完成功能定义额外需要自动写入的字段。

## alias

使用`alias()`方法，给数据库起一个别名：

`Db::name('user')->alias('a')->select();`
