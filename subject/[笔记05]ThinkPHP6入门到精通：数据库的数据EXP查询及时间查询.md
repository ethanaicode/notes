# [笔记05]ThinkPHP6入门到精通：数据库的数据EXP查询及时间查询

> 使用教程：[【李炎恢】【ThinkPHP6.x / PHP框架】](https://www.bilibili.com/video/BV12E411y7u8)

[本地链接](E:\BaiduNetdiskDownload\哔哩哔哩\小虫师兄\ThinkPHP6入门到精通)

![img](https://pic.shejibiji.com/i/2022/06/06/629dd7216f741.png)

查询方式主要有：比较查询、区间查询、EXP查询等。

## 数据查询

### 比较查询

1、查询表达式支持大部分常用的SQL语句，语句格式如下：

```php
where('字段名','查询表达式','查询条件');
```

在查询数据进行筛选时，我们采用where()方法，比如id=80；

2、使用<>、>、<、>=、<=可以筛选出格中适合比较值的数据列表；

```php
public function query()
    {
        $userQuery = Db::name('user');
        return $userQuery->where('id', '<>', 2)->select();
    }
// '<>'这个符号表示不等于
```

### 区间(模糊)查询

1、使用`like`表达式进行模糊查询；

2、`like`表达式还可以支持数组传递进行模糊查询；

```php
public function query()
    {
        $userQuery = Db::name('user');
        return $userQuery->where('user_email', 'like', ['svip2011%', 'svip2012%'], 'or')->select();
    }
```

3、`like`表达式具有两个快捷方式`whereLike()`和`whereNoLike()`；

4、`between`表达式具有两个快捷方式`whereBetween()`和`whereNotBetween()`；

5、`in`表达式具有两个快捷方式`whereIn()`和`whereNotIn()`；

6、`null`表达式具有两个快捷方式`whereNull()`和`whereNotNull()`； 

```php
Db::name('user')->where('uid', 'null')->select();
//相当于
Db::name('user')->whereNotNull('uid')->select();
```

### EXP查询

1、使用`exp`可以自定义字段后的SQL语句；

*也就是意味着你可以自己拼装后面的SQL语句*

```php
public function query()
    {
        $userQuery = Db::name('user');
        $data = $userQuery->where('id', 'exp', 'IN(1,3,4)')->select();
        return json($data);
    }
//也可以直接whereExp()快捷方式，就不用再条件里面写'exp'了
```

## 时间查询

### 传统方式

1、可以使用`>, <, >=, <=`或者`between`来筛选匹配时间的数据；

例如：

```php
public function time()
    {
        $userQuery = Db::name('user');
        $user = $userQuery->where('user_registered', 'between', ['2018-01-01', '2021-12-30'])->select();
        return json($user);
    }
```

*`not between`即为`between`的方向操作*

### 快捷方式

1、时间查询的快捷方式为`whereTime()`，直接使用`>, <, >=, <=`；

2、快捷方式也可以使用`between`和`not between`；

例如：

```php
public function time()
    {
        $userQuery = Db::name('user');
        $user = $userQuery->whereTime('user_registered', 'between', ['2018-01-01', '2021-12-30'])->select();
        return json($user);
    }
```

3、还有一种快捷方式为`whereBetweenTime()`和`whereNotBetweenTime()`；

**这个就不用以数组的形式传入开始和结束时间，直接以字符串传入即可。**

4、默认的条件为大于`>`，可以省略。

### 固定查询

1、使用`whereYear`查询今年的数据、去年的数据和某一年的数据：

```php
public function time()
    {
        $userQuery = Db::name('user');
//        $user = $userQuery->whereYear('user_registered')->select();
//        $user = $userQuery->whereYear('user_registered', 'last year')->select();
        $user = $userQuery->whereYear('user_registered', '2019')->select();
        return json($user);
    }
```

2、使用`whereMonth`查询当月的数据、上月的数据和某一个月的数据；

3、使用`whereDay`查询今天的数据、昨天的数据和某一天的数据。

### 其它查询

1、查询指定时间的数据，比如两小时内的：

```php
Db::name('user')->whereTime('create_time', '-2 hours')->select()
```

2、查询两个时间字段时间有效期的数据，比如会员开始到结束的期间；

```php
Db::name('user')->whereBetweenTimeField('start_time', 'end_time')->select()
```

