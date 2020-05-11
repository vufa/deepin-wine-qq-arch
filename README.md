在Archlinux及衍生发行版上运行QQ
========

<p align="center">
  <a href="https://travis-ci.org/countstarlight/deepin-wine-qq-arch">
    <img src="https://travis-ci.org/countstarlight/deepin-wine-qq-arch.svg?branch=master" alt="Build Status">
  </a>
  <a href="https://im.qq.com/download/">
    <img src="https://img.shields.io/badge/QQ-9.3.2.26869-blue.svg" alt="QQ Version">
  </a>
  <a href="https://aur.archlinux.org/packages/deepin-wine-qq/">
    <img src="https://img.shields.io/aur/version/deepin-wine-qq.svg" alt="AUR Version">
  </a>
  <a href="https://github.com/countstarlight/deepin-wine-qq-arch/releases">
    <img src="https://img.shields.io/github/downloads/countstarlight/deepin-wine-qq-arch/total.svg" alt="GitHub Release">
  </a>
  <a href="https://github.com/countstarlight/deepin-wine-qq-arch/issues">
    <img src="https://img.shields.io/github/issues/countstarlight/deepin-wine-qq-arch.svg" alt="GitHub Issues">
  </a>
</p>

Deepin打包的QQ容器移植到Archlinux，不依赖`deepin-wine`，包含定制的注册表配置，QQ安装包替换为官方最新

<!-- TOC -->

