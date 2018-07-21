# HC5962---1.4.8.20462s
极路由4增强版

先看救砖教程

https://s.histatic.com/ued/rom/romdoc.html

已上传固件



几个小问题
biyehong 发表于 2018-1-19 23:45
兄弟，之前B70免root开启了权限，现在不知道怎么刷入breed，能出一套教程吗？

上传 breed 到 /tmp/storage/ 然后写入 uboot
mtd write breed-mt7621-hiwifi-hc5962.bin u-boot
复制代码





原来的MAC，怎么弄进去？
点评
 lily339
你刷完bdinfo和oem原来的mac就回来了，不用再命令行改




lily339 发表于 2018-1-15 13:45
key怎么写回去呢？感觉还是breed里面直接恢复备份的firmware.bin更完美

pb-boot备份的firmware.bin用breed恢复备份 MAC后六位都是0
点评
 lily339
那就只有用这个把key写回去  发表于 2018-2-4 11:53






B70从padavan恢复到极路由原厂固件全过程，MAC地址正确恢复 [复制链接]
start2005a

电梯直达
跳转到指定楼层 1#
 发表于 2018-5-15 18:13 | 只看该作者 回帖奖励
斐讯总部【独家】探秘！内有零元购产品高清拆机大图，点击下单，再送额外现金红包！【微信公众号：diydaily】
本帖最后由 start2005a 于 2018-5-17 09:09 编辑


需要使用：
openwrt-ramips-mt7621-hc5962-squashfs-factory.bin （在相关资源文件里）
bdinfo.bin、oem.bin、firmware.bin 3个备份分区文件（在相关资源文件里有其他人备份的 bdinfo.bin、oem.bin 文件，但不建议使用）


【现状】
已刷成 padavan 固件 + breed。

分区如下：

dev:    size   erasesize  name
mtd0: 00040000 00020000 "Bootloader"
mtd1: 00040000 00020000 "BootEnv"
mtd2: 00080000 00020000 "Config"
mtd3: 00040000 00020000 "Factory"
mtd4: 00180000 00020000 "Kernel"
mtd5: 01e80000 00020000 "RootFS"
mtd6: 00400000 00020000 "Storage"
mtd7: 05a40000 00020000 "RWFS"
mtd8: 02000000 00020000 "Firmware_Stub"

【还原步骤】
这个刷机步骤是参照 only1word 的 http://www.right.com.cn/forum/thread-269196-1-1.html
hc5962 (b70) 全分区读写固件 - 刷回原厂固件，修复 mac 变成 0

进入 breed，固件更新-常规固件-固件，刷入固件 openwrt-ramips-mt7621-hc5962-squashfs-factory.bin，刷完重新启动路由器

登录ssh（用户名：root，密码：password）
查看分区：

cat /proc/mtd

分区变成：
dev:    size   erasesize  name
mtd0: 00080000 00020000 "u-boot"
mtd1: 00080000 00020000 "debug"
mtd2: 00040000 00020000 "factory"
mtd3: 00200000 00020000 "kernel"
mtd4: 01e00000 00020000 "ubi"
mtd5: 00080000 00020000 "hw_panic"
mtd6: 00080000 00020000 "bdinfo"
mtd7: 00080000 00020000 "backup"
mtd8: 01000000 00020000 "overly"
mtd9: 02000000 00020000 "firmware_backup"
mtd10: 00200000 00020000 "oem"
mtd11: 02ac0000 00020000 "opt"

将备份的 bdinfo.bin，oem.bin 上传到路由器的 /proc 目录下，，

《提示》：我是使用自己备份的 bdinfo.bin 和 oem.bin，没有使用 B70_by_huangxzying 目录下的 bdinfo.bin, oem.bin。

cd /proc

刷写特殊分区 bdinfo 和 oem：
mtd write bdinfo.bin bdinfo
mtd write oem.bin oem

重新进入 breed 中，固件更新-常规固件-固件，刷入备份的 firmware.bin
重启后，进入设置极路由管理界面，发现mac地址没有变，进入智能插件可以安装在线插件，安装开发者模式插件后，用ssh登录进入，查看分区如下：

dev:    size   erasesize  name
mtd0: 00080000 00020000 "u-boot"
mtd1: 00080000 00020000 "debug"
mtd2: 00040000 00020000 "Factory"
mtd3: 02000000 00020000 "firmware"
mtd4: 00180000 00020000 "kernel"
mtd5: 01e80000 00020000 "rootfs"
mtd6: 00080000 00020000 "hw_panic"
mtd7: 00080000 00020000 "bdinfo"
mtd8: 00080000 00020000 "backup"
mtd9: 01000000 00020000 "overlay"
mtd10: 02000000 00020000 "firmware_backup"
mtd11: 00200000 00020000 "oem"
mtd12: 02ac0000 00020000 "opt"

这时 u-boot 还是breed，而其他部分则是极路由的了。手机app又可以管理这个路由器了。
据说：在原厂固件内点 "路由器固件升级" 会刷写 uboot 回到原厂uboot（我没有试）

相关资源：

链接：https://pan.baidu.com/s/1sJaEEx_IUr0DbrK9UlucUA 密码：rp6q

【提醒】：相关资源文件里有别人的 bdinfo.bin 和 oem.bin，据说极路由分区的mac、key是保存在这2个分区里的。如果使用别人的bdinfo.bin 和 oem.bin，也应该可以刷回去，不过mac、key可能是别人的，有可能产生无法预料的其他问题，比如：被原主人的极路由账户绑定你的路由器，远程控制你的路由器。

分享到:  
QQ好友和群QQ好友和群
 
QQ空间Q


*******************************************

hc5962 (b70) 全分区读写固件 - 刷回原厂固件，修复 mac 变成 0     [复制链接]
only1word

电梯直达
跳转到指定楼层 1#
 发表于 2018-1-15 12:16 | 只看该作者 回帖奖励
斐讯总部【独家】探秘！内有零元购产品高清拆机大图，点击下单，再送额外现金红包！【微信公众号：diydaily】
本帖最后由 only1word 于 2018-2-8 08:20 编辑


ssh ：
root:password

刷写 breed：
mtd write breed-mt7621-hiwifi-hc5962.bin u-boot

刷写特殊分区：
mtd write 7.bin bdinfo
mtd write 11.bin oem

特别提醒：
官网下载的固件带 uboot ，链接内有 B70 最新 (1.4.8.20462s) 去除 uboot 固件，用 breed 直刷恢复即可。
刷写固件完成后，在 breed 恢复出厂设置。
在固件内点 "路由器固件升级" 会刷写 uboot !!!

最后的话：


基于 lean ，lede 分支编译，特别感谢。

各种各种原因，取消分享和停止更新了。后续可能会提供教程。

http://www.right.com.cn/forum/thread-250789-1-1.html

1、下载putty
2、进极路由里面把开发者模式插件下载下来，前提是这个极路由开了开发者模式，这个会失去保修

3、端口是1022，用户名是root，密码是admin
ok
4、login as: root
root@192.168.199.1's password:


BusyBox v1.22.1 (2017-08-10 12:16:35 CST) built-in shell (ash)
Enter 'help' for a list of built-in commands.

***********************************************************
              __  __  _              _   ____  _   TM
             / / / / (_) _      __  (_) / __/ (_)
            / /_/ / / / | | /| / / / / / /_  / /
           / __  / / /  | |/ |/ / / / / __/ / /
          /_/ /_/ /_/   |__/|__/ /_/ /_/   /_/
                  http://www.hiwifi.com/
***********************************************************
root@Hiwifi:~#

查看分区

root@Hiwifi:~# cat /proc/mtd
dev:    size   erasesize  name
mtd0: 00080000 00020000 "u-boot"
mtd1: 00080000 00020000 "debug"
mtd2: 00040000 00020000 "Factory"
mtd3: 02000000 00020000 "firmware"
mtd4: 00180000 00020000 "kernel"
mtd5: 01e80000 00020000 "rootfs"
mtd6: 00080000 00020000 "hw_panic"
mtd7: 00080000 00020000 "bdinfo"
mtd8: 00080000 00020000 "backup"
mtd9: 01000000 00020000 "overlay"
mtd10: 02000000 00020000 "firmware_backup"
mtd11: 00200000 00020000 "oem"
mtd12: 02ac0000 00020000 "opt"



Ø  2、刷入pb-boot。
楼主的第二没弄成，最后

>>
Ø  2、刷入pb-boot。
l ssh登录路由器输入以下红色部分命令。（注意：路由器要联网）
ssh 192.168.199.1 22
root@Hiwifi:/tmp# cd /tmp   //命令说明：进入tmp目录
root@Hiwifi:/tmp# wget http://files.80x86.io/router/rom ... /pb-boot-hc5962.bin //命令说明：用wget命令下载B70 pb-boot，后面网址为pb-boot下载地址，直接复制即可。
Connecting to files.80x86.io(172.104.85.105:80)
pb-boot-hc5962.bin   100%|**************************************************************|   157k 0:00:00 ETA
root@Hiwifi:/tmp# md5sum pb-boot-hc5962.bin   //命令说明：验证pb-boot MD5值，保证文件完整性。
0ebdb3f60b5c407fa82570855c703522  pb-boot-hc5962.bin
root@Hiwifi:/tmp# mtd write pb-boot-hc5962.bin u-boot  //命令说明：用mtd命令写入pb-boot
Unlocking u-boot ...

Writing from pb-boot-hc5962.bin to u-boot...
[e:0] [w0]
[e:1] [w1]
[e:1] [w1]                                                                                                  
root@Hiwifi:/tmp#mtd erase firmware_backup   //命令说明：擦除原厂备份固件。如果不擦backup,重启后会恢复回去。
Unlocking firmware_backup
Erasing firmware_backup

我是这么办的，首先找到pb boot，我在论坛里找到了，并附上连接
mtd write /tmp/B70_3.4.3.9-099_20170910-2224.trx firmware
pb-boot-hc5962.rar
这个帖子里给的刷法不一样
我把PandoraBox-ralink-mt7621-hc5962-2017-03-17-git-3840fad-squashfs-sysupgrade.bin换成了B70_3.4.3.9-099_20170910-2224.trx
其他不变，成功了。
>>
***************
刷写/恢复方法
在安装好极路由的开发者模式后. 将固件和pb-boot上传到路由/tmp目录下,然后使用如下命令刷入:
1.mtd write /tmp/PandoraBox-ralink-mt7621-hc5962-2017-03-17-git-3840fad-squashfs-sysupgrade.bin firmware
2.mtd erase firmware_backup
更新为pb-boot:
3.mtd write /tmp/pb-boot-hc5962.bin u-boot

如果不擦backup,重启后会恢复回去. 
提醒: 开通开发者模式会失去官方保修，且不可恢复.

固件保留了极4的分区信息, 不破坏原机信，建议刷机前备份firmware分区，
这样可以在pb-boot下面恢复原厂固件。
****************************
在此找到固件，因为我要刷华硕。
华硕固件http://www.upantool.com/gujian/asus/11525.html
极路由B70华硕padavan固件3.4.3.9-099


*****************
http://www.right.com.cn/forum/thread-320375-1-1.html
这个帖子里介绍了MAC变000000后怎么操作
