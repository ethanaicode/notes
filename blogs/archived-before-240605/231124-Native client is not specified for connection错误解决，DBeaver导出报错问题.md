# Native client is not specified for connection错误解决，DBeaver导出报错问题

新装了DBeaver后，选择 dump 导出数据时，一直报错，提示：Native client is not specified for connection。

官方解释了这个事情的原因，就是**暂时不支持在Linux上自动加载本机客户端**。[#15749](https://github.com/dbeaver/dbeaver/issues/15749)

![Ethan_2023-11-28_13-32-11](https://pic.shejibiji.com/i/2023/11/28/65657b7e2798e.jpg)

我用的是MySQL，那么应该就是DBeaver 在电脑系统上找不到 **mysqldump** 可执行文件。

**其它的数据库报这个错误应该也是类似的问题。**

解决方法也很简单，就是配置指定下 **mysqldump** 可执行文件的位置即可。

## 解决方法

1.

在DBeaver的导出对话框中，点击“本地客户端…”按钮。

![Ethan_2023-11-28_13-36-41](https://pic.shejibiji.com/i/2023/11/28/65657ce943dfa.jpg)

2.

在弹出窗口中的下拉菜单中，选择“浏览…”选项。

（我这里已经安装过了，如果还没安装这里会是空的，只有浏览选项）

![Ethan_2023-11-28_13-37-25](https://pic.shejibiji.com/i/2023/11/28/65657cfbb40b9.jpg)

然后，点击添加，找到你电脑上的**mysqldump**可执行文件，添加进来就可以了。

记得点击保存。



**如何找到自己的mysqldump可执行文件？**

直接全局搜索吧，最直接快速：

![Ethan_2023-11-28_13-43-12](https://pic.shejibiji.com/i/2023/11/28/65657dfca1df5.jpg)