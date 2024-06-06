# 如何使用CNAMEs自定义亚马逊Amazon S3访问域名

<img src="http://ossimg.yzitc.com/2021/11/30/d9373a8971536.png" alt="1638253525635.png" title="1638253525635.png" />

最近尝试了下亚马逊Amazon的对象存储服务S3，操作逻辑类似阿里云的OSS，没什么难度，但是因为翻译的问题很多词都不是很好理解什么意思，有点尴尬……

也不知道国外人的逻辑是不是不同，很多操作做的就有点“不人性化”，比如自定义访问域名，就没有一个明确的入口。

找了半天官方文档，才看到有个说到这个的。

以下是官方原文：

原文链接：[VirtualHostingCustomURLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/VirtualHosting.html#VirtualHostingCustomURLs)

<img src="http://ossimg.yzitc.com/2021/11/30/ddd4154a02f30.png" alt="1638252820858.png" title="1638252820858.png" />

大概意思就是你设置的桶的名字必须与你的CNAME相同。

比如你的自定义域名是：`images.yzitc.com`，那么你桶的名称就得是：`images.yzitc.com`，然后再CNAME到http://`images.yzitc.com`.s3.`Region`.amazonaws.com/

注意其中的`Region`，是区域信息。

这样设置后，就完成了自定义域名`images.yzitc.com`的设置。

（以上仅作记录，可能写的不详细，有问题可以下方留言）