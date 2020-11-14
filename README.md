# Surface Pro 5运行Linux系统

## 前言

首先说一下背景，本人之前有MacBook Pro（2016款），因2016年出的这批有电池、键盘等一系列问题（官方已确认），我的电池鼓包了两次，键盘也有按键重复问题以及按键摁不动的问题，所以最终也没在闲鱼上坑别人，直接走了闲鱼的回收，只回收了2700块钱。

在此期间一直关注Surface Pro，因为它是平板，在便携性方面非常吸引我，另外它的背部支架设计不错。当然在购买之前就已经开始考虑往Surface Pro上运行Linux这件事了，对各版本对Linux的支持情况做了考察，具体见https://github.com/linux-surface/linux-surface/wiki/Supported-Devices-and-Features#feature-matrix

总的来说，从Surface Pro 5（2017）开始，支持的比较完善了（摄像头除外，但我基本不用）。

机型选择上，主要考虑了价格。因为从Surface Pro 5开始，机型的外观和功能方面，感觉变化并不大，另外本来也没想花很多钱在这上面，所以最终选择了Surface Pro 5。闲鱼上淘的二手，花费3600块。

买回来之后，开始用了2周左右Win10，但是作为一个从MacBook Pro转到Surface Pro的用户，实在是无法接受Win10的问题：命令行、某些软件分辨率的问题、Win10的乱七八糟、系统占用问题、软件各种弹广告等等。是时候开始考虑使用Linux了。

## 安装Linux前的准备

作为一个几年没有用过Windows系统的用户，因为前期准备不足，首先遇到的就是 Secure Boot 的问题。如果你正在考虑安装Linux系统，行动之前建议充分阅读一下这里：https://github.com/linux-surface/linux-surface/wiki/Installation-and-Setup。

因经验不足，我是从双系统安装开始的。

这里主要有几个点：

1. 开机键、音量+键一起按进入BIOS设置
2. 在Win10上关闭bitlocker加密。https://jingyan.baidu.com/article/ab0b5630e17204815afa7dc5.html
3. BIOS设置中关闭Secure Boot。关闭之后在开机画面上会显示红色的块，是正常现象。
4. 准备好Linux启动盘

第2条，这个非常坑，会导致蓝屏无法进入系统，让输入秘钥。我遇到了这个问题，好在最后在其他电脑上登录了之前在Win10下登录过的微软账号获得了秘钥，进入了系统，之后赶紧关闭了加密。

## Surface Pro 5上运行各种Linux发行版的对比

我尝试了很多发行版在Surface Pro 5上的运行情况，所以这里先给出一些关键的对比。Fedora系的Fedora、CentOS等没有尝试。

| 体验排名 | 发行版名称        | 发行版系列 | 主要优点                                                    | 主要缺点                                 |
| -------- | ----------------- | ---------- | ----------------------------------------------------------- | ---------------------------------------- |
| 1        | Manjaro           | Arch       | KDE版本近乎完美，软件多，发行版排名第2，休眠支持            | 偶尔有些小问题                           |
| 2        | Kubuntu/KDE  neon | Ubuntu     | KDE近乎完美，Ubuntu系软件支持好                             | 微信等软件不好安装，需要额外操作         |
| 3        | Deepin            | Debian     | 国产软件，良心，软件多，DDE桌面美观，符合国人习惯，休眠支持 | 偶尔卡顿、休眠问题、耗电问题             |
| 4        | Ubuntu Kylin      | Ubuntu     | 国产软件                                                    | 休眠问题，对比Deepin和Ubuntu显得没啥亮点 |
| 5        | Ubuntu            | Ubuntu     | 界面，社区支持好                                            | 休眠问题                                 |
| 6        | elementary        | Ubuntu     | 界面美观，Mac风格                                           | 休眠问题                                 |

休眠问题指的是：当合上键盘盖或者长时间不用时，无法唤醒屏幕，或者唤醒后WIFI无法连接等，建议设置不允许休眠以防止休眠问题产生。

Manjaro和Deepin都提供了休眠支持，但有时候休眠的功能还是不太好用。

总的来说，KDE桌面能够为Surface Pro提供更好的支持，建议选择与KDE相关的发行版。

## 发行版选择向导

如果你完全不想折腾，选择Deepin，因为Deepin更符合国人习惯，常用的软件、输入法、QQ、微信之类的不需要过多配置，基本商店里直接下载安装。

[Deepin安装向导](deepin.md)

如果你想使用ArchLinux系的，希望软件多一些，选择Manjaro的KDE版本。Manjaro提供了snap、AUR等支持，但需要少量配置，像输入法等。大部分软件也能在界面搜索和安装。

[Manjaro KDE安装向导](manjaro.md)

如果你接受较多的配置，希望系统更好用一些，选择Kbuntu或KDE neon，个人推荐KDE neon，在省电方面做的好。

[Kubuntu安装向导](kubuntu.md)

[KDE neon安装向导](kdeneon.md)

## KDE桌面设置

[KDE桌面设置](kde.md)

## Linux常用软件

| 软件                    | 功能                      |
| ----------------------- | ------------------------- |
| Typora                  | MarkDown编辑              |
| MyPaint、Krita          | 绘图工具，可以使用pen绘图 |
| ThunderBird             | 邮件                      |
| Chromium,Chrome,Firefox | 浏览器                    |
| Genymotion              | 安卓模拟器                |
| GIMP                    | 图像处理                  |



















