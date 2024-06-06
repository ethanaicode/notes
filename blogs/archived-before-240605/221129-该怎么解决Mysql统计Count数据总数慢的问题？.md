# 该怎么解决Mysql统计Count数据总数慢的问题？

![Vida_2022-11-29_11-50-21](https://pic.shejibiji.com/i/2022/11/29/6385818960e97.jpg)

## 问题描述：

　　有一个mysql数据表，想去统计一下具体有多少行数据，于是就使用了 SELECT COUNT(url_id) FROM `spider_71_ggzy_zgzfcgw_content`    查询了好久也没有出来，有什么解决办法呢？

![01](https://pic.shejibiji.com/i/2022/11/29/638580a0550e4.png)　　

## 查询速度慢的 原因是什么？

innodb引擎在统计方面和myisam是不同的，Myisam内置了一个计数器，所以在使用 select count(*) from table 的时候，直接可以从计数器中取出数据。而innodb必须全表扫描一次方能得到总的数量。

###  解决方案一：使用索引查询数据　　

![02](https://pic.shejibiji.com/i/2022/11/29/638580b100e8a.png) 

我们添加了添加查询 WHERE url_id > 0，查询速度20s就出来结果了。url_id 是 NORMAL 索引类型

 ### 解决方案二：用下载代替查询

好多时候查询不如下载数据，这次我们用下载代替查询。

![03](https://pic.shejibiji.com/i/2022/11/29/638580ba34141.png)　　

153s出结果，速度相对于全扫描查询快多了！