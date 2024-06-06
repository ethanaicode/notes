# Debian 使用 apt 无法安装软件，连接失败问题解决

![Ethan_2024-05-31_18-33-28](https://pic.shejibiji.com/i/2024/05/31/6659a78abc051.jpg)

最近新买了一台 Debian 的服务器，准备自己跑着玩玩。

但是使用 apt 安装软件时，一直提示连接失败，404等错误，就是无法连接网络（忘记截图了，这里就不展示了）。

去官方镜像仓库看了下，才发现官方最近更换了套件的位置，通知在这里：[Stretch has been moved to archive.debian.org](https://lists.debian.org/debian-devel-announce/2023/03/msg00006.html)

原文为：

> Hi,
>
> the stretch, stretch-debug and stretch-proposed-updates suites have now
> also been imported on archive.debian.org. People still interested in
> these should update their sources.list.
>
> I plan to remove the suites from the main archive in about a month
> (2023-04-23 or later).
>
> The stretch-backports, stretch-backports-sloppy and related debug suites
> will likely move soon as well and might be removed from the main archive
> around the same time.
>
> Ansgar

**翻译：**

> stretch、stretch-debug 和 stretch-proposed-updates 套件现在也已导入 archive.debian.org。仍对这些感兴趣的人应该更新 sources.list。
>
> 我计划在大约一个月后（2023-04-23 或更晚）从主存档中删除这些套件。
>
> stretch-backports、stretch-backports-sloppy 和相关调试套件
> 可能也会很快移动，并可能在大约同一时间从主存档中删除。

根据官方的提示，解决也很简单，只需要修改资源列表的配置文件即可。

配置文件在 `/etc/apt/sources.list`，可以使用以下命令来更新:
（最好注释掉之前存在的源）

```bash
echo "deb http://archive.debian.org/debian stretch main" >> /etc/apt/sources.list
echo "deb-src http://archive.debian.org/debian stretch main" >> /etc/apt/sources.list
echo "deb http://archive.debian.org/debian stretch-backports main" >> /etc/apt/sources.list
echo  "deb http://archive.debian.org/debian-security stretch/updates main" >> /etc/apt/sources.list
echo  "deb-src http://archive.debian.org/debian-security stretch/updates main" >> /etc/apt/sources.list
```

这些命令就是把内容写入`sources.list`文件，所以你也可以直接用`vim`来编辑配置文件，达到相同的目的。
