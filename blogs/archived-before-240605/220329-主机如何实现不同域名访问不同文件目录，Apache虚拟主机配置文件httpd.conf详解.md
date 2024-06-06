# 主机如何实现不同域名访问不同文件目录，Apache虚拟主机配置文件httpd.conf详解

> 教程是在本地Windows系统上，使用XAMPP搭建的服务器环境做的示范。
>
> 原理都是类似的，不管是Nginx或者Linux服务器，都可以参考这个进行修改。

![APACHE Software](https://ossimg.yzitc.com/2022/03/29/e1218c9ec11d2.png)

搭建了服务器环境，上线了网站，却发现默认地址只能访问服务器根目录。

如果我想在服务器上搭建多个网站该怎么办呢？能否不同的域名访问同一台服务器，并定位到不同的文件目录？

Apache中，这个很容易实现，通过虚拟主机在同一台服务器上，可以运行多个网站或者Web应用，并使用自定义域名访问每个网站或者Web应用。

每个虚拟主机都可以映射到服务器的不同目录。

这个功能特别好用，它可以让同一个根域名，来访问不同的应用。

例如，域名http://app01.localhost和http://app02.localhost可以指向同一服务器上的两个单独的应用。

或者，可以使用不同的域名来访问同一个服务器上的不同应用，例如http://client1/、http://client2/等。

## 配置虚拟主机

1、打开XAMPP 安装目录（通常为*C:\xampp*），使用文本编辑器打开`apache\conf\extra\`下的`httpd-vhosts.conf`文件。

2、在文件底部添加下面指令：

   ```
   <VirtualHost *:80>
    DocumentRoot "C:/xampp/htdocs"
    ServerName localhost
   </VirtualHost>
   <VirtualHost *:80>
    DocumentRoot "C:/xampp/apps/wordpress/htdocs"
    ServerName wordpress.localhost
   </VirtualHost>
   ```

> 上面这段包含两个虚拟主机配置块：
>
> - 第一个块是默认虚拟主机，用于后续块不匹配的所有请求。
> - 第二个块设置一个名为*wordpress.localhost*的虚拟主机。**DocumentRoot** 指令指定为该虚拟主机服务请求时要使用的目录（在本例中为 WordPress 安装目录），而 **ServerName** 指令指定虚拟主机的自定义域名。
>
> 要添加更多虚拟主机，只需复制第二个虚拟主机块并根据您的要求修改端口号、DocumentRoot 和 ServerName 指令。
>
> 例如，如果您想将 SSL 与您的自定义域名一起使用，您可以为端口 443 添加一个新的虚拟主机块。

比如我想自定义一个域名`chen.com`，访问网站根目录为`www/wp1/`，就可以改成如下图这样：

（前面地址根据不同的XAMPP 安装目录会有所不同）

![image-20220329215932503](https://ossimg.yzitc.com/2022/03/29/453745b9bb0ab.png)

这样就配置好了虚拟主机！

我们重启下Apache服务。

但现在这个域名并不知道应该访问我们这台主机，所以我们还需要修改下域名解析。

3.我们找到主机上的hosts文件，位置在：`C:\windows\system32\drivers\etc\hosts`，使用记事本打开这个文件，在尾部添加这句：

```
127.0.0.1       chen.com
```

（如果是服务器就使用域名解析到对应的IP）

现在使用`chen.com`这个域名就可以访问对应的虚拟主机目录了。

> **拓展：**
>
> Directoryindex shouye.html
>
> 默认首页访问的是index.html，我们可以通过类似上面的语句，来自定义首页的文件名。

