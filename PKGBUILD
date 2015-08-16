# $Id: PKGBUILD 135478 2011-08-14 09:26:08Z allan $
# Maintainer: josephgbr <rafael.f.f1@gmail.com>
# Contributor: Florian Pritz <flo@xssn.at>

_pkgbasename=gmp
pkgname=lib32-$_pkgbasename
pkgver=5.0.2
pkgrel=5
pkgdesc="A free library for arbitrary precision arithmetic (32-bit)"
arch=('x86_64')
url="http://gmplib.org/"
depends=('lib32-gcc-libs' $_pkgbasename)
makedepends=(gcc-multilib)
license=('LGPL3')
options=(!libtool)
source=(ftp://ftp.gnu.org/gnu/gmp/gmp-${pkgver}.tar.bz2
        538dfce27f41.patch)
md5sums=('0bbaedc82fb30315b06b1588b9077cd3'
         'a769be9c41618ca9c35d83375e7097d0')

build() {
  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  patch -Np1 -i $srcdir/538dfce27f41.patch

  export ABI=32
  ./configure \
    --prefix=/usr --infodir=/usr/share/info \
    --enable-cxx --libdir=/usr/lib32 \
    --includedir=/usr/lib32/gmp

  #Put gmp.h in the same folder as gmpxx.h
  sed -i 's/$(exec_prefix)\/include/$\(includedir\)/' Makefile

  make
}

check() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  make check
}

package() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  make DESTDIR="${pkgdir}" install

  rm -rf "${pkgdir}"/usr/{include,share,bin}
}
