# PHP基础极速入门笔记

教程链接：https://www.bilibili.com/video/BV1Vp4y1e7pz

https://huke88.com/course/31941.html?referrer=huke88.com

https://www.51zxw.net/Show.aspx?cid=865&id=97657

**推荐软件：**

PhpStorm

Navicat （用于编辑数据库和表）



推荐学习：

三大框架：vue.js/Angular/React

[前端知识图谱+B站视频整合](https://gitee.com/jishupang/web_atlas)

## 基础知识

### 一、‘./ ’、‘../’和‘/’的区别？

`./` 表示当前目录

`../` 表示上级目录

`/`表示根目录



### 二、注册表单常见的语句概念

#### 1.placeholder

表单提示语句，输入后会这段语句消失

#### 2.action和method

action 是跳转页面

method 是执行方法

**案例：**

index.html（部分）

![image-20220317163658387](https://ossimg.yzitc.com/2022/03/17/c7a57aa60c93b.png)

registercheck.php

![image-20220317172445777](https://ossimg.yzitc.com/2022/03/17/90390c879875c.png)

![image-20220317172430175](https://ossimg.yzitc.com/2022/03/17/1f07da223cf24.png)

#### 3.PDO（）

### 数据库操作

#### 连接数据库

PHP 5 及以上版本建议使用以下方式连接 MySQL :

- **MySQLi extension** ("i" 意为 improved)
- **PDO (PHP Data Objects)**

#### 我是该用 MySQLi ，还是 PDO?

MySQLi 和 PDO 有它们自己的优势：

PDO 应用在 12 种不同数据库中， MySQLi 只针对 MySQL 数据库。

所以，如果你的项目需要在多种数据库中切换，建议使用 PDO ，这样你只需要修改连接字符串和部分查询语句即可。 

使用 MySQLi, 如果不同数据库，你需要重新编写所有代码，包括查询。

两者都是面向对象, 但 MySQLi 还提供了 API 接口。

两者都支持预处理语句。 预处理语句可以防止 SQL 注入，对于 web 项目的安全性是非常重要的。
