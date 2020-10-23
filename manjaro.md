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

在https://github.com/linux-surface/linux-surface/releases

页面上下载lts内核文件。

linux-surface-lts-4.19.150-1-x86_64.pkg.tar.zst

linux-surface-lts-headers-4.19.150-1-x86_64.pkg.tar.zst

#### 安装内核

双击打开下载的两个文件就可以安装了

#### 安装触摸屏支持

安装IPTS firmware package

https://github.com/linux-surface/surface-ipts-firmware/releases

#### 安装完成后重启

重启之后，触摸屏、pen、WIFI通通都正常了。

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
sudo pacman -Sy vim
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

#### 替换KDE的Dolphin（可选）

可以用nautilus替换一下KDE的Dolphin，顺便系统设置 --- 个性化 --- 应用程序 --- 可以设置文件的默认打开软件

#### 