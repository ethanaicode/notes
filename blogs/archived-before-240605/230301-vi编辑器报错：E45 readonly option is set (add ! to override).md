# vi编辑器报错：E45 readonly option is set (add ! to override)

vi编辑器退出时，弹出只读提示，如下：

[![1677657328039.jpg](https://img.shejibiji.com/2023/03/01/63ff04f2b8c4b.jpg)](https://img.shejibiji.com/2023/03/01/63ff04f2b8c4b.jpg)

这是因为没有使用管理员模式进行编辑。

可以先使用`:qa!`退出编辑器，然后再使用命令`sudo vim filename`来编辑（filename请换成要编辑的文件）。

可能需要输入密码，输入即可。

这样再`:wq`时就可以了正常保存退出了。