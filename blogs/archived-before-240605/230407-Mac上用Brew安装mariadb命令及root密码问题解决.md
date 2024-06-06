# Mac上用Brew安装mariadb命令及root密码问题解决

![Ethan_2023-04-07_17-38-23](https://pic.shejibiji.com/i/2023/04/07/642fe4ab16252.jpg)

最近需要用到MariaDB，习惯性用brew安装了，一行命令搞定：

```bash
brew install mariadb
```

然后设置自动启动mariadb，也是一行命令：

```bash
brew services start mariadb
```

官方文档：[Installing MariaDB Server on macOS Using Homebrew](https://mariadb.com/kb/en/installing-mariadb-on-macos-using-homebrew/)

打印下已启动的服务列表：`brew services list`，可以看到mariadb已经启动了：

![Ethan_2023-04-07_17-17-40](https://pic.shejibiji.com/i/2023/04/07/642fdfbd1a66b.jpg)

以上，就算完成了mariadb的安装及启动。

可以输入`mariadb -v`来查看版本信息。

![Ethan_2023-04-07_16-23-47](https://pic.shejibiji.com/i/2023/04/07/642fd32a33e6f.jpg)

这个时候会默认进入mariadb命令，可以输入下面命令来查看端口号和状态（加分号后按回车才会执行语句）

查看端口号：

```bash
show global variables like 'port';
```

查看状态：

```bash
status;
```

## 密码问题解决

当我输入`mariadb-secure-installation`初始化时，上来就找我要密码，我直接按enter是不管用的，可是去网上搜了下，说的都是root用户，默认没有密码，我就有点无语了。

**最后还是找到了这一条命令解决的：**

```bash
MariaDB [(none)]> ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD("你的密码");
```

首先需要输入`mariadb`，进入mariadb命令行模式，然后再输入上面的命令就可以修改root用户的密码了。

**完整的过程可以下面的代码：**

```bash
os@osdeMacBook-Pro mariadb@10.11 % mariadb
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 29
Server version: 10.11.2-MariaDB Homebrew

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> ALTER USER root@localhost IDENTIFIED VIA mysql_native_password USING PASSWORD("123456");
Query OK, 0 rows affected (0.014 sec)

MariaDB [(none)]> Ctrl-C -- exit!
Aborted
os@osdeMacBook-Pro mariadb@10.11 % mariadb-secure-installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.

Enter current password for root (enter for none): 
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.

Switch to unix_socket authentication [Y/n] n
 ... skipping.

You already have your root account protected, so you can safely answer 'n'.

Change the root password? [Y/n] n
 ... skipping.

By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
```

现在再去连接本地的mariadb就可以成功了：

![Ethan_2023-04-07_17-29-17](https://pic.shejibiji.com/i/2023/04/07/642fe289c0ab2.jpg)
