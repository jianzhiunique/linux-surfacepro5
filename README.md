# Surface Pro 5运行Linux系统

## 前言

首先说一下背景，本人之前有MacBook Pro（2016款），因2016年出的这批有电池、键盘等一系列问题（官方已确认），我的电池鼓包了两次，键盘也有按键重复问题以及按键摁不动的问题，所以最终也没在闲鱼上坑别人，直接走了闲鱼的回收，只回收了2700块钱。

在此期间一直关注Surface Pro，因为它是平板，在便携性方面非常吸引我，另外它的背部支架设计不错。当然在购买之前就已经开始考虑往Surface Pro上运行Linux这件事了，对各版本对Linux的支持情况做了考察，具体见https://github.com/linux-surface/linux-surface/wiki/Supported-Devices-and-Features#feature-matrix。总的来说，从Surface Pro 5（2017）开始，支持的比较完善了（摄像头除外，但我基本不用）。

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

| 体验排名 | 发行版名称   | 发行版系列 | 主要优点                                      | 主要缺点                                               |
| -------- | ------------ | ---------- | --------------------------------------------- | ------------------------------------------------------ |
| 1        | Manjaro      | Arch       | 近乎完美，软件多，流行                        | 偶尔有些小问题                                         |
| 2        | Deepin       | Debian     | 国产，良心，软件多，DDE桌面美观，符合国人习惯 | 偶尔卡顿、睡死、耗电问题，但基本能正常运行             |
| 3        | Ubuntu Kylin | Ubuntu     | 国产                                          | 睡死，休眠需要自己配置，对比Deepin和Ubuntu显得没啥亮点 |
| 3        | Ubuntu       | Ubuntu     | 界面，社区支持                                | 睡死，休眠需要自己配置                                 |
| 4        | elementary   | Ubuntu     | 界面美观，Mac风格                             | 睡死，休眠需要自己配置                                 |

Manjaro发行版排名第2不是没有道理的，配置很全，使得我这种小白也能轻松进入Arch Linux的世界。

Manjaro和Deepin都提供了休眠支持，不用自己折腾了，好评。

Deepin更符合国人习惯，常用的软件输入法、QQ、微信之类的不需要过多配置，基本商店里直接下载安装。Manjaro需要少量配置，像输入法等，毕竟是老外搞的。

## 安装Manjaro KDE版本

#### 下载镜像

从清华大学镜像站下载速度会比较快

 https://mirrors.tuna.tsinghua.edu.cn/osdn/storage/g/m/ma/manjaro/kde/

#### 制作启动盘

使用dd命令写入镜像（我是在Linux下制作启动盘的，Windows下用Runfs制作）

```
dd if=manjaro-xxx.iso of=/dev/sda
其中U盘可以通过以下命令确认
fdisk -l
```

#### 安装系统

安装过程我就不详细写了，可以看看这个，看到安装完成部分就可以了。

https://www.jianshu.com/p/21c39bc4dd31

记得使用“带休眠”的模式规划磁盘，我是用了整块磁盘，选了带休眠的选项。

## 安装Surface内核

过程可以参考原文

https://github.com/linux-surface/linux-surface/wiki/Installation-and-Setup

#### 安装之后的第一个问题

可能无法连接WIFI，但能够连接手机热点。没有网络就无法下载一些必要的文件。也可以在其他电脑上下载一些必要的文件。

#### 下载linux-surface提供的内核

linux-surface提供了package仓库安装的方式，

https://github.com/linux-surface/linux-surface/wiki/Package-Repositories

但可能因为无法翻墙导致无法添加key，可以从能翻墙的地方复制下来，存到文件里，然后通过cat替换wget。

这种能够自动更新，但我推荐直接使用git上发布的release，选择lts版本的内核（4.19），主要原因是5.8内核iptsd多点触控对pen的支持不好，画图的时候手和pen识别有问题，无法正常使用pen。

在https://github.com/linux-surface/linux-surface/releases页面上下载lts内核文件。

linux-surface-lts-4.19.150-1-x86_64.pkg.tar.zst

linux-surface-lts-headers-4.19.150-1-x86_64.pkg.tar.zst

#### 安装内核

双击打开下载的两个文件就可以安装了

#### 安装触摸屏支持

安装IPTS firmware package

https://github.com/linux-surface/surface-ipts-firmware/releases

#### 安装完成后重启

