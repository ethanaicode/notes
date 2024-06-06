# Git给不同的分支配置不同的remote远程仓库地址

公司自建了gitlab本地仓库，使用起来是挺好。

但是我发现，回家之后就无法继续push代码到本地仓库了，因为公司的gitlab仓库是建在局域网的。

虽然可以直接copy一份代码带回去继续做，但是不能随时push代码，体验就差了些，于是就在想该怎么解决这个问题。

最终决定自己在gitlab.com新建一个仓库，然后在公司的时候，提交代码到本地gitlab仓库时，也提交一份到这个公共仓库。

逻辑大概是这样的：

[![gitlab diagrams.png](https://img.shejibiji.com/2023/02/21/63f3a256b38af.png)](https://img.shejibiji.com/2023/02/21/63f3a256b38af.png)

这样就可以在家里继续开发了。

那么问题来了，**该如何为不同的branch分支设置不同的远程仓库呢？**

其实只要修改下`.git/config`这个git配置文件即可。

我们首先准备两个远程仓库，然后在配置文件中，为不同的分支，设置不同的`remote`值即可：

[![1676911578594.png](https://img.shejibiji.com/2023/02/21/63f3a3dd637ec.png)](https://img.shejibiji.com/2023/02/21/63f3a3dd637ec.png)

主要就是要修改分支下面的`remote`后面的参数。

这样就可以顺利实现啦！