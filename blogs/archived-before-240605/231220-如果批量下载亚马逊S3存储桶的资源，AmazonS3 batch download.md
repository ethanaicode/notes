# 如果批量下载亚马逊S3存储桶的资源，AmazonS3 batch download

之前有些业务用到了AWS S3来存储，但最近看着每月的账单，有点吃不消，所以想把资源转到本地存储。

查看了下 Amazon Simple Storage Service 官方指南，虽然支持下载对象，但一次只能下载一个对象。

我真的是要说谢谢🙏。

搜了下网上的资料，很多人推荐了[**cyberduck**](https://cyberduck.io/s3/)，官方介绍说可以像浏览硬盘一样浏览 Amazon Simple Storage Service，看着不错，不过我还是不想下载额外的软件，毕竟我现在只是需要临时批量下载。

于是另外一个主角就要登场了：**AWS CLI**

这是Amazon AWS自己的命令行工具，