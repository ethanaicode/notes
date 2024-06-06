# 如何通过 supervisor 来监控并自动重启进程

> 本文来自我的记事本，我整理了下觉得挺有用就发出来了。

![Ethan_2024-05-16_15-54-46](https://pic.shejibiji.com/i/2024/05/16/6645bbf5b4f74.jpg)

## 介绍

Supervisor 是一个进程管理工具，它允许您监控和控制长时间运行的进程。
Supervisor 可以确保您的进程在失败时自动重新启动，并且可以在进程崩溃时发送通知。

## 开始使用

当关闭命令行或终止进程时，后台运行的 PHP 脚本将被停止。
为了使脚本持续运行，可以使用进程管理工具，如 Supervisor。
Supervisor 确保您的脚本在失败时自动重新启动并持续运行。
以下是如何设置 Supervisor：

### 安装 Supervisor

确保 Supervisor 已安装在您的系统上。通常可以使用包管理器安装它：

```bash
brew install supervisor 					# For Mac by brew
sudo apt-get install supervisor             # For Ubuntu/Debian
sudo yum install supervisor                 # For CentOS/RHEL
```

### 启动 Supervisor

可以运行以下命令启动 Supervisor：

```bash
brew systemctl start supervisor
```

如果是 Linux 系统，可以使用以下命令启动 Supervisor：

```bash
sudo systemctl start supervisor
```

### 创建 Supervisor 配置文件

为了使其工作，我们必须创建一个配置文件。

Supervisor 提供了一个方便的命令来生成默认配置文件。可以使用以下命令生成默认配置文件：

```bash
echo_supervisord_conf > /usr/local/etc/supervisord.conf
```

现在默认配置已设置，我们需要创建以下目录，以便 Supervisor 可以查找您的配置文件：

```bash
mkdir /usr/local/etc/supervisor.d
```

现在在我们刚刚创建的目录中创建您的 Supervisor 配置文件：

```bash
vim /usr/local/etc/supervisor.d/test_worker.ini
```

为您的 PHP 脚本创建一个 Supervisor 配置文件。例如，创建一个名为 `test_worker.ini` 的任务：

```ini
[program:test_worker]
command=/Applications/MAMP/bin/php/php8.2.0/bin/php /Applications/MAMP/htdocs/zai/vcseem_ma/workers/worker_test.php
;; start at supervisord start (default: true)
autostart=true
;; retstart at unexpected quit (default: true)
autorestart=true
stderr_logfile=/var/log/test_worker.err.log
stdout_logfile=/var/log/test_worker.out.log
```

在这个配置文件中，我们定义了一个名为 `test_worker` 的进程，它将运行我们的 PHP 脚本。
我们还定义了一些其他选项，例如 `autostart` 和 `autorestart`，以确保进程在启动时自动启动并在失败时自动重新启动。

### 更新 Supervisor 配置

告诉 Supervisor 读取新配置并启动进程：

```bash
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl start test_worker
```

现在，Supervisor 将管理您的 PHP 脚本的执行，并且如果脚本崩溃或您手动停止它，它将自动重新启动脚本。

### 管理 Supervisor 进程

如果想停止或者重启进程，可以使用以下命令：

```bash
sudo supervisorctl stop test_worker
sudo supervisorctl start test_worker
```

你还可以使用 Supervisor 监控进程的状态：

```bash
sudo supervisorctl status
```

这个命令将显示所有受管进程的状态，包括您的 `test_worker`。

### 结论

通过使用 Supervisor，您可以确保您的 PHP 脚本在失败时自动重新启动并持续运行。它为在生产环境中管理长时间运行的进程提供了一个强大的解决方案。

## 常见问题

### 无法启动 Supervisor

如果您无法启动 Supervisor，可能是因为 Supervisor 的配置文件路径不正确。

在 Mac 上，您可以使用以下命令查找 Supervisor 的配置文件路径：

```bash
brew info supervisor
```

在 Linux 上，您可以使用以下命令查找 Supervisor 的配置文件路径：

```bash
sudo find / -name supervisord.conf
```

确保您的配置文件路径正确，并且 Supervisor 可以找到它。

### 无法启动配置的进程

如果您无法启动配置的进程，可能是因为您的配置文件中有错误。

您可以使用以下命令检查配置文件中的错误：

```bash
sudo supervisorctl reread
```

这将重新读取配置文件并显示任何错误。

你也可以先手动在命令行执行一次你的命令，看看是否有错误。

如果出现 ERROR (spawn error) 时，可能是因为您的命令路径不正确，或者文件没有执行权限。

如果有记录日志的路径，也要确保日志文件的路径是正确的，并且有写入权限。
