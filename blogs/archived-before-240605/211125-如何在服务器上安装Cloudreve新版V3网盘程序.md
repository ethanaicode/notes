# 如何在服务器上安装Cloudreve新版V3网盘程序

<p>刚解决了自建图床问题，也感受到了阿里云对象储存OSS的奇妙。</p>
<p>所以我就想既然解决了图片问题，那么如果是视频的话，该怎么解决呢？</p>
<p>有没有更好的办法，可以实现上传视频，在线播放，并快速下载呢？</p>
<p>于是我想到了网盘程序！</p>
<p>之前有收藏过多个网盘程序，比如Kiftd、蓝眼云盘等。</p>
<p>但在看了多个网盘程序后，最终选择了Cloudreve。原因无他，这界面也太简洁好看了吧。</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/853e926b592ca.png" alt="1637822763060.png" title="1637822763060.png" /></p>
<p>但是Cloudreve 升级到新版V3后，安装会比较麻烦。</p>
<p>网上的教程都是以前的方法：下载代码、宝塔建站、上传代码、安装扩展、访问域名安装。</p>
<p>可新版本V3，下载下来就一个执行文件。根本没办法用这一套方法解决。</p>
<p>&nbsp;</p>
<p>那真的有必要用新版本吗？</p>
<p>我觉得是有的，新版本增加了很多特性：</p>
<h3>✨ Cloudreve 新版V3特性</h3>
<ul>
<li>☁️ 支持本机、从机、七牛、阿里云 OSS、腾讯云 COS、又拍云、OneDrive (包括世纪互联版) 作为存储端</li>
<li>📤 上传/下载 支持客户端直传，支持下载限速</li>
<li>💾 可对接 Aria2 离线下载</li>
<li>📚 在线 压缩/解压缩、多文件打包下载</li>
<li>💻 覆盖全部存储策略的 WebDAV 协议支持</li>
<li>⚡ 拖拽上传、目录上传、流式上传处理</li>
<li>🗃️ 文件拖拽管理</li>
<li>👩‍👧‍👦 多用户、用户组</li>
<li>🔗 创建文件、目录的分享链接，可设定自动过期</li>
<li>👁️‍🗨️ 视频、图像、音频、文本、Office 文档在线预览</li>
<li>🎨 自定义配色、黑暗模式、PWA 应用、全站单页应用</li>
<li>🚀 All-In-One 打包，开箱即用</li>
<li>🌈 ... ...</li>

</ul>
<p>&nbsp;</p>
<p><strong>官方下载地址、官网和文档</strong></p>
<p>Cloudreve官网：<a href='https://cloudreve.org/'>https://cloudreve.org</a></p>
<p>官方下载地址：<a href='https://github.com/cloudreve/Cloudreve/releases'>https://github.com/cloudreve/Cloudreve/releases</a></p>
<p>官方文档：<a href='https://docs.cloudreve.org/'>https://docs.cloudreve.org/</a></p>
<p>官方论坛：<a href='https://forum.cloudreve.org/'>https://forum.cloudreve.org/</a></p>
<h2>Cloudreve新版V3安装步骤</h2>
<p><strong>写在前面</strong></p>
<ul>
<li>使用宝塔面板进行安装的</li>
<li>服务器的基础环境配置可以参考之前的文章</li>
<li>有任何问题可以下方留言讨论</li>
</ul>

