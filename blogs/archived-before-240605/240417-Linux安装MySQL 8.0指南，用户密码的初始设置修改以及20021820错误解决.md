# Linux 安装 MySQL8 指南，用户密码的初始设置修改以及 2002/1820 错误解决

![Vida_2022-11-29_11-50-21](https://pic.shejibiji.com/i/2022/11/29/6385818960e97.jpg)

## 起因

迁移服务器后，发现MySQL无法使用，一直提示错误：

```bash
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/lib/mysql/mysql.sock' (2)
```

在网上没找到好的办法，索性决定重新安装MySQL，结果也是各种小问题，折腾了一下午，所以在这里特意记录下。

内容主要包括如何在Linux中**卸载MySQL**，如何新**安装MySQL**，以及两个**2002/1820错误的解决**。

接下来就开始这次干货的记录吧，可以根据自己的需求，选择查看内容。

## 卸载 MySQL

1.

**关闭MySQL服务**

```bash
systemctl stop mysqld.service
```

2.

**查看当前MySQL安装状况**

```bash
rpm -qa | grep -i mysql

# 或

yum list installed | grep mysql
```

3.

**卸载上述命令查询出的已安装程序**

```bash
yum remove mysql-xxx
```

4.

**删除MySQL相关文件**

```bash
# 查找相关文件：
find / -name mysql
# 删除上述命令查找出的相关文件：
rm -rf xxx
# 删除my.cnf
rm -rf /etc/my.cnf
```

## 安装 MySQL

> 官方指南：https://dev.mysql.com/doc/mysql-yum-repo-quick-guide/en/

1.

**查看自己的系统信息**

```bash
uname -a

# 结果

Linux izj6cgg3toifr6rhjppqezz 3.10.0-693.2.2.el7.x86_64 #1 SMP Tue Sep 12 22:26:13 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
```

2.

**更新YUM源**

打开 MySQL Yum 仓库：[MySQL Yum Repository](https://dev.mysql.com/downloads/repo/yum/)，找到适合自己系统的版本，然后替换下面的命令（`.../get/`后面的那段）：

```bash
sudo rpm -Uvh https://dev.mysql.com/get/mysql80-community-release-el7-11.noarch.rpm
```

![Ethan_2024-04-17_16-31-21](https://pic.shejibiji.com/i/2024/04/17/661f88e89b1cc.jpg)

3.

**安装MySQL**

```bash
sudo yum -y install mysql-community-server --enablerepo=mysql57-community --nogpgcheck
```

等待安装完成，就可以准备开始使用了。

## 配置MySQL并修改用户密码

1.

**启动并设置开机自启动MySQL服务**

```bash
sudo systemctl start mysqld
sudo systemctl enable mysqld
```

2.

**获取并记录root用户的初始密码**

*如果你是输入mysql就可以直接进入，则表示没有初始密码，可以跳过这一步。*

```bash
grep 'temporary password' /var/log/mysqld.log
```

执行命令结果示例如下:

```bash
2024-04-17T07:20:19.505536Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: P/eAwdtdl3Zl
# 示例末尾的P/eAwdtdl3Zl为初始密码
```

3.

修改密码

现在就可以使用这个临时密码进入MySQL服务了：

```bash
mysql -uroot -p
```

首次登录后，是没有办法正常使用的。MySQL 会强制你修改初始密码，这个时候无论你做什么操作都会提示：

```sql
ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement.
```

使用命令修改密码：

```sql
# NEW PWR 替换为你自己的
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'NEW PWR'; 
```

要注意的是，因为新的安全策略，可能你的密码会不通过，你可以先使用临时密码来通过这个检查。

之后通过下面这个命令来查看密码验证规则：

```sql
SHOW VARIABLES LIKE 'validate_password%';
```

执行命令结果示例如下:

![Ethan_2024-04-17_17-48-55](https://pic.shejibiji.com/i/2024/04/17/661f9b12170af.jpg)

我这个密码规则解读出来就是：最小长度为8，需要包含数字字母以及特殊符号。

（你之后可以通过设置全局变量的方式来修改这些值）

然后再次修改密码就可。

## 如何开启远程访问

*并不推荐远程访问，因为这样并不安全*

如果确实想开，请先确保载防火墙中，3306端口已经放行。

1.

进入服务器的 MySQL

```bash
mysql -uroot -p
```

2.

查看用户权限配置

1）使用 `mysql`

```sql
use mysql;
```

2）查询数据表 `user` 的 `host` 和 `user` 字段信息

 ```sql
 select host, user from user;
 ```

执行命令结果示例如下：

![Ethan_2024-04-17_18-02-41](https://pic.shejibiji.com/i/2024/04/17/661f9e5a6f86b.jpg)

`host`字段就表示能允许访问的**host**，`localhost`就表示只允许本机访问。

3.

**修改访问权限**

如果我们希望改成指定ip，则可以设置值为指定ip，如：

```mysql
update user set host = '192.168.1.%' where user = 'root';
```

`192.168.1.%`表示内网地址，意味着内网地址都可以访问。

如果想更改为任何ip，则直接使用通配符`%`即可。

**最后记得一定要刷新下权限：**

```sql
flush privileges;
```

## 关于 mysql.sock 的错误，代码2202

关于最开始的错误：

```bash
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/lib/mysql/mysql.sock' (2)
```

网上其实没有很好的解答，但在找了一圈资料后，发现这玩意会存在创建文件的动作，所以我在想是不是文件夹权限的问题，于是给这个文件夹一个全部的权限，问题就解决了，供参考：

```bash
chmod -R 777 /var/lib/mysql/
```

