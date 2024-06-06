# [笔记06]ThinkPHP6入门到精通：数据库的聚合、原生及子查询

> 使用教程：[【李炎恢】【ThinkPHP6.x / PHP框架】](https://www.bilibili.com/video/BV12E411y7u8)

[本地链接](E:\BaiduNetdiskDownload\哔哩哔哩\小虫师兄\ThinkPHP6入门到精通)

![img](https://pic.shejibiji.com/i/2022/06/06/629dd7216f741.png)

### 聚合查询

系统提供的一系列方法来方便查询整合数据。

1、使用`count()`方法，可以求出说查询数据的数量；

2、`count()`可设置指定id，比如有空值（Null）的uid，不会计算数量；

> 大概意思就是会排除掉指定id为空的数据

3、使用`max()`方法，求出所查询数据字段的最大值；

4、使用`max()`方法，求出的值不是数值，则通过第二参数强制转换；

（意义不大，可忽略）

`Db::name('user')->max('price', false);`

5、使用`min()`方法，求出所查询数据字段的最小值，也可以强制转换；

6、使用`avg()`方法，求出所查询数据字段的平均值；

7、使用`sum()`方法，求出所查询数据字段的总和；

### 子查询

1、使用`fetchSql()`方法，可以设置不执行SQL，而返回SQL语句，默认true；

> 用这个就可以实现快速控制返回的是SQL语句还是查询结果，下面的也是同样的效果

2、使用`buildSql()`方法，也是返回SQL语句，不需要再执行`select()`，且有括号；

⭐拼接查询要用到

```php
public function poly()
    {
        $userQuery = Db::name('user');
        $user = $userQuery->buildSql();
        return json($user);
    }
//>>> 运行结果
//"( SELECT * FROM `tp_user` )"

//如果用1的方法，结果会略有区别
//>>> 运行结果
//"SELECT * FROM `tp_user`"
```

3、可以结合以上方法，实现复杂的子查询（拼接SQL语句）；

```php
public function poly()
    {
        $subQuery = Db::name('users')->field('id')->where('user_login', 'cshengs')->buildSql();
        $result = Db::name('usermeta')->where('user_id', 'exp', 'IN' . $subQuery)->select();
        return json($result);
    }
//数据表来自wordpress，通过这个就可以查看所有与用户名cshengs相关的用户配置资料
```

4、推荐使用闭包的方式，执行子查询。

上面的例子就可以改成：

```php
public function poly()
    {
        $result = Db::name('usermeta')->where('user_id', 'in', function($query){
            $query->name('users')->field('id')->where('user_login', 'cshengs');
        })->select();
        return json($result);
    }
// $query相当于Db::
```

### 原生查询

> 这个就是直接执行你写的SQL语句

1、可以使用`query()`方法，进行原生SQL查询，适用于读取操作，SQL错误返回false；

例如：`Db::query('select * from wp_user');`

2、使用`execute`方法，进行原生SQL更新写入等，SQL错误返回false；

