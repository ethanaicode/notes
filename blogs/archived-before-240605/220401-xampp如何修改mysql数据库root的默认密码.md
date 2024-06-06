# xampp如何修改mysql数据库root的默认密码

因为安装xampp后的mysql默认用户root的密码为空，而部署一些应用时需要提供数据库密码，填空无法通过。

此时就需要给root设定密码。

xampp的mysql数据库也是通过phpmyadmin管理的，所以我们能登录到phpmyadmin，在浏览器地址上输入http://localhost/phpmyamdin 进入到数据库控制面板，然后选择名称为mysql数据库，如图，可从中看出 user表中，root的两个用户的密码为空（我这个已经改好了）。

![image-20220401212115188](https://ossimg.yzitc.com/2022/04/01/bf04a8b844068.png)

接下来我们手动更改下密码即可。

点击数据库左上角的小房子，回到首页。

![image-20220401212242857](https://ossimg.yzitc.com/2022/04/01/a55ba95a03e52.png)

然后找到`账户`（有的是用户）。

![image-20220401211508743](https://ossimg.yzitc.com/2022/04/01/a3790cc37e488.png)

打开账户管理后就可以用户概况。

我们点击root账户的`修改权限`。

![image-20220401211547818](https://ossimg.yzitc.com/2022/04/01/37a542228365c.png)

然后点击上面的`修改密码`。

![image-20220401211612622](https://ossimg.yzitc.com/2022/04/01/3bd44f1d19df1.png)

输入密码后，点击执行即可。

![image-20220401211623365](https://ossimg.yzitc.com/2022/04/01/94f05cab54012.png)

执行成功后刷新页面，会出现错误页面，原因是没有修改配置文件，你的密码已经修改了，系统依然按旧密码登陆，所以显示登陆失败。

改下phpmyadmin中的对应密码配置即可解决这个问题。

我们找到phpmyadmin的配置文件，如我的是：
F:\xampp\phpMyAdmin\config.inc.php

打开后，修改这一段，把刚才改好的密码输入进去：

![image-20220401211807923](https://ossimg.yzitc.com/2022/04/01/b080cb907abae.png)

当然您不改这块数据库也会照常工作，只不过phpmyadmin是数据库管理程序，我们要用到它来创建管理数据库等操作，如果不修改config.inc.php文件中的内容，则phpmyadmin无法打开页面。