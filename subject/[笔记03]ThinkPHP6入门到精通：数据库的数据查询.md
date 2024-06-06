# [笔记03]ThinkPHP6入门到精通：数据库的数据查询

> 使用教程：[【李炎恢】【ThinkPHP6.x / PHP框架】](https://www.bilibili.com/video/BV12E411y7u8)

[本地链接](E:\BaiduNetdiskDownload\哔哩哔哩\小虫师兄\ThinkPHP6入门到精通)

![img](https://pic.shejibiji.com/i/2022/06/06/629dd7216f741.png)

## 数据库的查询

### 一、单数据查询

1、`Db::table()`中**table**必须指定完整数据表；

2、如果希望只查询一条数据，可以使用`find()`方法，需置顶where条件；

```php
$user = Db::table('tp_users')->where('id', 2)->find();
return json($user);
//返回数组，需要json格式化，不然无法显示
```

3、`Db::getLastSql()`方法，可以得到最近一条SQL查询的原生语句；

4、没有查询到任何值，则返回null；

5、使用`findOrFail()`方法同样可以查询到一条数据，在没有数据时抛出一个异常；

```php
$user = Db::table('tp_users')->where('id', 3)->findOrFail();
return json($user);
//会抛出异常，而不是返回null
```

6、使用`findOrEmpty()`方法也可以查询到一条数据，但在没有数据时返回一个空数据。

### 二、数据集查询

1、想要获取多列数据，可以使用`select()`方法；

2、默认返回空数组，使用`selectOrFail()`抛出异常；

3、在`select()`方法后再使用`toArray()`方法，可以将数据集对象转化为数组；

**默认是数据集：**

![2022-07-06_15-51-55](https://pic.shejibiji.com/i/2022/07/06/62c53f2083252.jpg)

代码链式方法中加入`toArray()`，改为这样：

![2022-07-06_15-53-35](https://pic.shejibiji.com/i/2022/07/06/62c53fada5951.jpg)

**输出后结果为数组：**

![2022-07-06_15-52-32](https://pic.shejibiji.com/i/2022/07/06/62c53f4e2e039.jpg)

4、当在数据库配置文件中设置了前缀，那么我们可以使用`name()`方法忽略前缀：（⭐推荐这种）

```php
$user = Db::name('users')->select(); 
//等同于之前的$user = Db::table('tp_users')->select()
return json($user);
```

### 三、其它查询

1、通过`value()`方法，可以查询指定字段的值（单个），没有数据返回`null`；

```php
$user = Db::name('users')->where('id', 1)->value('user_login'); 
//不加where筛选，会显示最后一个值
return json($user);
```

2、通过`column()`方法，可以查询指定列的值（多个），没有数据返回`null`；

3、可以置顶id作为列值的索引；

```php
$user = Db::name('users')->column('user_login', 'id');
//id记得要单引号括起来，不然会报错
```

**如果处理的数据量巨大，成百上千那种，一次性读取有可能导致内存开销过大。**

我们可以使用两种方法解决这个问题：

4、`chunk()`方法分批处理数据；

```php
        Db::name('users')->chunk(1, function($users){
            foreach($users as $user){
                dump($user);
            }
        });
        // 1表示每次处理1条数据，可以设定大一些
```

5、`cursor()`游标查询功能，利用了PHP生成器特性，每次查询只读一行，然后再读取时，自动定位到下一行继续读取。（⭐推荐这种！处理非常快！）

例：

```php
        $cursor = Db::name('users')->cursor();
        foreach($cursor as $user){
            dump($user);
        }
```

## 数据库的链式查询

### 查询规则

1、前面课程中我们通过指向符号“->”多词连续调用方法称为：链式查询；

2、当`Db::name('user')`时，返回查询对象（Query），即可连缀数据库对应的方法；

3、而每次执行一次数据库查询方法时，比如`where()`，还将返回查询对象（Query）;

4、**只要还是数据库对象，那么就可以一直使用指向符号进行链式查询；**

5、再利用find()、select()等方法返回数组（Array）或者数据集对象（Collection）；

6、而find()和select()是结果查询方法（放在最后），并不是链式查询方法；

7、除了查询方法可以使用链式连贯操作，CURD操作也可以使用。

> 通俗来说就是可以使用多个链式，来增加条件，然后使用结果查询方法返回想要的数据。

更多规则还可以在官方手册继续学习：

[ThinkPHP6.0完全开发手册](https://www.kancloud.cn/manual/thinkphp6_0)

![2022-07-06_19-33-13](https://pic.shejibiji.com/i/2022/07/06/62c5731300fa2.jpg)

### 更多查询

1、如果多次使用数据库查询，那么每次静态创建都会生成一个实例，造成浪费。

我们可以把对象实例保存下来，再进行反复调用即可：

```php
$userQuery = Db::name('user');
$dataSelect = $userQuery->order('id', 'desc')->select();
```

2、当同一个对象实例第二次查询后，会保留第一次查询的值。

我们可以使用removeOption()方法，可以清理掉上一次查询保留的值：

```php
$data1 = $userQuery->order('id', 'desc')->select(); //以id倒序排序数据
$data2 = $userQuery->select(); //我们重新赋值，这次没有倒序
return json($data2); //但是结果还是倒序，这就是因为第一次查询被保留的结果
// 我们修改程序成下面这个即可解决问题
$data1 = $userQuery->order('id', 'desc')->select();
$data2 = $userQuery->removeOption('order')->select(); //无脑清除即可
return json($data2);
```

![2022-07-06_19-57-04](https://pic.shejibiji.com/i/2022/07/06/62c5789575d00.jpg)