- [安装](#安装)
    - [从AUR安装](#从aur安装)
    - [用安装包安装](#用安装包安装)
    - [本地打包安装](#本地打包安装)
- [兼容性记录](#兼容性记录)
- [切换到 `deepin-wine`](#切换到-deepin-wine)
    - [自动切换(推荐)](#自动切换推荐)
    - [手动切换](#手动切换)
        - [1. 安装 deepin-wine](#1-安装-deepin-wine)
        - [2. 对于非 GNOME 桌面(KDE, XFCE等)](#2-对于非-gnome-桌面kde-xfce等)
        - [3. 删除已安装的QQ目录](#3-删除已安装的qq目录)
        - [4. 修复 `deepin-wine` 字体渲染发虚](#4-修复-deepin-wine-字体渲染发虚)
- [字体](#字体)
    - [使用其他字体](#使用其他字体)
    - [修复字体模糊](#修复字体模糊)
- [常见问题及解决](#常见问题及解决)
    - [不能记住密码](#不能记住密码)
    - [网络连接状态改变后不能重连](#网络连接状态改变后不能重连)
    - [高分辨率屏幕支持](#高分辨率屏幕支持)
    - [使用全局截图快捷键](#使用全局截图快捷键)
- [感谢](#感谢)
- [更新日志](#更新日志)

<!-- /TOC -->

## 安装

`deepin-wine-qq`依赖`Multilib`仓库中的`wine`，`wine_gecko`和`wine-mono`，Archlinux默认没有开启`Multilib`仓库，需要编辑`/etc/pacman.conf`，取消对应行前面的注释([Archlinux wiki](https://wiki.archlinux.org/index.php/Official_repositories#multilib)):

```diff
# If you want to run 32 bit applications on your x86_64 system,
# enable the multilib repositories as required here.

#[multilib-testing]
#Include = /etc/pacman.d/mirrorlist

-#[multilib]
-#Include = /etc/pacman.d/mirrorlist
+[multilib]
+Include = /etc/pacman.d/mirrorlist
```

### 从AUR安装

已添加到AUR [deepin-wine-qq](https://aur.archlinux.org/packages/deepin-wine-qq/)，可使用 `yay` 或 `yaourt` 安装:

```shell
yay -S deepin-wine-qq
```

### 用安装包安装

> 由[Travis CI](https://travis-ci.org/countstarlight/deepin-wine-qq-arch)在Docker容器[mikkeloscar/arch-travis](https://hub.docker.com/r/mikkeloscar/arch-travis)中自动构建的ArchLinux安装包

在[GitHub Release](https://github.com/countstarlight/deepin-wine-qq-arch/releases)页面下载 `.pkg.tar.xz`后缀的安装包，使用`pacman`安装：

```bash
sudo pacman -U #下载的包名
```

### 本地打包安装

```shell
 git clone https://github.com/countstarlight/deepin-wine-qq-arch.git

 cd deepin-wine-qq-arch
  
 makepkg -si
```

* 运行应用菜单中创建的QQ快捷方式

* **前几次运行时可能会提示 "qq安全组件异常"，等一会再运行或重启一下系统**

## 兼容性记录

|   QQ版本    | wine版本 | 兼容性 |        备注        | deepin-wine版本 | 兼容性 | 备注 |
| :---------: | :------: | :----: | :----------------: | :-------------: | :----: | :--: |
| 9.3.2.26869 |   5.8    |  支持  |                    |    2.18_22-3    |  支持  |      |
| 9.1.8.26211 |  4.20-1  |  支持  |                    |                 |        |      |
| 9.1.8.26211 |  4.18-1  |  部分  | 不能使用中文输入法 |                 |        |      |
| 9.1.8.26211 |  4.17-1  |  部分  | 不能使用中文输入法 |                 |        |      |
| 9.1.8.26211 |  4.16-1  |  支持  |                    |                 |        |      |

## 切换到 `deepin-wine`

原版 `wine` 在 [DDE(Deepin Desktop Environment)](https://www.deepin.org/dde/) 上，有托盘图标无法响应鼠标事件([deepin-wine-tim-arch#21](https://github.com/countstarlight/deepin-wine-tim-arch/issues/21))的问题，且原版 `wine` 尚不能实现保存登录密码等功能，可以选择切换到 `deepin-wine`。

**注意：切换前先确保 `deepin-wine` 支持**

根据 [deepin-wine-wechat-arch#15](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/15#issuecomment-515455845)，[deepin-wine-wechat-arch#27](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/27)，由 [@feileb](https://github.com/feileb), [@violetbobo](https://github.com/violetbobo), [@HE7086](https://github.com/HE7086)提供的方法：

### 自动切换(推荐)

```bash
/opt/deepinwine/apps/Deepin-QQ/run.sh -d
```

这会安装需要的依赖，移除已安装的微信目录并回退对注册表文件的修改

切换回 `wine`：

```bash
rm ~/.deepinwine/Deepin-QQ/deepin
```

如果要卸载自动安装的依赖：

```bash
sudo pacman -Rns deepin-wine xsettingsd lib32-freetype2-infinality-ultimate
```

### 手动切换

#### 1. 安装 deepin-wine

```bash
yay -S deepin-wine
```

#### 2. 对于非 GNOME 桌面(KDE, XFCE等)

需要安装 `xsettingsd`：

根据 [deepin-wine-wechat-arch#36](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/36#issuecomment-612001200)，由[Face-Smile](https://github.com/Face-Smile)提供的方法：

```bash
sudo pacman -S xsettingsd
```

修改 `/opt/deepinwine/apps/Deepin-QQ/run.sh`：

```diff
-WINE_CMD="wine"
+WINE_CMD="deepin-wine"

 RunApp()
 {
+    if [[ -z "$(ps -e | grep -o xsettingsd)" ]]
+    then
+        /usr/bin/xsettingsd &
+    fi
        if [ -d "$WINEPREFIX" ]; then
                UpdateApp
        else
```

**注意：对 `/opt/deepinwine/apps/Deepin-QQ/run.sh` 的修改会在 `deepin-wine-qq` 更新或重装时被覆盖，可以单独拷贝一份作为启动脚本**

#### 3. 删除已安装的QQ目录

```bash
rm -rf ~/.deepinwine/Deepin-QQ
```

#### 4. 修复 `deepin-wine` 字体渲染发虚

kde桌面参考：[deepin-wine-wechat-arch#36](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/36)

deepin 桌面：

```bash
yay -S lib32-freetype2-infinality-ultimate
```

**注意：切换到 `deepin-wine` 后，对 `wine` 的修改，如更改dpi，都改为对 `deepin-wine` 的修改**

## 字体

### 使用其他字体

默认使用文泉驿微米黑(`wqy-microhei`)字体，目前有字体虚化、模糊问题，可以使用Windows平台常用字体替代，直接将字体文件或字体链接文件放置到字体文件夹就会生效，不会影响系统字体

字体文件夹在：`$HOME/.deepinwine/Deepin-QQ/drive_c/windows/Fonts`

Windows 10自带字体及版本：<https://docs.microsoft.com/en-us/typography/fonts/windows_10_font_list>

* 中易宋体(SimSun)：`simsun.ttf` 或 `simsun.ttc`，图为SimSun, Regular：

  ![simsun](simsun.png)

* 微软雅黑(Microsoft YaHei)：`msyh.ttf`或`msyh.ttc`，图为Microsoft YaHei, Regular：

  ![msyh](msyh.png)

  Microsoft YaHei, Bold：

  ![msyhb](msyhb.png)

* (繁体)细明体(MingLiU)：`mingliu.ttf` 或 `mingliu.ttc`

* (繁体)新细明体(PMingLiU)：`pmingliu.ttf` 或 `pmingliu.ttc`

### 修复字体模糊

参见：[deepin-wine-tim-arch#修复字体模糊](https://github.com/countstarlight/deepin-wine-tim-arch#%E4%BF%AE%E5%A4%8D%E5%AD%97%E4%BD%93%E6%A8%A1%E7%B3%8A)

## 常见问题及解决

### 不能记住密码

参照[切换到 `deepin-wine`](#切换到-deepin-wine) 解决

### 网络连接状态改变后不能重连

参照[切换到 `deepin-wine`](#切换到-deepin-wine) 解决

### 高分辨率屏幕支持

在 2k/4k 屏幕下字体和图标都非常小, 参见[issue1](https://github.com/countstarlight/deepin-wine-tim-arch/issues/1)

### 使用全局截图快捷键

使用全局截图快捷键和解决Gnome上窗口化问题，参见[issue2](https://github.com/countstarlight/deepin-wine-tim-arch/issues/2)

## 感谢

* [Wuhan Deepin Technology Co.,Ltd.](http://www.deepin.org/)

* [@wszqkzqk](https://github.com/wszqkzqk) 的 [wszqkzqk-deepin-wine-tim-arch](https://github.com/wszqkzqk/wszqkzqk-deepin-wine-tim-arch)

* [@ssfdust](https://github.com/ssfdust) 的 [wszqkzqk-deepin-wine-tim-arch](https://github.com/ssfdust/wszqkzqk-deepin-wine-tim-arch)

## 更新日志

* 2020-05-11 QQ-9.3.2.26869
* 2019-11-17 QQ-9.1.8.26211 deepin.com.qq.im_9.1.8deepin0
* 2019-09-21 QQ-9.1.8.26211 deepin.com.qq.im_8.9.19983deepin23
* 2019-04-19 QQ-9.1.1.24953
* 2019-03-18 QQ-9.1.0.24712
* 2019-03-06 QQ-9.0.9.24445
* 2019-02-05 QQ-9.0.9_1
* 2017-12-31 QQ-8.9.6

