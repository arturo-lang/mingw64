# Maintainer: https://github.com/arturo-lang

pkgname=arturo
pkgver=0.10.0
pkgrel=1
pkgdesc="Simple, expressive & portable programming language for efficient scripting."
arch=('x86_64')
url="https://arturo-lang.io/"
license=("spdx:MIT")
purl=("pkg:github/arturo-lang/arturo@v${pkgver}")


msys2_repository_url="https://github.com/arturo-lang/arturo"
mingw_arch=('mingw64')

depends=(
  mingw-w64-x86_64-gmp
  mingw-w64-x86_64-mpfr
  mingw-w64-x86_64-mpfr
  mingw-w64-x86_64-sqlite3
)

makedepends=(
  base-devel
  git
  zip
  unzip
)

source=("https://github.com/arturo-lang/arturo/archive/refs/tags/v${pkgver}.zip")
sha256sums=('D7317D3DD0DA4E72F60F08242D332D2C807A3E8CBF790B6B2FD20E81ADE008FC')

install=arturo.install

options=(
  !staticlibs
  !libtool
  !strip
)

prepare() {
  git clone https://github.com/nim-lang/Nim "$srcdir/Nim"
  cd "$srcdir/Nim"
  git checkout v2.2.6
  cmd //C build_all.bat
}

build() {
  cd "$srcdir/arturo-$pkgver"
  ../Nim/bin/nim build.nims -l
}

package() {
  install -d "$pkgdir/opt/arturo" 
  cp -r "$srcdir/arturo-$pkgver/bin" "$pkgdir/opt/arturo"
}
