# Maintainer: uffe _.at._ uffe _.dot._ org

pkgname=minipro-git
pkgver=0.4.r78.gce259af
pkgrel=2
pkgdesc="Open source programming utility for autoelectric.cn Minipro TL866"
url="https://gitlab.com/DavidGriffith/minipro"
arch=("i686" "x86_64")
license=("GPL")
depends=("libusb")
optdepends=('srecord: for miniprohex (frontend for .bin file conversion)')
makedepends=("git")
source=($pkgname::git+https://gitlab.com/DavidGriffith/minipro.git)
conflicts=("minipro")
provides=("minipro")
md5sums=("SKIP")

pkgver()
{
  cd "${srcdir}/${pkgname}"
  ( set -o pipefail
    git describe --long --tags 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build()
{
  cd "${srcdir}/${pkgname}"
  make PREFIX="/usr"
}

package()
{
  cd "${srcdir}/${pkgname}"
  make DESTDIR="${pkgdir}" PREFIX="/usr" COMPLETIONS_DIR="/usr/share/bash-completion/completions" install
  rm ${pkgdir}/usr/lib/udev/rules.d/61-minipro-plugdev.rules
}

# vim: ts=2 sw=2 et:
