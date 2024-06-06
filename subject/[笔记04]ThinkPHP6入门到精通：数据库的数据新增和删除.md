# [笔记04]ThinkPHP6入门到精通：数据库的数据新增和删除

> 使用教程：[【李炎恢】【ThinkPHP6.x / PHP框架】](https://www.bilibili.com/video/BV12E411y7u8)

[本地链接](E:\BaiduNetdiskDownload\哔哩哔哩\小虫师兄\ThinkPHP6入门到精通)

![img](https://pic.shejibiji.com/i/2022/06/06/629dd7216f741.png)

## 数据库的数据新增

### 单数据新增

1、使用`insert()`方法可以向数据表添加一条数据，更多的字段采用默认；

2、如果新增成功，`insert()`返回一个1值；

3、如果里添加一个不存在的字段数据，会抛出一个异常Exception；

*数据表中不存在的字段*

4、如果你强行新增抛弃不存在的字段数据，则使用`strick(false)`方法，忽略异常；

5、如果我们采用的数据库是mysql，可以支持replace写入；

6、insert和replace写入的区别，前者表示表中存在主键相同则报错，后者则修改；

例如：

```php
    public function insert()
    {   
        $data2 = [
            'user_login' => 'user4',
            'user_pass' => '123456',
            'user_nicename' => 'user5_nice',
            'user_email' => 'user5@qq.com',
            'user_registered' => '2022-06-04 15:25:38',
            'display_name' => 'user5_nice'
        ];
        $userQuery = Db::name('user');
        $data1 = $userQuery->replace()->insert($data2);
        return Db::getLastSql();
    }
```

7、使用`insertGetId()`方法，可以在新增成功后返回当前数据ID。

#### save()新增

1、`save()`方法是一个通用方法，可以自行判断是新增还是修改（更新）数据；

2、`save()`方法判断是否为新增或修改的依据为：是否存在主键，不存在即新增。

### 批量数据新增

1、使用`insertAll()`方法，可以批量新增数据，但要保持数据结构一致；

*使用方法就是上例中，把inser换为insertAll*

2、批量新增也支持`replace()`方法，添加后改变成`replace into`；

## 数据库的数据修改

1、使用`update()`方法来修改数据，修改成功返回影响行数，没有修改返回0；

2、如果修改数据包含了主键信息，比如id，那么可以省略掉`where`条件；

3、如果想让一些字段修改时执行SQL函数操作，可以使用`exp()`方法实现；

4、如果要自增/自减某个字段，可以使用`inc/dec`方法，并支持自定义步长；

例如：

```php
// 两个例子对应上面的3&4点
public function update()
    {
        $userQuery = Db::name('user');
        return $userQuery->where('ID', 3)
                         ->exp('user_email', 'UPPER(user_email)') //字母大写
                         ->update();
    
        $userQuery = Db::name('user');
        return $userQuery->where('ID', 3)
            ->inc('user_status', 2)
            ->update();
    }
```

5、一个更加简单粗暴灵活的方式，使用`::raw()`方法实现3，4点的内容；

例如：

```php
public function update()
    {
        $userQuery = Db::name('user');
        return $userQuery->where('ID', 4)
            ->update([
                'user_email' => Db::raw('UPPER(user_email)'),
                'user_status' => Db::raw('user_status - 2')
            ]);
    }
```

6、使用`save()`方法进行修改数据，这里必须指定主键才能实现修改功能。

例如：

```php
public function update()
    {
        $userQuery = Db::name('user');
        return $userQuery->where('ID', 5)
                         ->save(['user_login' => 'user5']);
    }
```

## 数据库的数据删除

 1、可以根据主键直接删除，删除成功返回影响行数，否则为0；

2、根据主键，还可以删除多条记录；

例如：

```php
public function del()
    {
        $userQuery = Db::name('user');
        return $userQuery->delete([7, 8, 9]);
    }
// 只删除一条的话，只要填入数字，无需数组形式
```

3、正常情况下，通过`where()`方法来删除；

4、通过`true`参数删除数据表所有数据，谨慎操作！

例如：

```php
public function del()
    {
        return Db::name('user2')->delete(true);
    }
```

