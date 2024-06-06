# Git遇到refusing to merge unrelated histories错误该怎么解决

Git遇到refusing to merge unrelated histories错误，会有两种情况，但都可以通过`--allow-unrelated-histories`来解决。

一、本地合并时遇到refusing to merge unrelated histories的错误。

如果git merge合并的时候出现refusing to merge unrelated histories的错误，原因是两个仓库不同而导致的。

需要在后面加上`--allow-unrelated-histories`进行允许合并，即可解决问题。

如果还不能解决问题，就把本地的remote删除，重新git remote add添加远程仓库，再按上面的方法来，问题解决。

二、远程push 的时候出现 refusing to merge unrelated histories

本地仓库在想做同步远程仓库到本地为之后本地仓库推送到远程仓库做准备时报错了，错误如下：

`fatal: refusing to merge unrelated histories` 
（拒绝合并不相关的历史）

出现这个问题的最主要原因还是在于本地仓库和远程仓库实际上是独立的两个仓库。

假如我之前是直接clone的方式在本地建立起远程Git仓库的克隆，本地仓库就不会有这问题了。

解决方案还是可以在pull命令后紧接着使用`--allow-unrelated-history`选项来解决问题（该选项可以合并两个独立启动仓库的历史）。