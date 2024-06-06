# PicGo无法上传图片，RequestError错误解决方法

![image-20211201165730331](https://ossimg.yzitc.com/2021/12/01/80d43c8ce5b03.png)

最近把公司的电脑搬到家里开始工作了。

公司电脑配置还不错，比家里的16年自己装的B150主板电脑好太多了，于是就这样开始干活了。

之前的那种每日自由自在的日子一去不复返了。



其它都挺好，因为自己习惯资料都放在云端同步，基本上换了电脑就可以直接开始工作，不影响使用。

只是typora上传图片用的PicGo似乎出问题了，无法正常上传图片，总是报：**RequestError**

全文是这样的：

> RequestError: Error: tunneling socket could not be established, cause=getaddrinfo ENOTFOUND 7890

![2022-06-12_22-02-52](https://pic.shejibiji.com/i/2022/06/12/62a5f38419340.jpg)

![2022-06-12_22-03-38](https://pic.shejibiji.com/i/2022/06/12/62a5f3ce12d74.jpg)<font>Typora也无法使用了</font>

我研究了半天，更换图床，设置Server，都无法成功。

仔细看了半天的PicGo错误日志，也没看懂有啥错误：

![2022-06-12_22-11-32](https://pic.shejibiji.com/i/2022/06/12/62a5f41b691ea.jpg)

不过根据错误，大概能看出是端口的问题。

于是我又尝试关闭梯子，或者改变梯子的端口都没解决问题。

说了半天，只是想记录下这次解决问题的过程，下面提供解决方法：

### 解决方法

首先我们打开系统的网络代理，查看代理服务器地址：

![2022-06-12_22-04-15](https://pic.shejibiji.com/i/2022/06/12/62a5f4e88da5b.jpg)

比如从上图可知我的代理服务器为`127.0.0.1:7890`

然后再在PicGo中设置代理和镜像地址，修改其**上传代理**为我们刚刚获取的代理服务器地址。

![2022-06-12_22-04-21](https://pic.shejibiji.com/i/2022/06/12/62a5f52dab308.jpg)

现在就可以正常上传图片了。

![2022-06-12_22-04-30](https://pic.shejibiji.com/i/2022/06/12/62a5f56dce028.jpg)

虽然这个应该也解决不了所有的RequestError错误，但也是比较有代表性的问题了，希望可以提供一些帮助。