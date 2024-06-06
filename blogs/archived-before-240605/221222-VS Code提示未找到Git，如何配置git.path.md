## VS Code提示未找到Git，如何配置git.path

![R_22-12-22-11-40-51_80](https://pic.shejibiji.com/i/2022/12/22/63a3d1d057b27.jpg)

> 使用VS Code 提示 '未找到Git.请安装Git，或在“git.path”设置中配置'

首先请确保已经安装git。

确保安装后，还出现这个提示，肯定是因为没有配置git安装目录。

打开VS Code的`setting.json`，添加下面这段即可：

```json
	// Is git enabled
    "git.enabled": true,

    // Path to the git executable
    "git.path": "H:\\Program Files\\Git\\bin\\git.exe",
    "git.defaultCloneDirectory": "H:\\Documents\\Github\\"
```

找不到设置的，可以参考下图：

![R_22-12-22-11-37-15_80](https://pic.shejibiji.com/i/2022/12/22/63a3d10e2b3b4.jpg)

配置完成，重启下VS Code即可使用Git了。