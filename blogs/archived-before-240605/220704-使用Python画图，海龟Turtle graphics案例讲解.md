# 使用Python画图，海龟Turtle graphics案例讲解

> 官方文档：https://docs.python.org/3/library/turtle.html

最近在学习Python时，发现有人介绍这个官方自带的海龟图形包，可以使用简单的命令画出图形，还是很有趣的！而且它的整个逻辑和现实中拿笔绘画很像，所以也比较好理解，以下是我这次学习的笔记：

## 介绍

Turtle graphics(海龟图形)是向**孩子们**介绍编程的一种流行方式。 它是由 Wally Feurzeig、Seymour Papert 和 Cynthia Solomon 在 1967 年开发的原始 Logo 编程语言的一部分。

*所以Turtle graphics比较适合入门，当并不适合实际开发使用*

官方提供了这样一个案例和代码，大家也可以自己试一下：

![1656906011912.png](https://img.shejibiji.com/2022/07/04/62c2611d9fd7e.png)

```python
from turtle import *
color('red', 'yellow')
begin_fill()
while True:
    forward(200)
    left(170)
    if abs(pos()) < 1:
        break
end_fill()
turtle.hideturtle()
done()
```

## 简单案例入门

第一步自然是要导入包。

因为是python自带的包，所以直接导入即可，使用以下命令：

```python
import turtle
```

接下来开始尝试。

首先是**画直线**。

我们可以用`turtle.forward(200)`来画出一条200像素的线段（默认方向从左到右）：

![2022-07-04_11-48-17](https://pic.shejibiji.com/i/2022/07/04/62c2630da8f83.jpg)

当然我们也可以让**线条转弯**。

使用`turtle.left(90)`即可实现左转90度。

结合上面的画线段，就可以方便的画出正方形，完整代码如下：

```python
import turtle

turtle.forward(100)
turtle.left(90)
turtle.forward(100)
turtle.left(90)
turtle.forward(100)
turtle.left(90)
turtle.forward(100)
turtle.left(90)
```

![2022-07-04_11-52-31](https://pic.shejibiji.com/i/2022/07/04/62c26409b28ab.jpg)

（有基础的小伙伴可以使用for循环实现这个，代码会更简单些）

接下来我们尝试画**两个圆**。

画一个100像素直径的圆命令为：`turtle.circle(100)`。

画两个圆就重复这个命令即可，比如这样：

```python
import turtle

turtle.circle(100)
turtle.circle(60)
```

运行后结果是这样的：

![2022-07-04_11-57-28](https://pic.shejibiji.com/i/2022/07/04/62c2652e8fe30.jpg)

如果我们想要让小圆到大圆中间去改怎么做呢？

思路很简单，当第一个圆画好后，我们应该让箭头改变位置，再画圆即可。

改进下代码：

```python
import turtle

turtle.circle(100)
turtle.left(90) # 左转进入大圆内部
turtle.forward(40)
turtle.right(90) # 记得笔的方向要调回来
turtle.circle(60)
```

效果如下：

![2022-07-04_12-02-44](https://pic.shejibiji.com/i/2022/07/04/62c26669ec2ef.jpg)

看起来是这个意思了。

但是我们不想大圆和小圆中间有线条连接，这个时候就要考虑加入**抬笔**的动作。

抬笔命令为：`turtle.penup()`

落笔命令为：`turtle.pendown()`

我们继续优化下之前的命令：

```python
import turtle

turtle.circle(100)
turtle.penup() # 加入抬笔的动作
turtle.left(90)
turtle.forward(40)
turtle.right(90)
turtle.pendown()
turtle.circle(60)
```

现在就差不多了。



那么如果我们想**填充**内部的圆形，该如何操作呢？

可以使用填充命令：`turtle.fillcolor('blue')`

但是计算机是比较傻的，我们还要告诉计算机什么时候开始填充，什么时候结束，这个时候要用到命令：

开始填充：`turtle.begin_fill()`

结束填充：`turtle.end_fill()`

前面的代码就可以改成这样：

```python
import turtle

turtle.circle(100)
turtle.penup()
turtle.left(90)
turtle.forward(40)
turtle.right(90)
turtle.pendown()
turtle.fillcolor('blue')
turtle.begin_fill()
turtle.circle(60)
turtle.end_fill()
```

我们运行一下：

![2022-07-04_12-12-23](https://pic.shejibiji.com/i/2022/07/04/62c268b5531ac.jpg)

另外我们也可以改变线条的颜色和粗细，命令分别为：`turtle.pensize(1)`和`turtle.pencolor('red')`

学会了这些，我们就可以画出一个稍微复杂的图形了。



比如我们想画一个美国队长的盾牌图案，就可以用以下代码：

```python
import turtle

# 绘制大圆
turtle.pensize(5)
turtle.pencolor('red')
turtle.circle(105)
# 移动位置
turtle.left(90)
turtle.penup()
turtle.forward(50)
turtle.pendown()
turtle.right(90)
# 绘制小圆并填充
turtle.pensize(8)
turtle.fillcolor('blue')
turtle.begin_fill()
turtle.circle(55)
turtle.end_fill()
# 移动位置，并更换笔
turtle.pensize(1)
turtle.pencolor('white')
turtle.fillcolor('white')
turtle.penup()
turtle.left(90)
turtle.forward(70)
turtle.left(90)
turtle.forward(48)
turtle.left(180)
turtle.pendown()
# 绘制五角星并填充
turtle.begin_fill()
i = 0
while i < 5:
    turtle.forward(100)
    turtle.right(144)
    i += 1
turtle.end_fill()
# 隐藏箭头
turtle.hideturtle()
```

运行代码后结果就是这样：

![2022-07-04_12-16-58](https://pic.shejibiji.com/i/2022/07/04/62c269ca6b30f.jpg)

是不是还挺有趣的！



掌握了以上这些命令，一般的图形就都可以画出了，只是复杂程度不一样而已。

网上也有很多复杂图形的案例，但都是这些简单命令的重复，有兴趣的可以继续多多尝试下。