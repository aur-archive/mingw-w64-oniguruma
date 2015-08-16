pkgname=mingw-w64-oniguruma
pkgver=5.9.2
pkgrel=2
pkgdesc="a regular expressions library (mingw-w64)"
arch=(any)
url="http://www.geocities.jp/kosako3/oniguruma/"
license=("BSD")
makedepends=(mingw-w64-gcc)
depends=(mingw-w64-crt)
options=(!libtool !strip !buildflags)
source=("http://www.geocities.jp/kosako3/oniguruma/archive/onig-$pkgver.tar.gz")
md5sums=('0f4ad1b100a5f9a91623e04111707b84')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  unset LDFLAGS
  for _arch in ${_architectures}; do
    mkdir -p "${srcdir}/${pkgname}-${pkgver}-build-${_arch}"
    cd "${srcdir}/${pkgname}-${pkgver}-build-${_arch}"
    ${srcdir}/onig-${pkgver}/configure \
      --prefix=/usr/${_arch} \
      --build=$CHOST \
      --host=${_arch}
    make
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "${srcdir}/${pkgname}-${pkgver}-build-${_arch}"
    make DESTDIR="$pkgdir" install
    find "$pkgdir/usr/${_arch}" -name '*.a' | xargs -rtl1 ${_arch}-strip -g
  done
}
