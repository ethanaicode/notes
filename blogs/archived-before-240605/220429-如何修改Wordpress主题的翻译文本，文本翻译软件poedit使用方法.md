# 如何修改Wordpress主题的翻译文本，文本翻译软件poedit使用方法

![image-20220429163407780](https://pic.shejibiji.com/i/2022/04/29/626ba2ffeb4ee.png)

今天想改一个主题的一段文本，前台是一段中文，我找到对应的php文件，直接搜索这段中文，竟然没有找到。

于是仔细看了下代码，发现这个位置是一段英文，使用了_e()方法包裹着。

![image-20220429162015814](https://pic.shejibiji.com/i/2022/04/29/626b9fc01fff5.png)

推测是使用了多语言设置，这是默认的英文，输出时根据位置输出对应的中文。

于是去WordPress查看了下`_e()`的意思，这是原文链接：

https://developer.wordpress.org/reference/functions/_e/

我也没仔细看，大概知道是显示翻译文本的。

那我要想修改这一段文本，最好的方法当然是，不破坏主题本身，而是仅仅修改这一段的对应翻译。

那么如何修改Wordpress主题的翻译文本呢？

其实Wordpress主题的翻译文件一般都是放在`language`文件夹下，格式一般为`.mo`。如：

![image-20220429162646875](https://pic.shejibiji.com/i/2022/04/29/626ba14718732.png)

`.po`是文本文件，可以直接用记事本打开的。

`.mo`是编译后的，wordpress用的为这个文件。

如果要修改`.mo`文件，需要用到专门的翻译工具，这里推荐：[Poedit](https://poedit.net/)

## .mo语言包修改方法

1.

**下载翻译工具[Poedit](https://poedit.net/)并安装。**

2.

**下载翻译文件。**

就是之前上图的那两个后缀分别为`.po`、`.mo`文件。

3.

**修改翻译文件。**

打开翻译工具Poedit，通过浏览文件打开`.po`文件。

![image-20220429163502207](https://pic.shejibiji.com/i/2022/04/29/626ba3366ee6c.png)

打开后，我们可以直接搜索，找到我们想要修改的文本：

![image-20220429163739409](https://pic.shejibiji.com/i/2022/04/29/626ba3d3a3cec.png)

修改后，点击`文件`，选择`编译为MO`，即可保存一个同名的`.mo`文件。

![image-20220429163813471](https://pic.shejibiji.com/i/2022/04/29/626ba3f5a25eb.png)

4.

**替换MO文件，完成修改**

我们把修改好的MO文件，传到服务器替换掉之前的翻译文件，即可完成修改。