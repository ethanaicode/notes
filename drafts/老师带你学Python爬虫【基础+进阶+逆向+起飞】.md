# 老师带你学Python爬虫【基础+进阶+逆向+起飞】

[本地视频地址](E:\哔哩哔哩\Python-武沛齐\老师带你学Python爬虫【基础+进阶+逆向+起飞】)

## 一、爬虫概述

### Anacanda开发环境

**jupyter：**就是Anaconda这个集成环境提供的一个基于浏览器可视化的编码工具

*安装路径要是全英文*

## 二、requests模块

### 捕获动态加载的数据

**判断是否为动态加载**

看到这种文件，表示网页是动态加载的，我们如果直接爬取单个url是无法获取数据的。

![image-20220507181359223](https://pic.shejibiji.com/i/2022/05/07/6276466793eca.png)

预览下页面，也可以看到整个页面其实是没有内容的：

![image-20220507181512341](https://pic.shejibiji.com/i/2022/05/07/627646b09dd00.png)

**如何捕获动态加载的数据**

局部数据肯定是存在抓包工具捕获的某个或多个数据包中。

可以直接全局搜索关键词，随便点击其中一个文件，按`ctrl+F`打开全局搜索：

![image-20220507182009989](https://pic.shejibiji.com/i/2022/05/07/627647da4327f.png)

就可以搜索到对应的数据包，比如搜索**这个杀手不太冷**：

![image-20220507193604302](https://pic.shejibiji.com/i/2022/05/07/627659a48a976.png)

就可以看到返回值**Response**，大概可以看出这是个json数据。

我们打开`Headers`，就可以看到正确的请求头了：

![image-20220507193753199](https://pic.shejibiji.com/i/2022/05/07/62765a11653a0.png)

有这些数据我们就可以开始爬取：

```python
# 指定爬取地址
url = 'https://movie.douban.com/j/chart/top_list'
params = {
    'type': '5',
    'interval_id': '100:90',
    'action': '',
    'start': '0',
    'limit': '20'
}
# 发起get请求返回值为响应对象
response = requests.get(url=url, params=params, headers=headers)
# 获取相应数据
response.encoding = 'utf-8'
page_text = response.json() # json数据格式化
# 解析出电影的名称+评分
for each in page_text:
    title = each['title']
    score = each['score']
    print(title, score)
```

**如果搜索不到数据包**

原因是可能动态加载的数据是经过加密的密文数据。

## 数据解析

