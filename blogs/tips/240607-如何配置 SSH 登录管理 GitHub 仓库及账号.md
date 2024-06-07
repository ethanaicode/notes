# 如何配置 SSH 登录管理 GitHub 仓库及账号

现在 Github 官方推荐的方式就是 SSH，之前一直也懒得配置，反正有办法可以上传仓库，没啥影响就没动。

但想用 VSCode 直接同步仓库，就容易报错，今天有空，索性就按照官方教程实现 SSH 管理，彻底解决掉这个问题。

官方有教程：[Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

按照官方教程一步步来，也不会特别复杂。

## 详细步骤

1.

**首先在本地生成一个新的 SSH Key**

打开命令行工具，输入下列命令，替换邮箱为你的 GitHub 邮箱地址：

```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

> 如果你的系统不支持 Ed25519，可以用下列命令
>
> ```bash
> ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
> ```

这会生成一个新的 SSH Key：

![Ethan_2024-06-07_18-56-06](https://pic.shejibiji.com/i/2024/06/07/6662e759ba140.jpg)

中间会有提示，让你输入安全密码，你可以设置，也可以直接跳过。

2.

**找到公钥**

创建时，可以看到提示身份信息被储存到什么位置，通常在用户的`.ssh`目录下，可以通过下列命令来访问：

```bash
cd ~/.ssh/
```

不出意外的你可以看到文件：`id_ed25519.pub`

打开它，并复制里面的公钥。

![Ethan_2024-06-07_19-04-56](https://pic.shejibiji.com/i/2024/06/07/6662e9671b7c8.jpg)

3.

**在 GitHub 上添加该公钥**

在 GitHub 上，找到个人设置里面，找到 SSH 和 GPG，点击添加新的 SSH Key：

![Ethan_2024-06-07_19-07-08](https://pic.shejibiji.com/i/2024/06/07/6662e9e9bd786.jpg)

打开后，填入公钥，点击保存即可：

![Ethan_2024-06-07_19-08-05](https://pic.shejibiji.com/i/2024/06/07/6662ea279d28e.jpg)

现在 SSH 配置就完成了。

4.

**测试 SSH 的有效性**

你可以测试下你的 SSH 配置是否生效了，只需要使用下方命令：

```bash
ssh -T git@github.com
```

如果成功会返回下列消息：

```bash
> Hi shejibiji.com! You've successfully authenticated, but GitHub does not provide shell access.
```

5.

**修改 git 配置以应用 SSH**

打开你想用 SSH 管理的 GitHub 项目目录，通过 git 命令修改配置：

```bash
git config remote.origin.pushurl "git@github.com:YOUR_ACCOUNT/YOUR_PROJECT.git"
```

注意里面的`YOUR_ACCOUNT`和`YOUR_PROJECT`需要改成自己的用户名及项目名称。

这样就完成了项目的 git 配置修改。

现在你就可以直接开始提交该代码到对应的仓库了，而且也不用输入密码，还是非常舒适的。



官方教程考虑的情况比较多，如果遇到什么问题，可以在 设计笔记 这个网站留言，也可以参考教程继续寻找答案。

\- enjoy! -