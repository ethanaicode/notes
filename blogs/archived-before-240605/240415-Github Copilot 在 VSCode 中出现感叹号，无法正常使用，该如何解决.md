# Github Copilot 在 VSCode 中出现感叹号，无法正常使用，该如何解决

![Ethan_2024-04-15_11-27-17](https://pic.shejibiji.com/i/2024/04/15/661c9eb25d673.jpg)

最近在用 Github Copilot 时，图标旁边一直有一个感叹号，功能也无法使用。

![Snipaste_2024-04-10_14-23-24](https://pic.shejibiji.com/i/2024/04/15/661c987241ba0.png)

尝试联系 GitHub 支持，给我的回复也是和网上的解决方法类似，更新 VSCode，重新安装插件等。

![Ethan_2024-04-15_11-02-14](https://pic.shejibiji.com/i/2024/04/15/661c98c0e421f.jpg)

不过官方提供了一个很重要的信息，那就是我压根没有发送 Token 令牌。

据此我推断，可能是我的网络问题，经过一番测试，我确定是 VSCode 的网络问题。

因为我开了代理，推测最大的可能是这块没有设置好，那么只需要设置下 VSCode 的端口代理即可。

### 解决方法

打开 VSCode 的设置界面，输入 `proxy` ，找到 Proxy 设置，更新下本地网络代理的 proxy 设置即可。

![Ethan_2024-04-15_11-21-11](https://pic.shejibiji.com/i/2024/04/15/661c9d64c90ce.jpg)

重启 VSCode，问题就被解决了。