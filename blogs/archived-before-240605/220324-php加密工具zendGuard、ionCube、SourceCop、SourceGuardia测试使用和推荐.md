# php加密工具zendGuard、ionCube、SourceCop、SourceGuardia测试使用和推荐

最近遇到一个非常不爽的主题作者，恶意关闭我的网站后倒流到自己网站。

联系解决，就要加钱，明明我是正版用户却跟孙子似的，真的是大写的无语。

于是就好奇研究了下他的主题加密方法。

因为主题要加载一个`loader.so`的文件，大概能推测出加密工具。

以下是测试的几款php加密工具：

## 测试

### zendGuard

<a href="http://www.zend.com/store/products/zend-encoder.php" data-wpel-link="external" rel="nofollow">Zend Encoder</a> 的架构已经非常老旧，价格昂贵而且更新速度慢，还任由<a href="http://www.zend.com/phorum/list.php?num=8" data-wpel-link="external" rel="nofollow">讨论区</a>让广告覇佔，也难怪反 Zend 的 user 愈来愈多。

<a href="https://ossimg.yzitc.com/2022/03/24/86b5a85487e09.gif" data-wpel-link="internal"><img alt="20051125_05.gif" src="https://ossimg.yzitc.com/2022/03/24/86b5a85487e09.gif" width="388" height="280" border="0"></a>
(Zend Encoder 官方讨论区形同废墟，满满的都是广告)

Zend Encoder 目前市价为 US$960、SafeGuard Suite  更是到 <a href="http://www.zend.com/store/products/zend-safeguard-pricing.php" data-wpel-link="external" rel="nofollow">US$2,920</a> 以上的天价，而且 US$2,920 还只能使用一年。但由于破解档流通快速，早期也是加密 PHP 的最佳解决方案，因此可以说是市佔率第一名的 PHP 原始码加密软件，连虚拟主机商也为了要执行 Zend 加密过的档案，不得不纷纷安装 Zend Optimizer 。

直到现在 Zend 对于 Encoder 的态度消极已经是众所皆知，久久才出现一次新版本，因此也开始让其它的 Encoder 冒出头了。

到上个月Zend Encoder 破解的消息甚嚣尘上，更是让对于想保护自己 PHP 原始码的公司及设计师开始寻求替代方案。

由于目前大部份的虚拟主机都已安装 Zend Optimizer (Zend Encoder 的执行环境)，因此本次 PHP 原始码加密软件的测试重点为“不需在服务器设定或安装任何软件”。

### ionCube  Standalone Encoder (US$199 起)

<a href="http://www.ioncube.com/sa_encoder.php?xp=NXEZWA" data-wpel-link="external" rel="nofollow">http://www.ioncube.com/sa_encoder.php</a>

<a href="http://www.ioncube.com?xp=NXEZWA" data-wpel-link="external" rel="nofollow">ionCube</a> 在国外已经是软件公司取代 Zend Encoder 的不二选择，知名的 PHP 购物车 <a href="http://www.x-cart.com" data-wpel-link="external" rel="nofollow">X-Cart</a> 就是採用 <a href="http://www.ioncube.com/sa_encoder.php?xp=NXEZWA" data-wpel-link="external" rel="nofollow">ionCube Standalone Encoder</a> 加密原始码。服务器端不需安装任何软件，只要把  Loader 放在程式的目录裡面就可以了。

<a href="https://ossimg.yzitc.com/2022/03/24/1b154a65558d1.gif" data-wpel-link="internal"><img alt="20051125_01.gif" src="https://ossimg.yzitc.com/2022/03/24/1b154a65558d1.gif" width="388" height="360" border="0"></a>
(Windows+IIS 下执行加密过后的 phpinfo(); )

<a href="https://ossimg.yzitc.com/2022/03/24/8478a9d71ad8a.gif" data-wpel-link="internal"><img alt="20051125_02.gif" src="https://ossimg.yzitc.com/2022/03/24/8478a9d71ad8a.gif" width="388" height="347" border="0"></a>
(Linux+Apache 下执行加密过后的 phpinfo(); )

### SourceCop (US$30)

<a href="http://www.sourcecop.com/" data-wpel-link="external" rel="nofollow">http://www.sourcecop.com/</a>

服务器完全不用外挂任何 Loader 及 Module，完全用 PHP 的方式来加密程式，有点功力的人追踪一下就能看出编码方式了，所以只能防君子不能防小人。

<a href="https://ossimg.yzitc.com/2022/03/24/9ef05f1172b6a.gif" data-wpel-link="internal"><img alt="20051125_03.gif" src="https://ossimg.yzitc.com/2022/03/24/9ef05f1172b6a.gif" width="388" height="92" border="0"></a>
(编码后的程式)

<a href="https://ossimg.yzitc.com/2022/03/24/1465c2c1f4f55.gif" data-wpel-link="internal"><img alt="20051125_04.gif" src="https://ossimg.yzitc.com/2022/03/24/1465c2c1f4f55.gif" width="388" height="216" border="0"></a>
(sourcecop 的解码载入程式)

注:<a href="http://www.networksecuritytech.com/viewtopic.php?t=3854&amp;postdays=0&amp;postorder=asc&amp;start=10" data-wpel-link="external" rel="nofollow">这边</a>也有人有说明将原始码还原的方式。

### SourceGuardian(US$250)

这家应该算是相当知名的PHP加密软件，不过服务器端需要外挂 Loader，因此其它测试省略。

测试结果: (失败! 需安装 Loader)

<blockquote>PHP script <b>i.php</b> is protected by <a href="http://www.sourceguardian.com/">SourceGuardian</a> and requires the SourceGuardian loader <b>ixed.4.3ev.win</b>. The SourceGuardian loader has not been installed, or is not installed correctly. Please visit the <a href="http://www.sourceguardian.com/ixeds/">SourceGuardian php encoder</a> site to download required loader.
</blockquote>

### phpShield ( US$99)

<a href="http://www.phpshield.com" data-wpel-link="external" rel="nofollow">http://www.phpshield.com</a>

操作就跟一般的 Encoder 一样简单，因为 phpShield 跟 SourceGuardian 的试用流程、Email 内容、画面、压缩档都一模一样，有可能是 SourceGuardian 的简易版，因为我没用过旧版，也有可能是 SourceGuardian 的旧版便宜卖。

测试结果: (失败! 需加装 Loader，讯息也同SourceGuardian  )

<blockquote>PHP script <b>phpinfo.php</b> is protected by <a href="http://www.phpshield.com/">phpSHIELD</a> and requires file <b>phpshield.4.3.11ev.win</b> or <b>phpshield.4.3ev.win</b>.
Please read <a href="http://www.phpshield.com/loaders/">phpSHIELD protected scripts manual</a>.
</blockquote>

## 总结

<a href="http://www.ioncube.com/sa_encoder.php?xp=NXEZWA" data-wpel-link="external" rel="nofollow"> ionCube Standalone Encoder</a> 不论功能性、方便性都是几个当中最好的，而且不需在服务器端安装任何软件，在预算许可的范围下 <a href="http://www.ioncube.com/sa_encoder.php?xp=NXEZWA" data-wpel-link="external" rel="nofollow">ionCube Standalone Encoder</a> 的确是最好的选择。

如果不介意主机需安装载入器，只是要单纯保护程式码不妨选择 phpShield 。