重启之后，触摸屏、pen、WIFI通通都正常了。

## Manjaro后续系统配置

#### 连接WIFI

#### 缩放设置

进入系统后字体没有缩放很小，先设置缩放。

系统设置 --- 硬件 --- 显示和监控 --- 全局缩放率调整到200%

#### 注销重新登录

为了让缩放生效

#### 设置KDE全局主题（Mac风格）

系统设置 --- 外观 --- 全局主题 --- 获取新的全局主题

--- 搜索WhiteSur-dark（mac风格的）--- 安装

回到全局主题界面 --- 勾选使用来自主题的桌面布局 --- 应用

然后一个mac风格的界面就OK了

#### 电源管理

1.进入系统设置 - 硬件 - 电源管理 - 节能

将交流供电、电池供电、电池电量低三个Tab页中的

按键事件处理 - 合上笔记本盖时 - 设置为关闭屏幕

默认的设置是合上盖子时休眠，但我一般是要合上键盘盖后拿去另一个地方，所以干脆只是关闭屏幕就好了。

另外如果设置睡眠，在合上键盘盖马上打开，会有很差的体验，推荐不要设置睡眠。

2.活动项设置 - 定义特殊行为 - 勾选不要关闭计算机，也不让它睡眠

这么设置的目的是防止睡眠睡死

另外经过测试，不睡眠只是关闭屏幕的耗电量也不很快

#### 软件仓库设置

这里可以用命令行设置，但为了小白，还是界面操作比较好

添加/删除软件 --- 点击右上角的三个点 （...） --- 首选项 

--- 官方软件仓库选择China （加快下载速度）

--- AUR --- 启用AUR支持（为了安装大量软件）

---Snap --- 启用Snap支持（为了安装大量软件）

---Flatpak --- 启用Flatpak支持（为了安装大量软件）

#### 安装搜狗输入法

```undefined
sudo pacman -S fcitx-im
sudo pacman -S fcitx-configtool
sudo pacman -S fcitx-sogoupinyin
```

添加输入法配置文件 `sudo vim ~/.xprofile`

```bash
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

重启系统让输入法生效，输入法配置可以搜索软件“fcitx配置“ 来进行配置

#### 常用pacman命令

```bash
pacman -S  软件名   #安装
pacman -Syu    #更新
pacman -R 软件名    #移除
```

#### 安装软件的方法

1. 可以在添加/删除软件中直接搜索安装
2. 也可以用pacman安装软件

```
例如
sudo pacman -S google-chrome
sudo pacman -S deepin-screenshot
sudo pacman -S deepin-wine-tim
sudo pacman -S netease-cloud-music
```

#### 安装dock软件

常见的dock软件有latte-dock、plank等，我使用的是latte-dock，plank虽然很简洁，但自动隐藏后好像不好触发回来。

#### 安装微信

软件商店搜索deepin-wine-wechat（AUR）安装

安装后打开，缩放有问题，设置wine缩放

终端中输入

```
env WINEPREFIX="$HOME/.deepinwine/Deepin-Wechat" winecfg
```

然后，调节`显示`中的dpi即可，144大概是1.5倍，168大概是2倍。

重启微信

#### 替换KDE的Dolphin

这个实在有点丑，用nautilus替换一下，顺便系统设置 --- 个性化 --- 应用程序 --- 可以设置文件的默认打开软件

#### 其他常用软件

| 软件        | 功能                  |
| ----------- | --------------------- |
| Typora      | MarkDown编辑          |
| MyPaint     | 绘图工具，对pen支持好 |
| ThunderBird | 邮件                  |

#### 其他的系统设置

系统设置 

--- 工作区 --- 开机和关机 --- 登录屏幕SDDM --- 选择WhiteSur

--- 个性化 --- 应用程序 --- 可以设置文件的默认打开软件

--- 硬件 --- 输入设备 

  --- 键盘 --- 高级 

​     --- Ctrl键位置 --- 左Alt和左Ctrl对换 （符合MacBook Pro习惯）

​     --- 大写锁定行为 --- 大写锁定被禁用

  --- 触摸板 

​     --- 轻触拖拽 取消勾选

​     --- 反向滚动（自然滚动）（符合MacBook Pro习惯）

#### 最终桌面效果图

![深度截图_选择区域_20201012213453](images/深度截图_选择区域_20201012213453.png)



















