# 详解 htop，如何使用 htop 命令监视系统进程和资源使用

> 本文详细介绍了 linux 中 htop 命令的使用方法，如果你发现这个命令不可用，可以先安装 htop。

## 介绍

`htop`是`top`命令的更漂亮、更丰富色彩、略微更更新的版本。

在`top`中，一些指标如“steal”和“iowait”更容易看到，但对于大多数其他目的，`htop`可能是更好的工具，用于解决服务器性能问题。

就像`top`一样，这是一个很好发展的工具，用于您诊断网站和服务器上的任何性能问题。一旦您掌握了基础知识，使用起来很容易。

本文的目标是让您能够在服务器上运行`htop`命令并理解其显示的信息。拥有这些信息，您将能够排除您发现的任何性能问题。

##  “htop”能显示什么？

`htop`会实时显示服务器上发生的情况概览。简而言之，您可以一目了然地看到以下内容：

1. 服务器上各个CPU的数量及其资源使用情况逐个列出；
2. 按进程、缓存和磁盘缓存分解的RAM使用情况；
3. 交换空间使用情况；
4. 总任务数、线程计数和运行任务数；
5. 1分钟、5分钟和15分钟的负载平均值；
6. 系统正常运行时间和当前时间（默认为UTC时间）；
7. 运行进程的详细情况。

