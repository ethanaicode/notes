# 兰空图床LskyV2如何获取Token和API，如何搭配PicGo实现快速上传图片到个人图床

> 我们搭建的免费图床，所有用户均已支持高速云存储，
>
> 限时免费开放使用中，有需求的欢迎试用：[设计图床](https://pic.shejibiji.com/)

![R_22-04-18-20-07-41_80_1080PX](https://pic.shejibiji.com/i/2022/04/18/625d54d516b6f.jpg)

兰空图床(Lsky Pro)新版本V2图床带来了很多特性，速度也得到明显提升，而且自带API接口，可以配合PicGo，实现快速批量上传图片到个人账户下。

兰空图床(Lsky Pro)V2版本接口采用 「HTTP 基本验证」的方式验证授权，获取到 token 后，通过设置请求 header 标头来验证请求。

所以token的获取就稍微要麻烦一点。

接下来就结合[设计图床](https://pic.shejibiji.com/)，配合**Postman**在线工具，来具体演示下如何获取Token，以及正确搭配**PicGo**来使用的方法。

## 一、获取Token

我们首先来讲如何获取[设计图床](https://pic.shejibiji.com/)的个人Token，以及Postman具体使用方法。

不知道Postman是什么的可以看站内文章：[《API调试工具Postman介绍》](https://www.shejibiji.com/archives/8409)

1、

**首先我们打开图床的接口页面**:

[设计图床API](https://pic.shejibiji.com/api)

![image-20220418192814109](https://pic.shejibiji.com/i/2022/04/18/625d4b4dbe33f.png)

这里有接口说明，可以大概看一下具体的获取方法。

2、

**发起请求，生成token**

根据接口说明，可以看到我们需要通过api 调试工具发起一个 http post 请求来生成一个 token。

这里我们使用postman调试工具，个人使用基本上是免费的。

postman官网：https://www.postman.com/

打开后，可以填入邮箱，然后再按照要求填入账号密码即可完成注册：

![image-20220418193256775](https://pic.shejibiji.com/i/2022/04/18/625d4c687a249.png)

登陆后我们来到个人工作台，在左边我们可以新建一个项目：

![image-20220418193653771](https://pic.shejibiji.com/i/2022/04/18/625d4d5569c8b.png)

我们修改请求类型为：`POST`，并填入我们的请求 url：`https://pic.shejibiji.com/api/v1/tokens`

![image-20220418193912337](https://pic.shejibiji.com/i/2022/04/18/625d4de000a20.png)

然后我们在头（Headers）里面，设置请求头KEY为 `Accept` ，值为 `application/json`，如下图：

![image-20220418185646327](https://pic.shejibiji.com/i/2022/04/18/625d467eaefe4.png)

在请求体（Body）中，我们分别填入邮箱和密码的KEY和对应的值。

KEY按照我们示例的填写，分别为：`email`和`password`

值VALUE为您的注册邮箱和您的登录密码，如下图：

![image-20220418185720255](https://pic.shejibiji.com/i/2022/04/18/625d4680cbe64.png)

填好之后，就可以点击右边的`Send`按钮，发起请求：

![image-20220418194431577](https://pic.shejibiji.com/i/2022/04/18/625d4f1f3ba7b.png)

稍微等待一会，在下方就可以看到返回的结果，token的值就是我们需要的内容了。

![image-20220418185735352](https://pic.shejibiji.com/i/2022/04/18/625d4682acab8.png)

保存好token值，接下来要用到。

## 二、配置PicGo

1、

**下载PicGo上传插件**

我们首先打开PicGo，然后在`插件设置`里面搜索`lankong`找到插件，点击安装，等待安装完成。

![image-20220418194720605](https://pic.shejibiji.com/i/2022/04/18/625d4fc83a3d7.png)

2、

**配置插件完成设置**

在`图床设置`下面找到`lankong`，打开插件的设置界面。

我们选择`Version`为`V2`

在`Server`一栏，填入我们的网址：`https://pic.shejibiji.com`

然后在token一栏，我们填入`Bearer`加上之前获取的token，形如：`Bearer 1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5`

注意 Bearer 和 返回的 token 之间有个空格，请严格按照格式填写。

![image-20220418194938335](https://pic.shejibiji.com/i/2022/04/18/625d5051ee1d1.png)

点击确定，就可以了。这样就配置好了PicGo。



现在我们在上传区，拖入图片就可以成功上传图片啦！

![image-20220418195359394](https://pic.shejibiji.com/i/2022/04/18/625d51570c448.png)

PicGo还可以搭配其它工具如Typora使用，具体方法可以参考之前的文章：

[《如何在Typora中利用PicGo.APP实现粘贴图片快速上传》](https://www.shejibiji.com/archives/8228)

