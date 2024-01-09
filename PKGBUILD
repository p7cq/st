# Maintainer: p7cq

pkgname=st-p7cq-git
_pkgname=st
pkgver=0.9.b23.e825c3d
pkgrel=1
pkgdesc='A fork of Simple Terminal for X from Suckless.org Community'
arch=('x86_64' 'aarch64')
license=('MIT')
depends=(libxft)
makedepends=('ncurses' 'libxext' 'git')
url=https://github.com/p7cq/st
source=(git+https://github.com/p7cq/st)
sha256sums=(SKIP)

provides=("${_pkgname}")
conflicts=("${_pkgname}")

pkgver() {
  cd ${srcdir}/${_pkgname}
  printf "%s.b%s.%s" "$(awk '/^VERSION =/ {print $3}' config.mk)" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd ${srcdir}/${_pkgname}
  make X11INC=/usr/include/X111 X11LIB=/usr/lib/X11
}

package() {
  cd ${srcdir}/${_pkgname}
  local installopts='--mode 0644 -D --target-directory'
  local shrdir="$pkgdir/usr/share"
  local licdir="$shrdir/licenses/$pkgname"
  local sourcedir=${srcdir}/${_pkgname}
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install $installopts "$licdir" "$sourcedir/LICENSE"
  install $installopts "$docdir" "$sourcedir/README.md"
  #install $installopts "$docdir" "$sourcedir/Xresources.example"
  install $installopts "$shrdir/$pkgname" "$sourcedir/st.info"
}
