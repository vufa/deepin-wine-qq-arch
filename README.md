# 在Archlinux及衍生发行版上运行QQ

Deepin打包的QQ容器移植到Archlinux

构建状态: ![https://github.com/countstarlight/deepin-wine-qq](https://travis-ci.org/countstarlight/deepin-wine-qq-arch.svg?branch=master)

感谢:

* [Wuhan Deepin Technology Co.,Ltd.](http://www.deepin.org/)


* @[wszqkzqk](https://github.com/wszqkzqk) 的 [wszqkzqk-deepin-wine-tim-arch](https://github.com/wszqkzqk/wszqkzqk-deepin-wine-tim-arch)

* @[ssfdust](https://github.com/ssfdust) 的 [wszqkzqk-deepin-wine-tim-arch](https://github.com/ssfdust/wszqkzqk-deepin-wine-tim-arch)

存在如下问题：
  * 1.不能视频通话
  * 2.不能记住密码

## 安装
* 1.已添加到AUR [deepin-wine-qq](https://aur.archlinux.org/packages/deepin-wine-qq/)，可直接安装:
```shell
yaourt deepin-wine-qq
```

* 2.手动安装

```shell
 git clone https://github.com/countstarlight/deepin-wine-qq-arch.git

 cd deepin-wine-qq-arch
  
 makepkg -si
```

* 运行开始菜单中创建的QQ，点击立即安装
* 安装完可直接启动，以后启动时无需安装
* **前几次运行时可能会提示 "qq安全组件异常"，尝试重启系统**
* 默认使用文泉驿微米黑(`wqy-microhei`)字体，要使用其他字体，如 微软雅黑或者微软宋体放进`～/.deepinwine/Deepin-QQ/drive_c/windows/Fonts`中。
## 常见问题
* 1.解决在 2k/4k 屏幕下字体和图标都非常小, 参见[issue1](https://github.com/countstarlight/deepin-wine-tim-arch/issues/1)
* 2.使用全局截图快捷键和解决Gnome上窗口化问题，参见[issue2](https://github.com/countstarlight/deepin-wine-tim-arch/issues/2)
## 更新日志
* 2017-12-31 QQ-8.9.6
