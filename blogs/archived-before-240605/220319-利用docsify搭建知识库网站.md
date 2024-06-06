# 如何利用docsify搭建文档知识库网站？

![image-20220319172426723](https://ossimg.yzitc.com/2022/03/19/196ba944d100e.png)

最近想做一个文档知识库的网站，目前主流的是VuePress或者Hexo这种来实现，简单了解了下还是比较简单的。

不过要说简单应该还是今天要介绍的这个：docsify。

实操了下，真的是几秒搞定。官方文档写的也比较详细，非常值得一试。

> 官方地址：
>
> https://docsify.js.org/#/zh-cn
>
> 我提供的demo：
>
> [docsify案例](/docsify)

> 本地部署docsify是需要npm和nodejs支持的。
>
> 不知道怎么安装的可以查看之前的文章：
>
> [安装Node.js详细步骤教程](https://www.shejibiji.com/archives/8113)

## 一、部署docsify详细步骤

1.

**本地安装部署docsify-cli**

首先打开命令行工具，输入npm安装命令：

````
npm install -g docsify-cli
````

然后我们在桌面新建一个docsify目录（其它位置也可以，只要自己记住这个路径即可）。

并使用cd命令访问这个docsify目录。



![image-20220319160446446](https://ossimg.yzitc.com/2022/03/19/37f805b94c898.png)

![image-20220319163350955](https://ossimg.yzitc.com/2022/03/19/2ca33b12220ad.png)

<font>（新建docsify目录，名称和位置都可以自定义）</font>

2.

**初始化docsify**

通过 `init` 初始化项目。

````
docsify init
````

![image-20220319160623898](https://ossimg.yzitc.com/2022/03/19/a76c5caeaa789.png)

中间会出现询问是否的选项，输入`y`即可。

如果出现上图这样，就表示成功了。

3.

**启动docsify服务**

终端输入命令：

````
docsify serve
````

![image-20220319160922575](https://ossimg.yzitc.com/2022/03/19/37e1f01e57ea2.png)

出现这个就表示成功了。



现在输入本地这个域名就可以打开访问了：

![image-20220319160854274](https://ossimg.yzitc.com/2022/03/19/2a5af4bab01bc.png)

上图这个就是默认的页面，是比较简单的。

我们可以通过修改`README.md`这个文件，来修改文档网站的内容。

## 二、更多优化设置

### 1、添加首页封面

首先我们需要开启封面。

打开根目录下的**index.html**，在这个位置添加一行：`coverpage: true`，开启封面。

![image-20220319161632138](https://ossimg.yzitc.com/2022/03/19/b83cf84f6bb7a.png)

然后再根目录下添加`_coverpage.md` 文件，编辑内容即可。

比如我提供的案例中，就是下面这段：

````html
<!-- _coverpage.md -->

# docsify <small>3.5</small>

> 这就是利用docsify生成的文档页面

- 简单几步就可以生成文档页面
- 不需要频繁生成启动
- 自带6个主题

[返回](/)
[查看案例](#利用docsify搭建知识库网站)
````

呈现的效果是这样的：

![image-20220319171044736](https://ossimg.yzitc.com/2022/03/19/97f962b12864e.png)

（背景色支持自定义，默认就是随机的渐变色背景）

### 2、添加定制导航栏

导航栏可以用来显示多语言，或者做成导航菜单，还是很有必要的。

方法是同样的，先开启导航栏，然后添加`_navbar.md`导航文件并编辑。

具体可以查看官方详细说明：[定制导航栏](https://docsify.js.org/#/zh-cn/custom-navbar)

## 三、其它相关问题

### 1、本地预览测试

关闭命令行工具后，端口就被关闭了，无法再打开页面测试了。

想本地预览的话，只要打开命令行工具，重新用cd命令访问上次的目录，然后使用启动服务命令，就可以重新打开了。

![image-20220319162821753](https://ossimg.yzitc.com/2022/03/19/1531975a7aadc.png)

### 2、部署到远程服务器

首先在服务器新建网站，并用域名访问网站目录。

复制目录和文件到网站目录下。

现在直接访问即可。

（我提供的案例是直接在我的网站下建立新目录放入文件实现的）

