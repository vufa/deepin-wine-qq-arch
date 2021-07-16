# Maintainer: Codist <countstarlight@gmail.com>
# Maintainer: taotieren <admin@taotieren.com>

pkgname=deepin-wine-qq
pkgver=9.4.9.27849
qq_installer=PCQQ2021
debpkgver=9.3.2deepin20
debpkgname="com.qq.im.deepin"
pkgrel=1
pkgdesc="Tencent QQ on Deepin Wine5(${debpkgname}) For Archlinux"
arch=("x86_64")
url="https://im.qq.com/"
license=('custom')
depends=('p7zip' 'wine' 'wine-mono' 'wine-gecko' 'xorg-xwininfo' 'wqy-microhei' 'lib32-alsa-lib' 'lib32-alsa-plugins' 'lib32-libpulse' 'lib32-openal' 'lib32-mpg123' 'lib32-gnutls')
conflicts=('deepin-qq-im' 'deepin.com.qq.im')
install="deepin-wine-qq.install"
_mirror="https://cdn-package-store6.deepin.com"
source=("$_mirror/appstore/pool/appstore/c/${debpkgname}/${debpkgname}_${debpkgver}_i386.deb"
  "${qq_installer}-${pkgver}.exe::https://down.qq.com/qqweb/PCQQ/PCQQ_EXE/${qq_installer}.exe"
  "run.sh")
md5sums=('5fdc20e614d945bd2ba5251420872479'
  'ff317c202b61e88c846b2c5b7384c130'
  '94d77ee0095f51d99537d6a0624fcdef')

build() {
  msg "Extracting DPKG package ..."
  mkdir -p "${srcdir}/dpkgdir"
  tar -xvf data.tar.xz -C "${srcdir}/dpkgdir"
  sed "s/\(Categories.*$\)/\1Network;/" -i "${srcdir}/dpkgdir/opt/apps/${debpkgname}/entries/applications/${debpkgname}.desktop"
  sed "s/run.sh\".*/run.sh\"/" -i "${srcdir}/dpkgdir/opt/apps/${debpkgname}/entries/applications/${debpkgname}.desktop"
  msg "Extracting Deepin Wine QQ archive ..."
  7z x -aoa "${srcdir}/dpkgdir/opt/apps/${debpkgname}/files/files.7z" -o"${srcdir}/deepinqqdir"
  msg "Cleaning up the original package directory ..."
  rm -r "${srcdir}/deepinqqdir/drive_c/Program Files/Tencent/QQ"
  #msg "Patching reg files ..."
  #patch -p1 -d "${srcdir}/deepinqqdir/" < "${srcdir}/reg.patch"
  msg "Creating font file link ..."
  ln -sf "/usr/share/fonts/wenquanyi/wqy-microhei/wqy-microhei.ttc" "${srcdir}/deepinqqdir/drive_c/windows/Fonts/wqy-microhei.ttc"
  msg "Copying latest QQ installer to ${srcdir}/deepinqqdir/drive_c/Program Files/Tencent/ ..."
  install -m644 "${srcdir}/${qq_installer}-${pkgver}.exe" "${srcdir}/deepinqqdir/drive_c/Program Files/Tencent/"
  #find -L "${srcdir}/deepinqqdir/dosdevices" -maxdepth 1 -type l -delete
  msg "Repackaging app archive ..."
  7z a -t7z -r "${srcdir}/files.7z" "${srcdir}/deepinqqdir/*"
}

package() {
  msg "Preparing icons ..."
  install -d "${pkgdir}/usr/share/applications"
  install -Dm644 "${srcdir}/dpkgdir/opt/apps/${debpkgname}/entries/applications/${debpkgname}.desktop" "${pkgdir}/usr/share/applications/${debpkgname}.desktop"
  cp -r "${srcdir}/dpkgdir/opt/apps/${debpkgname}/entries/icons/" "${pkgdir}/usr/share/"
  msg "Copying deepin files ..."
  install -d "${pkgdir}/opt/apps/${debpkgname}/files"
  install -m644 "${srcdir}/files.7z" "${pkgdir}/opt/apps/${debpkgname}/files/"
  cp ${srcdir}/dpkgdir/opt/apps/${debpkgname}/files/helper_archive* "${pkgdir}/opt/apps/${debpkgname}/files/"
  #install -m755 "${srcdir}/dpkgdir/opt/apps/${debpkgname}/files/gtkGetFileNameDlg" "${pkgdir}/opt/apps/${debpkgname}/files/"
  md5sum "${srcdir}/files.7z" | awk '{ print $1 }' > "${pkgdir}/opt/apps/${debpkgname}/files/files.md5sum"
  #install -m644 "${srcdir}/reg.patch" "${pkgdir}/opt/apps/${debpkgname}/files/"
  install -m755 "${srcdir}/run.sh" "${pkgdir}/opt/apps/${debpkgname}/files/"
}