<p><strong>那就开始安装吧</strong></p>
<p>1.</p>
<p><strong>确认服务器内核版本参数</strong></p>
<p>目前官方只提供常见系统架构下可用的主程序，所以需要我们先确认下我们服务器的系统架构。</p>
<p>在宝塔面板中，使用终端，输入<code>arch</code>，就可以看到系统架构。</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/76328a87fd77b.png" alt="1637823761900.png" title="1637823761900.png" /></p>
<p>输出结果x86_64代表amd64；aarch64代表arm64。</p>
<p>2.</p>
<p><strong>下载主程序</strong></p>
<p>之后系统架构后，我们就可以下载对应的主程序。</p>
<p>我们打开官方下载地址：<a href='https://github.com/cloudreve/Cloudreve/releases'>https://github.com/cloudreve/Cloudreve/releases</a></p>
<p>找到对应的系统版本下载。</p>
<p>我这边因为上一步输出结果为x86_64，那我需要下载amd64版本。</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/dc4bce435db64.png" alt="1637823956865.png" title="1637823956865.png" /></p>
<p>3.</p>
<p><strong>建立网站，创建文件夹</strong></p>
<p>我们在宝塔面板中，创建新网站，输入域名。</p>
<p>（数据库可以不创建，因为新版自带SQLite轻版数据库）</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/6bacdbece8417.png" alt="1637826765712.png" title="1637826765712.png" /></p>
<p>4.</p>
<p><strong>上传主程序到网站根目录</strong></p>
<p>上传刚才下载的主程序到网站根目录，并解压。</p>
<p>我们就得到了一个没有后缀的主程序。</p>
<p>（这个和我之前解压的主程序差别很大，导致我也是蒙了很久）</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/b3d216fecbaa4.png" alt="1637826883888.png" title="1637826883888.png" /></p>
<p>我们点击这个程序的权限管理，给予它755权限。</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/b7abe6844c2a4.png" alt="1637824376183.png" title="1637824376183.png" /></p>
<p>这样就算弄好了。</p>
<p>5.</p>
<p><strong>放行5212端口</strong></p>
<p>cloudreve默认需要通过5212端口访问。</p>
<p>我们在宝塔面板中，打开安全，放行5212端口。</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/5bba32e1273f0.png" alt="1637824549803.png" title="1637824549803.png" /></p>
<p>有的服务器可能还需要去服务商那边放行相应的端口才可以访问。</p>
<p>比如阿里云，默认5212端口是没有放行的，就需要在安全组里面添加5212端口。</p>
<p>（这部分因为各服务商不同，就不再赘述了）</p>
<p>6.</p>
<p><strong>启动程序</strong></p>
<p>走到这一步，就完成安装了。接下来就是启动。</p>
<p>我们到网站根目录下，点击终端，输入<code>./cloudreve</code>，启动 Cloudreve。</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/0627c0db60c48.png" alt="1637826990552.png" title="1637826990552.png" /></p>
<p>启动后就可以看到默认的<strong>账号</strong>和<strong>密码</strong>：</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/e40aab9dfe9cb.png" alt="1637825053542.png" title="1637825053542.png" /></p>
<p>然后输入登录地址<code>域名:5212</code>，类似这样：<a href='http://pan.yzitc.com:5050' target='_blank' class='url' rel="noopener noreferrer">http://pan.yzitc.com:5050</a>，就可以进入cloudreve，登录并使用了。</p>
<p>* 推荐在网站根目录下打开终端，不然进入终端后，还得使用cd命令进入该目录。</p>
<p>* 启动Cloudreve后，不要关闭终端，不然这个程序就关闭了。</p>
<h2>更多高级设置</h2>
<h3>1.进程常驻（程序一直开着）</h3>
<p>每次需要通过终端打开，关闭终端程序就会关闭，肯定没办法使用。我们可以使用Supervisor管理器，让cloudreve一直开着。</p>
<p>宝塔软件商店搜索Supervisor，即可安装。</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/c4b0ce58e9b46.png" alt="1637825414908.png" title="1637825414908.png" /></p>
<p>安装后，我们点击设置，添加守护进程。</p>
<p>输入名称，运行目录（我们的网站目录），启动命令（网站目录地址/cloudreve），即可让cloudreve这个进程常驻。</p>
<p>不会的可以参考我这个：</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/34cf8e0411297.png" alt="1637825526798.png" title="1637825526798.png" /></p>
<h3>2.更改访问地址（简化成直接域名访问）</h3>
<p>现在打开的域名后面还要加<code>：5121</code>，不是很好看，我们可以通过设置反代理，去掉这个小尾巴。</p>
<p>我们打开网站设置，找到反代理，添加反代理。</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/1b49197ab7acf.png" alt="1637825875189.png" title="1637825875189.png" /></p>
<p>填入名称，目标URL填入：<a href='http://127.0.0.1:5212' target='_blank' class='url' rel="noopener noreferrer">http://127.0.0.1:5212</a></p>
<p>点击提交即可。</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/e76840fff3c3f.png" alt="1637825951726.png" title="1637825951726.png" /></p>
<p>这样就可以直接使用域名不用添加小尾巴进行访问了。</p>
<p>网站打开后，后台设置里面也记得要设置下</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/f5dc2b940fd74.png" alt="1637826070184.png" title="1637826070184.png" /></p>
<h3>3.自定义数据库</h3>
<p>（自带的够用，不推荐改）</p>
<p>程序默认的数据库是自带的SQLite，可以改成常用的mysql。</p>
<p>我们新建一个mysql数据库，得到数据库名、用户名和密码。</p>
<p>将相关信息填写到网站目录下的conf.ini文件里，命令行里重启进程，获得新账号密码。</p>
<p><img src="http://ossimg.yzitc.com/2021/11/25/2ab2440b76464.png" alt="1637826934262.png" title="1637826934262.png" /></p>