# MariaDB 连接被拒绝，修改密码不生效问题解决

在 Debian 中，已经不推荐安装 MySQL，而是推荐 MariaDB。

今天安装 MariaDB 后，使用`mysql_secure_installation`命令做了初始化，设置了密码，命令行登录都没啥问题。

但是当我使用远程管理工具连接时，就发现连接被拒绝了，提示：

```bash
Access denied for user 'root'@'localhost'
```

因为我是使用 SSH 建立通道来远程连接的，理论上和本地运行应该是一样的……不应该呀，是哪里出问题了。

## 找出问题

在服务器上继续测试：

输入账号密码，登录数据库，没有问题。

检查 user 数据库表，密码字段有值，确认有密码，没有问题。

难道是我密码写错了？退出，重新登录，随便输入一个密码，然后……登录成功了……

啊？

继续尝试不输入密码，也登录成功，密码完全失效了。

去谷歌了下，才知道原因：

**新版的 Mariadb 身份验证默认都是用 Unix Socket 插件，而不是传统的密码。**

这意味着用户的身份验证是基于其 Unix/Linux 系统账户，而不是存储在数据库中的密码。

以下是更多相关知识，有兴趣的可以了解，想直接解决问题可以跳到最后：

### 什么是身份验证插件？

MariaDB 中的身份验证插件是一个模块，用于定义用户在尝试连接数据库服务器时的身份验证方式。这些插件扩展了 MariaDB 的功能，以支持默认之外的不同认证方法。

### 什么是 unix_socket 身份验证插件？

unix_socket 插件将 Unix/Linux 系统用户直接映射为 MariaDB 用户。

当用户通过 Unix 套接字（用于进程间通信的特殊文件）连接到 MariaDB 时，插件会检查用户的 Unix 凭证，以验证其身份。

### unix_socket 如何工作？

当您使用 unix_socket 插件连接 MariaDB 时，服务器会根据您登录的 Unix 用户验证您的身份。如果 Unix 用户与配置为使用 unix_socket 插件的 MariaDB 用户相匹配，则无需提供密码即可通过身份验证。

### 为什么不需要密码

不需要密码的主要原因是，unix_socket 插件利用了底层 Unix/Linux 系统的用户身份验证。我们的假设是，如果您已经通过了操作系统的身份验证（例如，通过登录系统），那么就没有必要再使用单独的密码对数据库进行身份验证。

### 常用的身份验证插件

以下是 MariaDB 中一些常用的身份验证插件：

- **mysql_native_password**：默认插件，使用原生的 MariaDB 密码散列机制。
- **unix_socket**： 允许用户使用其 Unix/Linux 系统凭证进行身份验证。
- **pam**： 使用可插拔身份验证模块（PAM）进行灵活的身份验证管理。
- **ldap**：与 LDAP（轻型目录）集成： 与 LDAP（轻量级目录访问协议）集成，用于集中式用户身份验证。

## 理解问题

unix_socket 身份验证的目的是让与 MariaDB 服务器登录在同一 Unix/Linux 系统中的用户使用。它会根据本地系统的用户数据库检查凭证。

由于 unix_socket 依赖于本地 Unix 用户凭据，虽然 SSH 隧道可以安全地转发端口，并有效地从网络角度使远程连接看起来像本地连接，但这并不能改变 unix_socket 需要本地 Unix 用户凭证进行身份验证的事实。

那么解决思路也就清楚了：**更换身份验证插件**

## 解决问题

我看网上的做法通常是直接修改 root 用户的验证插件来解决，但这就失去了 unix_socket 身份验证的便利性，毕竟官方默认用这种做法肯定是有道理的。

所以我这里是通过创建一个新管理用户来实现，用 root 用户登录后，**分别执行下面 3 条命令**：

_用户名及密码可以改成你喜欢的，如果不改密码，那么密码就是：your_secure_password（🐶）_

```sql
CREATE USER 'ssh_root'@'localhost' IDENTIFIED BY 'your_secure_password';
GRANT ALL PRIVILEGES ON *.* TO 'ssh_root'@'localhost';
FLUSH PRIVILEGES;
```

**这个新创建的用户，默认的验证方式就是：`mysql_native_password`，也就是传统的密码验证方式。**

可以使用下列命令验证下：

```sql
SELECT user, host, plugin FROM mysql.user;
```

![Ethan_2024-06-05_12-44-09](https://pic.shejibiji.com/i/2024/06/05/665fed2be1992.jpg)

现在使用这个新用户及密码就可以完成远程登录管理了。

\- Enjoy! -
