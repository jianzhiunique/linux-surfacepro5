## 安装Deepin20

#### 下载镜像

https://www.deepin.org/zh/download/

#### 制作启动盘

使用深度官方启动盘制作工具制作启动盘

#### 提前下载Surface内核文件

下载releases中的debian_lts的最新版即可

https://github.com/linux-surface/linux-surface/releases/tag/debian_lts-4.19.154-1

#### 安装系统

安装系统比较简单，简单操作即可

#### 首次进入系统

安装完成后第一次进入系统应该不能连接WIFI，将提前下载好的surface内核文件全部安装，然后重启

开机界面手动选择第二项，然后选择surface内核，进入系统

这样就可以连接WIFI了，电池电量也正常

#### 安装Grub Customizer

打开应用商店，下载Grub Customizer，用此软件来更改启动项，以便自动进入surface内核

打开软件后，可以看到开机选项列表，使用上箭头、下箭头可以更改他们的顺序

把二级菜单的全部移动，所有的选项都平级。

然后把Deepin 20 GNU/Linux，Linux 4.19.xxx-surface-lts放在第一个位置，保存即可

后续还会有系统更新调整，如果发现顺序变了，可以再次操作设置。

#### 进行一次系统更新

在控制中心 - 更新 中进行更新，然后将系统更新至最新，重启

#### 更改显卡驱动

在应用商店中下载显卡驱动管理器

打开软件，选择使用Intel加速模式，点击切换

重启系统，点击应用

再次进入系统后会进行设置，然后之后再次重启系统

#### 下载常用软件

应用商店中有大量软件，如IDEA、Steam、Typora、VS Code、WPS、微信、网易云音乐、Chrome等，按需安装即可。

#### 修改键盘映射

为了符合Mac的使用习惯，我习惯将Caps禁用（Mac上这个位置可以切换大小写，可惜在Linux下不好将Shift和Caps变换位置，由于经常按错，索性直接将Caps禁用，大写使用Shift即可），同时将左边的Alt和Ctrl更换位置，这样就能愉快的使用类似Mac的Command了。

在KDE的设置里，可以在键盘的高级设置里做同样的事情。

```
禁用capslock，更换alt、ctrl
gsettings set com.deepin.dde.keybinding.mediakey capslock '[]'
gsettings set com.deepin.dde.keyboard layout-options '["caps:none", "ctrl:swap_lalt_lctl"]'
```

PS：使用以下命令可以查看所有可选的键盘配置方案

```
查看options
localectl list-x11-keymap-options | grep caps:
cat /usr/share/X11/xkb/rules/xfree86.lst | grep caps
```

#### 在其他版本的Deepin中微信界面小的问题

如果微信缩放有问题，首先可以安装PlayOnLinux（其中包含了winecfg这个命令），然后设置wine缩放，终端中输入

```
env WINEPREFIX="$HOME/.deepinwine/Deepin-Wechat" winecfg
```

然后，调节`显示`中的dpi即可，144大概是1.5倍，168大概是2倍。

重启微信







