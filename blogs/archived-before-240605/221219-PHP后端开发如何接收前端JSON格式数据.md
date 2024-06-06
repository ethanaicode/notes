# PHP后端开发如何接收前端JSON格式数据

> 一句话回答：用 php://input，可以看下图

![R_22-12-19-19-41-33_80](https://pic.shejibiji.com/i/2022/12/19/63a04df5a1fa8.jpg)

当请求的请求头格式为`application/json`时，即在传递过程中，请求将JSON格式的参数放在request的body中，后端在接收时我们可以使用`file_get_contents('php://input')`方法或`$_POST`以获取参数值。

但是PHP 默认只识别 `application/x-www.form-urlencoded` 标准的数据类型，因此，对`text/xml`或者`soap` 或者 `application/octet-stream` 之类的内容无法解析，如果用 `$_POST` 数组来接收就会失败。

### 两种方式区别与简介

**（1）php://input 介绍**

php://input 是个可以访问请求的原始数据的只读流。

**（2）$_POST和 $_GET介绍**

`$_POST:` 变量是一个数组，内容是由 HTTP POST 方法发送的变量名称和值。

`$_POST:` 变量用于收集来自 method=”post” 的表单中的值。
从带有 POST 方法的表单发送的信息，对任何人都是不可见的（不会显示在浏览器的地址栏），并且对发送信息的量也没有限制

`$_GET:` 参数都出现在url上，可以用于翻页，简单查询，get只能接收2M以下的内容，所以有局限性，另外由于内容是可见的，安全性就下降了

总的来说，$_GET和 $_POST是PHP对 post 和 get 请求参数的两种存储的全局变量

**（3）php://input 与 $_POST 的使用场景比较**

只有 `Coentent-Type` 为 `application/x-www-data-urlencoded` 和 `multipart/form-data` 情况下，PHP 才会将 http 请求数据包中相应的数据填入全局变量 `$_POST`。
只有 `Coentent-Type` 为 `multipart/form-data` 的时候，PHP 不会将 http 请求数据包中的相应数据填入 `php: //input`，其余情况都会。