# 电影电视剧动漫 标准命名规则，jellfin、emby、kodi都适用

![image-20220210135201517](https://ossimg.yzitc.com/2022/02/10/126f10e6581cd.png)

搭建了电影墙之后，当然就需要下载很多内容。

下载内容多了以后，就会涉及整理的问题。比如有多季多集的剧集，多个不同清晰度不同年份的同名电影。

为了可以得到好的使用体验，我们必须要按照标准方式对影视文件及其文件夹进行规范命名，使媒体库软件可以正确地识别文件。

### 电影类

在括号的末尾加上年份会是最好的，这样避免同名电影识别错误。

**推荐的命名方式和目录结构：**

```
\电影目录\遗孀秘闻 (2019)\遗孀秘闻 (2019).mkv
\电影目录\大侦探福尔摩斯 (2009)\大侦探福尔摩斯 (2009).mp4
\电影目录\人肉农场 (2018)\人肉农场 (2018).mkv
```

### 电视剧类

不管电视剧（动漫）是否只有一季，一定要创建一个“Season 1”的文件夹，不然刮削的时候不能搜到每一集的介绍。

**剧集比较规范的方式：**

```
S01E01-海贼王.mkv
```

### 字幕命名规则

**推荐结构可以这样：**

```
/电影目录
 ``/300 (2006)
  ``/300 (2006).mkv
  ``/300 (2006).srt
  ``/300 (2006).default.srt
```

可以通过.default在文件名末尾附加字幕来将字幕标记为默认字幕。

### 多版本内容

**推荐类似下面这个结构：**

```
/电影目录
 ``/300 (2006)
  ``/300 (2006) - 1080p.mkv
  ``/300 (2006) - 4K.mkv
  ``/300 (2006) - 720p.mp4
  ``/300 (2006) - 特典版.mp4
  ``/300 (2006) - 导演剪辑版.mp4
  ``/300 (2006) - 3D版.mp4
```

为了区分版本，每个文件名都需要有一个空格，连字符，空格和一个标签。标签不是预先确定的，可以由用户制作。（注意：连字符是必需的。不支持句号，逗号和其他字符。）

### 拆分分段的视频

早期VCD分段视频形式

**推荐的一个命名结构：**

推荐使用：-cd1

```
Movies\Avatar (2009)\Avatar (2009)-cd1.mkv

Movies\Avatar (2009)\Avatar (2009)-cd2.mkv
```

### 特别篇命名

推荐建立一个文件夹：**Specials**，存放这些特别篇。

这里还有这些识别词（Season 0，Season 00，Specials）。

**下面是一个命名结构：**

```
Anime\海贼王\Specials\S00E01-海贼王.mkv
```

![image-20220210135109226](https://ossimg.yzitc.com/2022/02/10/d847076576950.png)

### 常见的英文缩写

*视频格式什么的不包括，仅列出常见的缩写*

S1 → Season 1（第一季）

SP → Specials（特别内容）

HD → Hign Definition Television（HDTV高清）

HR-HDTV → HDTV画质的一半（前面的HR是half）

BD → Blu-ray Disc（蓝光）

 X264/HEVC → 视频编码方式

 AAC → 音频编码

CHS → 简体中文

RMVB → 内嵌字幕的版本

OST → 影视原声集

TS → 枪版，声音是通过单独耳机接口录下来

Director’s Cut → 导演剪辑版

Unrated → 未分级版

Extended → 加长版

### 推荐影片数据库

**TMDB电影数据库**

https://www.themoviedb.org/

（可以切换中英文，切换为英文后，照样可以用中文搜索）

### 推荐的官方文档

**Emby官网的说明：**

电影命名规则：https://support.emby.media/support/solutions/articles/44001159102-movie-naming

电视命名规则：https://support.emby.media/support/solutions/articles/44001159110-tv-naming

**Kodi官方Wiki：**

电影命名规则：https://kodi.wiki/view/Video_library

电视命名规则：https://kodi.wiki/view/PVR