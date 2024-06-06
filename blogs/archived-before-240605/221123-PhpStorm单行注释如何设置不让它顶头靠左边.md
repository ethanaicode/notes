# PhpStorm单行注释如何设置不让它顶头靠左边

之前一直用的vs code，很舒服，不过老板不习惯，强制让我用回了PhpStorm:(

虽然总体两款工具区别用起来也没那么大，但是我实在受不了为什么PhpStorm用默认的快捷键 Ctrl+/ 注释代码时，`//`注释是顶格的，紧挨着左边，看起来就超级的别扭。

![00](https://pic.shejibiji.com/i/2022/11/23/637da263daff7.png)

而且这样的注释，如果放到vs code，折叠也会出现问题，vs code无法正常分块了。

那么该如何解决这个问题了？其实只要改下PhpStorm设置即可。

## 修改设置

1.

首先我们在`File`下，找到`Settings`，进入设置页面：

![01](https://pic.shejibiji.com/i/2022/11/23/637da07fb0e2e.png)

2.

然后左侧找到`Code Style`，找到`PHP`，点击它，打开PHP的配置项。

然后找到`Code Generation`，把下面的`Line comment at first column`的勾给去掉即可。

![03](https://pic.shejibiji.com/i/2022/11/23/637da33ff328f.png)

现在再按Ctrl+/注释，注释符`//`就不会再紧挨着左边了。

我们还可以顺便改一下格式化时的设置。

3.

还是刚才的位置，我们找到`Wrapping and Braces`，把下面的`comment at first column` 的勾也去掉。

这样格式化的时候，就不会影响到这个注释缩进了。

![02](https://pic.shejibiji.com/i/2022/11/23/637da342b27ae.png)

这下终于舒服了。

