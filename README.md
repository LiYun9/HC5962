# HC5962---1.4.8.20462s
极路由4增强版 

2018-7-21 21点开始 

2018年7月22日3:36结束 

先看救砖教程，网上一大堆


已上传原厂固件HC5962-sysupgrade-20170810-3a807c77.bin

注意：不要着急进入192.168.1.1的恢复界面，把整个帖子看完再动手不迟。一定要注意备份。 

备份的三个文件 

Factory.bin 

firmware.zip（用的话需要解压缩） 

u-boot.bin 

******************************************* 

以下是真正教程 

打开这个网址 

[http://www.right.com.cn/forum/thread-250789-1-1.html](http://www.right.com.cn/forum/thread-250789-1-1.html)



###开启ssh的办法帖子里没写 

开启ssh 

1、下载putty 

2、进极路由里面把开发者模式插件下载下来，前提是这个极路由开了开发者模式，这个会失去保修，网友的不失去保修开启ssh的方法我没学会。 

3、可以看到，端口是1022，用户名是root，密码是admin 

ok 

4、login as: root 

密码是admin（如果你改了，那就是你改的那个，大概是无线密码） 

root@192.168.199.1's password: 


这个是截图（我就截了这一个图）因为后面跟帖子上的都一样。 
 
 
>BusyBox v1.22.1 (2017-08-10 12:16:35 CST) built-in shell (ash) 

>Enter 'help' for a list of built-in commands. 

>
>***********************************************************
>              __  __  _              _   ____  _   TM
>             / / / / (_) _      __  (_) / __/ (_)
>            / /_/ / / / | | /| / / / / / /_  / /
>           / __  / / /  | |/ |/ / / / / __/ / /
>          /_/ /_/ /_/   |__/|__/ /_/ /_/   /_/
>                  http://www.hiwifi.com/
>***********************************************************
>root@Hiwifi:~# cat /proc/mtd

>dev:    size   erasesize  name

>mtd0: 00080000 00020000 "u-boot"

>mtd1: 00080000 00020000 "debug"

>mtd2: 00040000 00020000 "Factory"

>mtd3: 02000000 00020000 "firmware"

>mtd4: 00180000 00020000 "kernel"

>mtd5: 01e80000 00020000 "rootfs"

>mtd6: 00080000 00020000 "hw_panic"

>mtd7: 00080000 00020000 "bdinfo"

>mtd8: 00080000 00020000 "backup"

>mtd9: 01000000 00020000 "overlay"

>mtd10: 02000000 00020000 "firmware_backup"

>mtd11: 00200000 00020000 "oem"

>mtd12: 02ac0000 00020000 "opt"



刷pb-boot这一步用了很长时间，一直进不到192.168.1.1的界面。 

这个按照网址上说的的弄不成，又再论坛里各种找，最后找出正确办法 

下面是另一个帖子，我按照这个帖子成功的完成了后半段的刷机工作。 

[http://www.right.com.cn/forum/thread-209726-1-1.html](http://www.right.com.cn/forum/thread-209726-1-1.html)

1、我是这么办的，首先下载pb boot 

pb-boot-hc5962.bin 

这个文件我也上传了 

2、因为我要刷华硕。教程里面不一样，所以在论坛里找到了。 

华硕固件[http://www.upantool.com/gujian/asus/11525.html]（http://www.upantool.com/gujian/asus/11525.html）

极路由B70华硕padavan固件3.4.3.9-099 

这个我也上传了 

***************
刷写/恢复方法 

按照帖子里的方法将固件（B70_3.4.3.9-099_20170910-2224.trx）和pb-boot上传到路由/tmp目录下,然后使用如下命令刷入: 

1.mtd write /tmp/B70_3.4.3.9-099_20170910-2224.trx firmware 

2.mtd erase firmware_backup 

更新为pb-boot: 

3.mtd write /tmp/pb-boot-hc5962.bin u-boot 

重启路由可以进192.168.5.1了，admin，admin

注：有些固件是.bin，有些固件是.trx，虽然不知道区别，但是都对。。。 

**************************** 

按照教程很快刷成功了。 

以下就是一些变砖或出问题后的解决办法。 

***************** 

[http://www.right.com.cn/forum/thread-320375-1-1.html](http://www.right.com.cn/forum/thread-320375-1-1.html）

这个帖子里介绍了MAC变000000后怎么操作。我没实验，因为我没打算换回原厂固件。 


******************* 



最后我把我的备份都上传上来 

需要的东西我大部分也都上传，教程有点乱，凑合看吧，我用了6个小时刷机，这个教程最多半小时看完。 


[https://github.com/LiYun9/HC5962---1.4.8.20462s](https://github.com/LiYun9/HC5962---1.4.8.20462s)


需要的东西去这个网址下载 


两个工具软件 

putty-64bit-0.70-installer.msi 

WinSCP+5.9.3.7136+绿色便携.zip 


华硕固件 

B70_3.4.3.9-099_20170910-2224.trx 


原厂固件 

HC5962-sysupgrade-20170810-3a807c77.bin 


不死引导 

pb-boot-hc5962.bin 


教程.DOC版 

固件刷机教程.doc 


备份的三个文件 

Factory.bin 

firmware.zip（用的话需要解压缩） 

u-boot.bin 


README.md（这个就是我现在写的东西） 

注：
最后感谢坛友的贡献，如有侵权请告知，及时删除

[http://www.right.com.cn/forum/thread-250789-1-1.html](http://www.right.com.cn/forum/thread-250789-1-1.html)

[http://www.upantool.com/gujian/asus/11525.html](http://www.upantool.com/gujian/asus/11525.html)

[http://www.right.com.cn/forum/thread-320375-1-1.html](http://www.right.com.cn/forum/thread-320375-1-1.html)

