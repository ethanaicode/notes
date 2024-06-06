# Photoshop 所有的快捷键都无法使用，默认快捷键丢失解决办法

出现问题，解决问题。

刚装上的 Photoshop 快捷键都不可以用了，我还以为默认快捷键被改了呢？

但是试图 Ctrl + S 保存文件发现也不可以用，才意识到 Photoshop 是所有的快捷键都不可以用了。

而且注意看，菜单中后面的快捷键提示也都没了：

![Ethan_2024-05-28_15-05-16](https://pic.shejibiji.com/i/2024/05/28/6655826b48ab3.jpg)

中文搜了一圈，发现没有有用的答案。

于是尝试用英文搜索，意外让我找到了答案，就是这篇：[Default Photoshop keyboard shortcuts missing](https://community.adobe.com/t5/photoshop-ecosystem-discussions/default-photoshop-keyboard-shortcuts-missing/m-p/9203949)

有个用户回答说：

I tried this on my mac, and it worked: go to applications, find Photoshop, double-click to open, find Locales folder - en_US - support files - shortcuts, and located Default Keyboard Shortcuts.kys file, double-click it and recheck Photoshop shortcuts.

**翻译成中文就是：**

我在 Mac 上试过这个方法，很有效：进入应用程序，找到 Photoshop，双击打开，找到 Locales 文件夹 - en_US - 支持文件 - 快捷方式，找到 Default Keyboard Shortcuts.kys 文件，双击该文件并重新选中 Photoshop 快捷方式。

**试了下，问题完美解决：**

![Ethan_2024-05-28_15-14-10](https://pic.shejibiji.com/i/2024/05/28/66558456e41ae.jpg)

具体文件位置可以参考下图：

双击让 Photoshop 加载下即可。

![Ethan_2024-05-28_15-03-32](https://pic.shejibiji.com/i/2024/05/28/6655842b08a42.jpg)