# Maintainer: CountStarlight <countstarlight@gmail.com>
# Maintainer: wszqkzqk <wszqkzqk@gmail.com>
# Maintainer: ssfdust <ssfdust@gmail.com>

pkgname=deepin-wine-qq
pkgver=9.0.9_1
deepinqqver=8.9.19983deepin23
pkgrel=3
pkgdesc="Tencent QQ (com.qq.im) on Deepin Wine For Archlinux"
arch=("x86_64")
url="http://im.qq.com/"
license=('custom')
depends=('p7zip' 'wine' 'wine-mono' 'wine_gecko' 'xorg-xwininfo' 'xdotool' 'wqy-microhei' 'adobe-source-han-sans-cn-fonts' 'lib32-alsa-lib' 'lib32-alsa-plugins' 'lib32-libpulse' 'lib32-openal')
conflicts=('deepin-qq-im' 'deepin.com.qq.im')
install="deepin-wine-qq.install"
_mirror="https://mirrors.ustc.edu.cn/deepin"
source=("$_mirror/pool/non-free/d/deepin.com.qq.im/deepin.com.qq.im_${deepinqqver}_i386.deb"
  "https://qd.myapp.com/myapp/qqteam/pcqq/QQ${pkgver}.exe"
  "run.sh"
  "reg_files.tar.bz2"
  "update.policy")
md5sums=('5135313eb131feeb6fef613ba02804cf'
  'a6273221731e7d253d6273c5de452e72'
  '6440495c91b01a2e23bbaeda2592ca63'
  '6675c8950e976b1ca01fd6001aa79523'
  'a66646b473a3fbad243ac1afd64da07a')

build() {
  msg "Extracting DPKG package ..."
  mkdir -p "${srcdir}/dpkgdir"
  tar -xvf data.tar.xz -C "${srcdir}/dpkgdir"
  sed "s/\(Categories.*$\)/\1Network;/" -i "${srcdir}/dpkgdir/usr/share/applications/deepin.com.qq.im.desktop"
  msg "Extracting Deepin Wine QQ archive ..."
  7z x -aoa "${srcdir}/dpkgdir/opt/deepinwine/apps/Deepin-QQ/files.7z" -o"${srcdir}/deepinqqdir"
  msg "Removing original outdated QQ directory ..."
  rm -r "${srcdir}/deepinqqdir/drive_c/Program Files/Tencent/QQ"
  msg "Adding config files and fonts"
  tar -jxvf reg_files.tar.bz2 -C "${srcdir}/"
  cp userdef.reg "${srcdir}/deepinqqdir/userdef.reg"
  cp system.reg "${srcdir}/deepinqqdir/system.reg"
  cp update.policy "${srcdir}/deepinqqdir/update.policy"
  cp user.reg "${srcdir}/deepinqqdir/user.reg"
  ln -sf "/usr/share/fonts/wenquanyi/wqy-microhei/wqy-microhei.ttc" "${srcdir}/deepinqqdir/drive_c/windows/Fonts/wqy-microhei.ttc"
  ln -sf "/usr/share/fonts/adobe-source-han-sans/SourceHanSansCN-Medium.otf" "${srcdir}/deepinqqdir/drive_c/windows/Fonts/SourceHanSansCN-Medium.otf"
  msg "Repackaging app archive ..."
  7z a -t7z -r "${srcdir}/files.7z" "${srcdir}/deepinqqdir/*"
}

package() {
  msg "Preparing icons ..."
  install -d "${pkgdir}/usr/share"
  cp -a ${srcdir}/dpkgdir/usr/share/* "${pkgdir}/usr/share/"
  msg "Copying QQ to /opt/deepinwine/apps/Deepin-QQ ..."
  install -d "${pkgdir}/opt/deepinwine/apps/Deepin-QQ"
  install -m644 "${srcdir}/files.7z" "${pkgdir}/opt/deepinwine/apps/Deepin-QQ/"
  install -m755 "${srcdir}/run.sh" "${pkgdir}/opt/deepinwine/apps/Deepin-QQ/"
  install -m644 "${srcdir}/QQ$pkgver.exe" "${pkgdir}/opt/deepinwine/apps/Deepin-QQ/"
  echo "$(tput setaf 1)$(tput setab 7)!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!$(tput sgr 0)"
  echo "$(tput setaf 1)$(tput setab 7)!!!!!                                 !!!!$(tput sgr 0)"
  echo "$(tput setaf 1)$(tput setab 7)!!!!!NEED TO REBOOT AFTER INSTALLATION!!!!$(tput sgr 0)"
  echo "$(tput setaf 1)$(tput setab 7)!!!!!                                 !!!!$(tput sgr 0)"
  echo "$(tput setaf 1)$(tput setab 7)!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!$(tput sgr 0)"
}
