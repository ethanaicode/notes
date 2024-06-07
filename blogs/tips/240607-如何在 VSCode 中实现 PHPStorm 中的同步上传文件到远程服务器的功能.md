# 如何在 VSCode 中实现 PHPStorm 中的同步上传文件到远程服务器的功能

需求来自部门的老大，他因为 PhpStorm 的和谐问题，想用 VSCode 来开发，不过习惯用 PhpStorm 中的右键同步上传文件到远程服务器的功能，所以问我能否在 VSCode 中找到替代。

这个简单，只需要用到 SFTP 插件即可实现，必须安排一个教程！

## 详细教程

1.

**下载插件 SFTP**

首先在 VSCode 中下载 SFTP 插件：

![Ethan_2024-06-07_10-56-50](https://pic.shejibiji.com/i/2024/06/07/666277099f0c5.jpg)

2.

**配置上传服务器信息**

在 VSCode 中打开你想上传的项目或者文件，

使用快捷键 `ctrl+shift+P` 打开指令窗口，也就是 VSCode 顶部的输入框内，然后输入：

```bash
>sftp
```

点击出现的第一个选项`SFTP:Config`，会自动在当前目录`.vscode`目录下，新建配置文件`sftp.json`：

![Ethan_2024-06-07_10-58-40](https://pic.shejibiji.com/i/2024/06/07/666278a82ad62.jpg)

在`sftp.json`中填入对应的服务器信息：

![Ethan_2024-06-07_11-00-00](https://pic.shejibiji.com/i/2024/06/07/666278cc57eec.jpg)

配置好后，保存。

3.

**现在就可以开始上传同步文件了**

右键点击想要上传的文件，选择 上传文件，

![Ethan_2024-06-07_11-01-13](https://pic.shejibiji.com/i/2024/06/07/666279dfb1d8a.jpg)

会让你输入密码，输入密码后继续：

![Ethan_2024-06-07_11-15-24](https://pic.shejibiji.com/i/2024/06/07/66627b5f1129c.jpg)

上传完成后，可以在服务器上确认下，可以看到测试的文件已经被上传了：

![Ethan_2024-06-07_11-02-19](https://pic.shejibiji.com/i/2024/06/07/66627a0605d9e.jpg)

亲测，如果本地文件夹下的文件，点击上传时，服务器上没有对应的文件夹，也会自动创建并上传到对应的文件夹内。