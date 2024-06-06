# 如何快速删除wordpress文章历史版本，两种简单方法搞定！附删除自动草稿数据方法

<img src="https://www.shejibiji.com/wp-content/uploads/2021/02/60c95-ThumbnailCover_febc162fb107da44.jpg" />

WordPress有很多人性化的设计，比如`自动草稿`和`文章历史版本`。

这两个功能虽好，避免了停电或者断网，写的资料没保存的情况，即使写错了，有历史版本可以回溯也是极好的。

但是！时间一久，你就会发现，数据库会变得非常庞大，特别是`wp-post`表，而且大部分都是重复的。

比如我们站有个页面专门放链接失效补链的，有新的链接我就会放入到这个文章中，结果不知不觉，这个页面就积累了27个版本：

![image-20220509153941254](https://pic.shejibiji.com/i/2022/05/09/6278c53cd56b4.png)<font>短短几天，我就修订了27个版本</font>

这27个版本在数据库中都是单独存放的，等于这一个页面，抵得上正常27个页面所占的空间了。

为了节省数据库空间，提高博客网站速度，我们删除掉这些历史修订版本和草稿是有必要的！

该如何做呢？其实也很简单，这里提供两种方式来批量删除数据库中wordpress历史文章版本和自动保存的草稿。

## 方法一：利用Wordpress自带的代码

WP是提供了操作数据库的方法的，我们只要把下面的代码复制到主题目录下的`function.php`中，再刷新下文章，就会自动删除全部文章修订版本和自动草稿文章。

代码为：

```php
// 删除修订版本所对应的相关联数据和自动草稿中的冗余数据。post_status='auto-draft'对应的是自动草稿数据
$wpdb->query( "DELETE FROM $wpdb->posts WHERE post_status='auto-draft' or post_type = 'revision'" );
```

这段代码不推荐长期放在`function.php`中，定期清理的时候，放入即可。

（你敢保证就没有需要自动保存的时候？）

## 方法二：使用数据库SQL语句命令

> 对数据库进行删除操作前，请一定记得先备份数据库！！！

首先我们进入数据库管理界面，一般是可以通过`phpmyadmin`登录后打开数据库管理系统，然后找到wordpress的数据库，点击`SQL`按钮，就可以输入执行语句命令了。

我们可以通过执行下面这段语句，就可以快速找出所有文章历史修订版本和草稿：

```sql
SELECT * FROM wp_posts WHERE post_type = 'revision' or post_status = 'auto-draft';
```

效果如图（界面可能会不同）：

![image-20220509160108608](https://pic.shejibiji.com/i/2022/05/09/6278ca4425aea.png)

可以看到已经发现了2495条记录！

事实上我总共也才只有6000多数据，这个就快占了一半了！

**接下来我们就可以开始动刀子了！**

首先执行下面这段语句命令，可以删除掉所有历史文章修订版本：

```sql
DELETE FROM wp_posts WHERE post_type = 'revision';
```

下面这段是删除所有自动草稿：

```sql
DELETE FROM wp_posts WHERE post_status = 'auto-draft';
```

这样就删除了所有wordpress历史文章版本和自动保存的草稿！

但是在这些历史文章版本和草稿中，通常还有很多相关联的数据，这个一般存在`post_postmeta`中，我们也可以一并删除，执行下面这段sql命令即可：

```sql
/* 下面这一段可以同时完成上面两段的工作 */
DELETE a,b,c
FROM wp_posts a
LEFT JOIN wp_term_relationships b ON (a.ID = b.object_id)
LEFT JOIN wp_postmeta c ON (a.ID = c.post_id)
WHERE a.post_status='auto-draft' or a.post_type = 'revision';
```

这样就可以完成所有清理工作！



其实还可以用插件的方法，但是这种一次性的工作大可不必这么麻烦，推荐还是SQL语句命令，最方便！