![htop-2.0](https://pic.shejibiji.com/i/2024/05/11/663ef78453c33.png)

##  入门指南

**关于系统用户的说明** - 我们强烈建议为您的每个网站分配一个独立的系统用户。这不仅重要的是保持您的网站彼此隔离（一个被黑客/恶意软件感染的网站不会影响到另一个系统用户上的网站），而且它还会显示在USER列中，因此您可以轻松地使用`top`或`htop`来识别任何资源使用率高的站点。

例如，如果我的网站分配给了一个名为“steve-com”的系统用户，您将在USER列中看到用户“steve-com”，并且知道需要查看哪个站点。如果它们都在同一个系统用户下，您将无法确定发生了什么。

一旦进入您的服务器，请运行：

```
htop
```

要退出`htop`，请使用**Q**或**CTRL+C**。

##  第一部分、htop 顶部总览

开头的总览区域是系统概览。下面我们将逐个部分解释各部分含义。

### CPU 概览

![img](https://pic.shejibiji.com/i/2024/05/11/663eebb633b16.png)

在这里，使用数字1和2，我们可以看到这是一个双核VPS。一个四核将会有4个条，八核将会有8个条，依此类推。每个数字/条代表一个CPU。每个条的右侧有一个百分比，表示正在使用的CPU量。

然后，具体的CPU使用情况通过以下颜色代码进行分解：

- **蓝色：** 低优先级进程使用的CPU百分比
- **绿色：** 用户进程使用的CPU百分比
- **红色：** 系统/内核进程使用的CPU百分比

额外的信息：

- **黄色/橙色：** IRQ时间使用的CPU百分比
- **品红色：** 软IRQ时间使用的CPU百分比
- **灰色：** IO等待时间使用的CPU百分比
- **青色：** 虚拟化环境下的CPU偷窃时间使用的CPU百分比

在本文中，条状图大部分是空的，这意味着CPU大部分时间处于空闲状态。

您的CPU使用率越高（满条、百分比更高），您的系统就越繁忙，这将影响到您网站的性能。

短时间内的高使用率是正常的，无需担心。持续高CPU使用率是需要进一步关注的。

### RAM 和 SWAP 概览

![img](https://pic.shejibiji.com/i/2024/05/11/663eebbd0e046.png)

这部分显示了系统的内存使用信息。

我们有RAM和Swap - Swap是硬盘的一部分，像RAM一样被服务器使用。这就是为什么保留足够的磁盘空间对您的系统至关重要，以及为什么当您的磁盘空间使用量超过90%时可能会出现性能问题。

RAM使用情况通过颜色进行分解。

1. **绿色：** 已使用的内存页
2. **蓝色：** 缓冲页（Buffer pages）
3. **黄色：** 缓存页（Cache pages）

Swap空间是您的安全网，如果RAM用尽，它会发挥作用。高交换和RAM使用率将影响系统有效处理任务的能力，可能导致 504 超时错误。进程会变慢，并在等待内存可用时积压。

### Tasks

![img](https://pic.shejibiji.com/i/2024/05/11/663eebc29fd03.png)

通常，我们可以把“任务”和“进程”理解为相同的东西。在这里，我们有44个总进程，其中有1个正在运行。100个“thr”代表“线程”。因此，在这里，我们有44个任务，分解成了100个线程。

### LOAD AVERAGE

![img](https://pic.shejibiji.com/i/2024/05/11/663eebc7344a1.png)

简而言之，在这里，我们可以看到过去一分钟、五分钟和十五分钟的平均“负载”。

负载是按CPU计算的，因此如果您有多个核心，您需要将所见的结果除以服务器运行的核心数。持续的高负载时间意味着您的服务器一直很忙碌。这可能是由于多种原因造成的，例如高流量网站或暴力攻击。`htop`提供的其余数据应该有助于填补这些空白。

### 系统正常运行时间和当前系统时间

在这里，您可以看到服务器已经在线的时间以及当前的系统时间。对于我们的目的来说，这并不特别重要。

## 第二部分、活动进程

现在您已经一目了然地了解了服务器上正在发生的情况。如果您看到资源使用率很高，现在我们需要查看进程本身，以确定是什么造成了这种情况。

活动进程列表位于概览的下部。如下所示：

![Ethan_2024-05-11_11-55-13](https://pic.shejibiji.com/i/2024/05/11/663eec906f657.jpg)

以下是每个列的解释：

- **PID：** 显示任务的唯一进程ID；

- **USER：** 启动任务的用户的用户名；

- **PRI：** 显示任务的调度优先级；

- **NI：** 表示任务的nice值；

  我们在第2部分CPU部分已经涵盖了这一点。Nice影响任务的优先级 - 19表示最低优先级，-20表示最高优先级。

- **VIRT：** 显示任务使用的内存总量；

- **RES：** 显示进程在RAM中消耗的内存（以kb为单位）；

- **SHR：** 表示任务使用的共享内存量（以kb为单位）；

- **S：** 进程的当前状态（僵尸、睡眠、运行、不间断睡眠或跟踪）；

- **CPU%：** 表示每个进程使用的CPU百分比；

- **MEM%：** 显示每个进程使用的总可用RAM百分比；

- **TIME+：** 任务使用的CPU时间总量，以百分之一秒为单位显示；

- **COMMAND：** 运行进程的名称。

在页面下方是 htop 的菜单项目。

## 第三部分、htop 菜单

在做任何其他操作之前，您可以使用箭头键垂直和水平滚动进程列表。

随着您了解基础知识，这将会很方便。

### 底部菜单

您可以通过按下**Esc**键退出以下任何命令。

- **F1 帮助：** 打开一个基本介绍页面，详细介绍了本节内容的许多内容
- **F2 设置：** 自定义功能 - 您可能不需要设置。
- **F3 搜索：** 打开搜索栏并搜索进程
- **F4 过滤：** 通过输入内容过滤进程（例如，通过输入“MySQL”来过滤所有MySQL任务）
- **F5 树形视图：** 以树形视图显示进程
- **F6 按列排序：** 按特定列排序进程
- **F7 提升优先级：** 通过单击任务或使用箭头键导航到任务并按F7来提高任务的优先级
- **F8 降低优先级：** 通过单击任务或使用箭头键导航到任务并按F8来降低任务的优先级
- **F9 终止：** 终止一个进程
- **F10 退出：** 关闭`htop`

### 常用快捷键

您可以通过在键盘上按下以下任何快捷键来使用它们。还有更多可用的快捷键（在`htop`内按F1获取更多详情），但是出于故障排除目的，这些是您需要学习的主要快捷键。

- **u：** 显示特定用户拥有的所有进程
- **p：** 基于CPU使用率高的进程进行排序
- **m：** 基于内存使用率高的进程进行排序
- **t：** 根据时间排序进程。
- **空格键：** 导航到进程，然后按空格键将其突出显示
- **Shift + u：** 删除所有标签
- **Shift + f：** 突出显示并跟踪一个进程。

## 第四部分、用 htop 来分析性能问题吧

在第4部分中的命令可以提供大量信息，帮助您准确定位性能问题。当您在`htop`中时，您可能会发现您经常使用**F3**、**F4**、**F9**、**u**、**p**、**m**和**t**这些命令。

我们在这里要查看的是在**COMMAND**列中使用最多**CPU%**和**MEM%**的任务。一旦我们知道了这一点，我们就可以开始进一步的诊断。

例如，如果您看到PHP使用率很高，您的服务器可能正在经历暴力攻击。使用上述命令，您应该能够缩小到一个特定的网站并相应采取行动。

高MySQL使用率可能表示数据库表锁定或缺乏适当的缓存。

> 翻译自（有删减）：https://gridpane.com/kb/how-to-use-the-htop-command-to-monitor-system-processes-and-resource-usage/