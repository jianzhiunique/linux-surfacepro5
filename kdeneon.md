# KDE neon安装

## 提前下载Linux Surface内核

在https://github.com/linux-surface/linux-surface/releases

页面上下载lts内核文件。选择debian_lts-4.19.157-1这样的进行下载

IPTS firmware package

https://github.com/linux-surface/surface-ipts-firmware/releases

## 安装系统

下载镜像、制作启动盘、安装系统

## 安装Linux Surface内核

首先安装Linux Surface内核

## 安装grub-customizer

安装此软件是为了在开机的时候自动使用Linux surface内核

然而此时WIFI可能并不可用，可以试试手机开个热点

```
sudo apt install grub-customizer
```

## 使用grub-customizer修改启动内核

进入软件，调整内核顺序，使linux surface内核排在第一个，保存退出，重启，重启后可以正常连接WIFI

## 替换ubuntu软件源

Ubuntu 的软件源配置文件是 `/etc/apt/sources.list`。将系统自带的该文件做个备份，将该文件替换为下面内容。

```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

## 安装百度输入法

在安装百度输入法前，首先可以在Discover软件中心中搜索fcitx进行安装 

然后下载百度输入法进行安装https://srf.baidu.com/site/guanwang_linux/index.html

```
sudo dpkg -i fcitx-baidupinyin.deb 
```

## 安装WPS

https://www.wps.cn/product/wpslinux

```
sudo dpkg -i sudo dpkg -i fcitx-baidupinyin.deb  
```

## 安装微信

```
sudo apt install wget g++ git
git clone "https://gitee.com/wszqkzqk/deepin-wine-for-ubuntu.git"
cd deepin-wine-for-ubuntu/
sudo ./install.sh

# https://mirrors.aliyun.com/deepin/pool/non-free/d/
wget https://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.wechat/deepin.com.wechat_2.6.2.31deepin0_i386.deb
sudo dpkg -i deepin.com.wechat_2.6.2.31deepin0_i386.deb
sudo apt install libjpeg62:i386

# 安装playonlinux
# 设置缩放
env WINEPREFIX="$HOME/.deepinwine/Deepin-Wechat" winecfg
```



