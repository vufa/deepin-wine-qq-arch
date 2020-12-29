在Archlinux及衍生发行版上运行QQ
========

<p align="center">
  <a href="https://travis-ci.org/countstarlight/deepin-wine-qq-arch">
    <img src="https://travis-ci.org/countstarlight/deepin-wine-qq-arch.svg?branch=master" alt="Build Status">
  </a>
  <a href="https://im.qq.com/download/">
    <img src="https://img.shields.io/badge/QQ-9.4.0.27525-blue.svg" alt="QQ Version">
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

Deepin 打包的 QQ 容器移植到 Archlinux，不依赖 `deepin-wine5`，包含定制的注册表配置，QQ 安装包替换为官方最新

<!-- TOC -->

- [安装](#安装)
    - [从AUR安装](#从aur安装)
    - [用安装包安装](#用安装包安装)
    - [本地打包安装](#本地打包安装)
- [兼容性记录](#兼容性记录)
- [切换到 `deepin-wine`](#切换到-deepin-wine)
    - [自动切换(推荐)](#自动切换推荐)
    - [手动切换](#手动切换)
        - [1. 安装 `deepin-wine`](#1-安装-deepin-wine)
        - [2. 对于非 GNOME 桌面(KDE, XFCE等)](#2-对于非-gnome-桌面kde-xfce等)
        - [3. 删除已安装的QQ目录](#3-删除已安装的qq目录)
        - [4. 修复 `deepin-wine` 字体渲染发虚](#4-修复-deepin-wine-字体渲染发虚)
- [常见问题及解决](#常见问题及解决)
    - [不能记住密码](#不能记住密码)
    - [网络连接状态改变后不能重连](#网络连接状态改变后不能重连)
    - [高分辨率屏幕支持](#高分辨率屏幕支持)
    - [GNOME 桌面上的悬浮窗口问题](#gnome-桌面上的悬浮窗口问题)
    - [使用其他字体](#使用其他字体)
- [感谢](#感谢)
- [更新日志](#更新日志)

<!-- /TOC -->

## 安装

`deepin-wine-qq` 依赖`Multilib`仓库中的 `wine`，`wine-gecko` 和 `wine-mono`，Archlinux默认没有开启 `Multilib`仓库，需要编辑`/etc/pacman.conf`，取消对应行前面的注释([Archlinux wiki](https://wiki.archlinux.org/index.php/Official_repositories#multilib)):

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

**注意：由于新版QQ可能需要 `wine` 还没有实现的一些win api，这会导致一些功能不可用，安装前先根据[兼容性记录](#兼容性记录)选择一个合适的版本**

以下三种安装方式效果相同，选择一种即可

### 从AUR安装

已添加到 AUR [deepin-wine-qq](https://aur.archlinux.org/packages/deepin-wine-qq/)，可使用 `yay` 或 `yaourt` 安装:

```shell
yay -S deepin-wine-qq
```

### 用安装包安装

> 由 [Travis CI](https://travis-ci.org/countstarlight/deepin-wine-qq-arch) 在 Docker 容器 [mikkeloscar/arch-travis](https://hub.docker.com/r/mikkeloscar/arch-travis) 中自动构建的 ArchLinux 安装包

在 [GitHub Release](https://github.com/countstarlight/deepin-wine-qq-arch/releases) 页面下载后缀为 `.pkg.tar.xz` 或 `.pkg.tar.zst` 的安装包，使用`pacman`安装：

```bash
sudo pacman -U #下载的包名
```

`.md5` 文件用于校验包完整性：

```bash
md5sum -c *.md5
```

### 本地打包安装

```shell
 git clone https://github.com/countstarlight/deepin-wine-qq-arch.git

 cd deepin-wine-qq-arch
  
 makepkg -si
```

用上述三种安装方式之一安装完成后，运行应用菜单中创建的 QQ 快捷方式，首次运行会用 QQ 的安装包进行安装

**NOTE: 前几次运行时可能会提示 "qq安全组件异常"，等一会再运行或重启一下系统**

## 兼容性记录

|     QQ      |  wine  |   兼容性   |        备注        | deepin-wine | 兼容性 | 备注 |
| :---------: | :----: | :--------: | :----------------: | :----------: | :----: | :--: |
| 9.4.1.27572 |  5.22  | **不支持** |                    |  5.0.16-1    |  支持  |      |
| 9.4.0.27525 |  5.21  | **不支持** |                    |  2.18_24-3   |  支持  |      |
| 9.3.9.27427 |  5.19  |    支持    |                    |  2.18_24-3   |  支持  |      |
| 9.3.8.27381 |  5.17  | **不支持** |      无法启动      |  2.18_24-3   |  支持  |      |
| 9.3.7.27301 |  5.15  |    支持    |                    |  2.18_24-3   |  支持  |      |
| 9.3.6.27263 |  5.12  |    支持    |                    |  2.18_22-3   |  支持  |      |
| 9.3.5.27030 |  5.10  |    支持    |                    |  2.18_22-3   |  支持  |      |
| 9.3.3.27011 |  5.9   |    支持    |                    |  2.18_22-3   |  支持  |      |
| 9.3.3.27009 |  5.8   |    支持    |                    |  2.18_22-3   |  支持  |      |
| 9.3.2.26869 |  5.8   |    支持    |                    |  2.18_22-3   |  支持  |      |
| 9.1.8.26211 | 4.20-1 |    支持    |                    |              |        |      |
| 9.1.8.26211 | 4.18-1 |    部分    | 不能使用中文输入法 |              |        |      |
| 9.1.8.26211 | 4.17-1 |    部分    | 不能使用中文输入法 |              |        |      |
| 9.1.8.26211 | 4.16-1 |    支持    |                    |              |        |      |

## 切换到 `deepin-wine5`

> 根据 [deepin-wine-wechat-arch#15](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/15#issuecomment-515455845)，[deepin-wine-wechat-arch#27](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/27)，由 [@feileb](https://github.com/feileb), [@violetbobo](https://github.com/violetbobo), [@HE7086](https://github.com/HE7086)提供的方法

原版 `wine` 在 [DDE(Deepin Desktop Environment)](https://www.deepin.org/dde/) 上，有托盘图标无法响应鼠标事件([deepin-wine-tim-arch#21](https://github.com/countstarlight/deepin-wine-tim-arch/issues/21))的问题，且原版 `wine` 尚不能实现保存登录密码等功能，可以选择切换到 `deepin-wine5`。

**注意：切换前先确保 `deepin-wine5` 支持**

### 自动切换(推荐)

```bash
/opt/apps/com.qq.im.deepin/files/run.sh -d
```

这会安装需要的依赖，移除已安装的 QQ 目录并回退对注册表文件的修改

切换回 `wine`：

```bash
rm ~/.deepinwine/com.qq.im.deepin/deepin
```

如果要卸载自动安装的依赖：

```bash
sudo pacman -Rns deepin-wine5 xsettingsd lib32-freetype2-infinality-ultimate
```

### 手动切换

#### 1. 安装 `deepin-wine5`

```bash
yay -S deepin-wine5
```

#### 2. 对于非 GNOME 桌面(KDE, XFCE等)

> 根据 [deepin-wine-wechat-arch#36](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/36#issuecomment-612001200)，由[Face-Smile](https://github.com/Face-Smile)提供的方法

需要安装 `xsettingsd`：

```bash
sudo pacman -S xsettingsd
```

修改 `/opt/apps/com.qq.im.deepin/files/run.sh`：

```diff
-WINE_CMD="wine"
+WINE_CMD="deepin-wine5"

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

**注意：对 `/opt/apps/com.qq.im.deepin/files/run.sh` 的修改会在 `deepin-wine-qq` 更新或重装时被覆盖，可以单独拷贝一份作为启动脚本**

#### 3. 删除已安装的QQ目录

```bash
rm -rf ~/.deepinwine/com.qq.im.deepin
```

#### 4. 修复 `deepin-wine5` 字体渲染发虚

kde桌面参考：[deepin-wine-wechat-arch#36](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/36)

deepin 桌面：

```bash
yay -S lib32-freetype2-infinality-ultimate
```

**注意：切换到 `deepin-wine5` 后，对 `wine` 的修改，如更改dpi，都改为对 `deepin-wine5` 的修改**

## 常见问题及解决

### 不能记住密码

参照[切换到 `deepin-wine`](#切换到-deepin-wine) 解决

### 网络连接状态改变后不能重连

参照[切换到 `deepin-wine`](#切换到-deepin-wine) 解决

### 高分辨率屏幕支持

在 `winecfg` 的Graphics选项卡中修改dpi，如 修改为`192`

对于 `wine`：

```bash
env WINEPREFIX="$HOME/.deepinwine/com.qq.im.deepin" winecfg
```

对于 `deepin-wine` ：

```bash
env WINEPREFIX="$HOME/.deepinwine/com.qq.im.deepin" deepin-wine5 winecfg
```

### GNOME 桌面上的悬浮窗口问题

> 根据 [deepin-wine-tim-arch#2](https://github.com/countstarlight/deepin-wine-tim-arch/issues/2)，由[EricDracula](https://github.com/EricDracula)提供的方法

安装 GNOME 插件: [TopIcons Plus](https://extensions.gnome.org/extension/1031/topicons/)

### 使用其他字体

默认使用文泉驿微米黑(`wqy-microhei`)字体，可以使用Windows平台常用字体替代，直接将字体文件或字体链接文件放置到字体文件夹就会生效，不会影响系统字体

字体文件夹在：`$HOME/.deepinwine/com.qq.im.deepin/drive_c/windows/Fonts`

## 感谢

* [Wuhan Deepin Technology Co.,Ltd.](http://www.deepin.org/)

* [@wszqkzqk](https://github.com/wszqkzqk) 的 [wszqkzqk-deepin-wine-tim-arch](https://github.com/wszqkzqk/wszqkzqk-deepin-wine-tim-arch)

* [@ssfdust](https://github.com/ssfdust) 的 [wszqkzqk-deepin-wine-tim-arch](https://github.com/ssfdust/wszqkzqk-deepin-wine-tim-arch)

## 更新日志

<details open>
<summary>2020</summary>

* 2020-12-24 QQ-9.4.1.27572
* 2020-11-12 QQ-9.4.0.27525
* 2020-10-18 QQ-9.3.9.27427
* 2020-09-13 QQ-9.3.8.27381
* 2020-08-16 QQ-9.3.7.27301
* 2020-07-19 QQ-9.3.6.27263
* 2020-06-19 QQ-9.3.5.27030
* 2020-06-05 QQ-9.3.3.27011
* 2020-05-22 QQ-9.3.3.27009
* 2020-05-11 QQ-9.3.2.26869

</details>
<details>
<summary>2019</summary>

* 2019-11-17 QQ-9.1.8.26211 deepin.com.qq.im_9.1.8deepin0
* 2019-09-21 QQ-9.1.8.26211 deepin.com.qq.im_8.9.19983deepin23
* 2019-04-19 QQ-9.1.1.24953
* 2019-03-18 QQ-9.1.0.24712
* 2019-03-06 QQ-9.0.9.24445
* 2019-02-05 QQ-9.0.9_1

</details>
<details>
<summary>2017</summary>

* 2017-12-31 QQ-8.9.6

</details>

