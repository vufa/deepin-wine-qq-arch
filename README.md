# 在Archlinux及衍生发行版上运行QQ

Deepin打包的QQ容器移植到Archlinux，包含定制的注册表配置，QQ安装包替换为官方最新

构建状态: [![travis-ci](https://travis-ci.org/countstarlight/deepin-wine-qq-arch.svg?branch=master)](https://travis-ci.org/countstarlight/deepin-wine-qq-arch)

感谢:

* [Wuhan Deepin Technology Co.,Ltd.](http://www.deepin.org/)


* [@wszqkzqk](https://github.com/wszqkzqk) 的 [wszqkzqk-deepin-wine-tim-arch](https://github.com/wszqkzqk/wszqkzqk-deepin-wine-tim-arch)

* [@ssfdust](https://github.com/ssfdust) 的 [wszqkzqk-deepin-wine-tim-arch](https://github.com/ssfdust/wszqkzqk-deepin-wine-tim-arch)

存在如下问题：

- [ ] 1.不能视频通话
- [ ] 2.不能记住密码
- [ ] 3.网络连接状态改变后不能重连: [issue19](https://github.com/countstarlight/deepin-wine-tim-arch/issues/19)

## 安装
* 1.已添加到AUR [deepin-wine-qq](https://aur.archlinux.org/packages/deepin-wine-qq/)，可使用 `yay/yaourt` 安装:
```shell
yay -S deepin-wine-qq
```

如果添加了archlinuxcn源，这会直接从源里安装，源相比AUR仓库有一定的延迟，或选择从AUR仓库安装:

```shell
yay deepin-wine-qq
```

* 2.手动安装

```shell
 git clone https://github.com/countstarlight/deepin-wine-qq-arch.git

 cd deepin-wine-qq-arch
  
 makepkg -si
```

* 运行开始菜单中创建的QQ，点击立即安装

* 安装完可直接启动，以后启动时无需安装

* **前几次运行时可能会提示 "qq安全组件异常"，等一会再运行或重启一下系统**

## 字体

默认使用文泉驿微米黑(`wqy-microhei`)字体，目前有字体虚化、模糊问题，可以使用Windows平台常用字体，直接将字体文件或字体链接文件放置到字体文件夹就会生效，不会影响系统字体

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
## 常见问题
* 1.解决在 2k/4k 屏幕下字体和图标都非常小, 参见[issue1](https://github.com/countstarlight/deepin-wine-tim-arch/issues/1)
* 2.使用全局截图快捷键和解决Gnome上窗口化问题，参见[issue2](https://github.com/countstarlight/deepin-wine-tim-arch/issues/2)

## 更新日志

* 2019-03-18 QQ-9.1.0.24712
* 2019-03-06 QQ-9.0.9.24445
* 2019-02-05 QQ-9.0.9_1
* 2017-12-31 QQ-8.9.6

