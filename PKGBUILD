# Maintainer: Codist <countstarlight@gmail.com>

pkgname=deepin-wine-qq
pkgver=9.4.1.27572
qq_installer=PCQQ2020
deepinqqver=9.1.8deepin0
debpkgname="deepin.com.qq.im"
pkgrel=1
pkgdesc="Tencent QQ (com.qq.im) on Deepin Wine For Archlinux"
arch=("x86_64")
url="http://im.qq.com/"
license=('custom')
depends=('p7zip' 'wine' 'wine-mono' 'wine-gecko' 'xorg-xwininfo' 'wqy-microhei' 'lib32-alsa-lib' 'lib32-alsa-plugins' 'lib32-libpulse' 'lib32-openal' 'lib32-mpg123' 'lib32-gnutls')
conflicts=('deepin-qq-im' 'deepin.com.qq.im')
install="deepin-wine-qq.install"
_mirror="https://mirrors.njupt.edu.cn"
source=("$_mirror/deepin/pool/non-free/d/${debpkgname}/${debpkgname}_${deepinqqver}_i386.deb"
  "${qq_installer}-${pkgver}.exe::https://down.qq.com/qqweb/PCQQ/PCQQ_EXE/${qq_installer}.exe"
  "run.sh"
  "reg.patch")
md5sums=('d35bd4abfd1ac4c5e71c7fbc5282ccbd'
  '554b662419788aa893b5e342426f8548'
  '026bed7d6008f8125d6628ef8e9249a6'
  '62d7de16a69fd99bca881f801187ba13')

build() {
  msg "Extracting DPKG package ..."
  mkdir -p "${srcdir}/dpkgdir"
  tar -xvf data.tar.xz -C "${srcdir}/dpkgdir"
  sed "s/\(Categories.*$\)/\1Network;/" -i "${srcdir}/dpkgdir/usr/share/applications/deepin.com.qq.im.desktop"
  msg "Extracting Deepin Wine QQ archive ..."
  7z x -aoa "${srcdir}/dpkgdir/opt/deepinwine/apps/Deepin-QQ/files.7z" -o"${srcdir}/deepinqqdir"
  msg "Removing original outdated QQ directory ..."
  rm -r "${srcdir}/deepinqqdir/drive_c/Program Files/Tencent/QQ"
  msg "Patching reg files ..."
  patch -p1 -d "${srcdir}/deepinqqdir/" < "${srcdir}/reg.patch"
  msg "Creating font file link ..."
  ln -sf "/usr/share/fonts/wenquanyi/wqy-microhei/wqy-microhei.ttc" "${srcdir}/deepinqqdir/drive_c/windows/Fonts/wqy-microhei.ttc"
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
  install -m644 "${srcdir}/reg.patch" "${pkgdir}/opt/deepinwine/apps/Deepin-QQ/"
  install -m755 "${srcdir}/run.sh" "${pkgdir}/opt/deepinwine/apps/Deepin-QQ/"
  install -m644 "${srcdir}/${qq_installer}-${pkgver}.exe" "${pkgdir}/opt/deepinwine/apps/Deepin-QQ/"
}
