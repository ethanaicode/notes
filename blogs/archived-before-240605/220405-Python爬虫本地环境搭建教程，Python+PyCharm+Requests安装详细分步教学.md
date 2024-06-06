# Python爬虫本地环境搭建教程，Python+PyCharm+Requests安装详细分步教学

![image-20220405135624452](https://ossimg.yzitc.com/2022/04/05/8344af1f539c5.png)

最近想本地测试下Python爬虫项目，于是就想在我的Windows电脑上搭建一个Python本地环境。

如果要实现Python爬虫项目，下面这三个是必不可少的：

1、Python（基础）

2、Pycharm（Python编辑器）

3、Requests（第三方库，用来爬取网页）

如果需要爬视频下载等项目，还需要其它库，比如ffmage，aria2等。

今天主要演示下本地Python爬虫项目基础的三个环境搭建：

1.

**Python 3.10**

官方下载地址：https://www.python.org/downloads/

下载后打开安装包，可以按照需要进行安装。

（不熟悉的可以看到勾都给点上，第一步选择是`Install Now`）

![image-20220405104731815](https://ossimg.yzitc.com/2022/04/05/1cd7e1caf27f7.png)

2.

**Pycharm**

python编辑器的话，推荐pycharm，具体下载安装可以看这篇文章：[PyCharm下载和安装](/archives/600)

3.

**Requests**

Requests 一直在 Github 上积极地开发，你可以一直从[这里](https://github.com/requests/requests)获取到代码。

你可以克隆公共版本库：

```
git clone git://github.com/kennethreitz/requests.git
```

也可以下载 [tarball](https://github.com/requests/requests/tarball/master):

```
$ curl -OL https://github.com/requests/requests/tarball/master
# Windows 用户也可选择 zip 包
```

**推荐使用pip命令行安装。**

只需要运行Windows电脑命令行，输入以下命令即可安装：

````
pip install requests
````

安装后，输入`pip list`，如果pip列表中有`requests`就表示安装完成了。

![image-20220405134546695](https://ossimg.yzitc.com/2022/04/05/ad5670982ce7e.png)

现在来测试一下。

我们打开PyCharm，输入以下代码：

```
import requests
response = requests.get('http://httpbin.org/get')
print(response.text)
```

右键点击运行就可以看到结果了。

![image-20220405134244429](https://ossimg.yzitc.com/2022/04/05/594c0043e41be.png)

> requests这一步其实很容易出错，之前我也是遇到无法找到requests命令的错误。
>
> 经过测试推测应该是Python解释器的原因。（这个时候打开PyCharm是找不到项目解释器选项的）
>
> 可以通过新建项目，然后自定义解释器，选择之前安装的python目录，就可以解决。

