# 在 Linux 中使用 logrotate 管理日志文件

![logrotate](https://pic.shejibiji.com/i/2024/07/04/66867eff12058.jpg)

`logrotate` 是一个在 Linux 操作系统中用来管理日志文件的工具。其主要功能是帮助系统管理员自动管理和轮换日志文件，防止日志文件过大，占用过多的磁盘空间。`logrotate` 可以定期对日志文件进行压缩、删除、邮件通知等操作。

具体功能包括：

1. **轮换日志文件**：定期创建新的日志文件，并将旧的日志文件重命名或压缩。
2. **压缩日志文件**：将旧的日志文件压缩为 `.gz` 格式，以节省磁盘空间。
3. **删除旧日志文件**：在日志文件数量或大小超过指定限制时，自动删除最老的日志文件。
4. **邮件通知**：可以配置在日志文件轮换时发送邮件通知给系统管理员。
5. **自定义脚本**：在日志文件轮换前后执行自定义脚本，例如重启服务或运行特定的命令。

配置文件通常位于 `/etc/logrotate.conf` 和 `/etc/logrotate.d/` 目录中，系统管理员可以在这些配置文件中定义具体的日志轮换策略。

一个简单的 `logrotate` 配置示例如下：

```bash
/var/log/syslog {
    daily
    missingok
    rotate 7
    compress
    delaycompress
    notifempty
    create 0640 root utmp
    sharedscripts
    postrotate
        /usr/lib/rsyslog/rsyslog-rotate
    endscript
}
```

这个配置对 `/var/log/syslog` 日志文件进行如下操作：

- `daily`：每天轮换一次日志文件。
- `missingok`：如果日志文件不存在，不会报错继续执行。
- `rotate 7`：保留最近的7个日志文件，超出部分将被删除。
- `compress`：轮换后的日志文件进行压缩。
- `delaycompress`：延迟压缩到下次轮换时。
- `notifempty`：如果日志文件为空，不进行轮换。
- `create 0640 root utmp`：创建新日志文件，权限设置为0640，所有者为root，所属组为utmp。
- `sharedscripts`：在日志文件轮换前后执行脚本。
- `postrotate` 到 `endscript`：在日志文件轮换后执行 `/usr/lib/rsyslog/rsyslog-rotate` 脚本。

通过 `logrotate`，系统管理员可以确保日志文件管理的自动化和高效性，有效防止日志文件造成的磁盘空间问题。