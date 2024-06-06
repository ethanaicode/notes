# screw plus加密php代码

```
git clone https://git.oschina.net/splot/php-screw-plus.git
```

![R_22-05-16-16-41-26_80](https://pic.shejibiji.com/i/2022/05/16/628258c4c61fc.jpg)

执行php的**phpize**文件

![R_22-05-16-16-51-06_80](https://pic.shejibiji.com/i/2022/05/16/6282595573ca1.jpg)

![R_22-05-16-17-01-54_80](https://pic.shejibiji.com/i/2022/05/16/6282596e9517c.jpg)

![R_22-05-16-17-04-14_80](https://pic.shejibiji.com/i/2022/05/16/62825975501e3.jpg)

配置命令为 **./configure --with-php-config=[php-config]**, [php-config]一般也在php的bin目录下，写绝对路径就可以了。

![R_22-05-16-17-05-04_80](https://pic.shejibiji.com/i/2022/05/16/628259937b9af.jpg)

```
vi php_screw_plus.h
```

![R_22-05-16-17-07-07_80](https://pic.shejibiji.com/i/2022/05/16/628259ac440de.jpg)

修改完毕之后，直接开始编译，执行make命令，如果最后显示Build complete.说明编译成功，扩展在modules里面，如果报错请根据提示进行修复，然后make clean之后重新编译。

![R_22-05-16-17-17-59_80](https://pic.shejibiji.com/i/2022/05/16/628259d744e73.jpg)

进入tools目录执行make命令即可。如果没有报错，则扩展就全部编译完成了。

![R_22-05-16-17-18-31_80](https://pic.shejibiji.com/i/2022/05/16/628259f2494b3.jpg)

修改php的配置文件

![R_22-05-16-17-23-03_80](https://pic.shejibiji.com/i/2022/05/16/62825a001b14c.jpg)

phpinfo

![R_22-05-16-17-56-46_80](https://pic.shejibiji.com/i/2022/05/16/628258edc8ca4.jpg)

![R_22-05-16-17-56-25_80](https://pic.shejibiji.com/i/2022/05/16/628258f396988.jpg)

加密后的文件

![R_22-05-16-17-59-13_80](https://pic.shejibiji.com/i/2022/05/16/628258fe173e7.jpg)