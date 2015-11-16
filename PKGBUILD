# $Id: PKGBUILD 139577 2015-09-08 08:29:26Z lcarlier $
# Maintainer: Alexander Baldeck <alexander@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

_pkgbasename=libxcb
pkgname=lib32-$_pkgbasename
pkgver=1.11.1
pkgrel=1
pkgdesc="X11 client-side library (32-bit)"
arch=(x86_64)
url="http://xcb.freedesktop.org/"
depends=('lib32-libxdmcp' 'lib32-libxau' $_pkgbasename)
makedepends=('pkgconfig' 'libxslt' 'python' 'xorg-util-macros' 'gcc-multilib'
             'autoconf')
license=('custom')
source=(${url}/dist/${_pkgbasename}-${pkgver}.tar.bz2
        libxcb-1.1-no-pthread-stubs.patch)
sha256sums=('b720fd6c7d200e5371affdb3f049cc8f88cff9aed942ff1b824d95eedbf69d30'
            '3923bcb1930b851012968435909597d8d5251c72153511cb2982636c97100cc3')

prepare() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"

  patch -Np1 -i "${srcdir}/libxcb-1.1-no-pthread-stubs.patch"
  autoreconf -vfi
}

build() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"

  export CC="gcc -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  ./autogen.sh \
	  --prefix=/usr \
	  --enable-xinput \
          --enable-xkb \
	  --libdir=/usr/lib32 \
	  --disable-static
  make
}

package() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"

  make DESTDIR="${pkgdir}" install

  rm -rf "${pkgdir}"/usr/{include,share}

  mkdir -p "$pkgdir/usr/share/licenses"
  ln -s $_pkgbasename "$pkgdir/usr/share/licenses/$pkgname" 
}
