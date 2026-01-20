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
mingw_arch=('mingw64' 'ucrt64' 'clang64')

depends=()
makedepends=(
  base-devel
  git
  p7zip
  zip
  unzip
  mingw-w64-x86_64-toolchain
  mingw-w64-x86_64-nim
  mingw-w64-x86_64-mpfr
)
source=("https://github.com/arturo-lang/arturo/archive/refs/tags/v${pkgver}.zip")
sha256sums=('77b724d37fc70d3fb5d8d040b3c8ead103cf8323c1c32a650ccdba4465df6d86')

install=arturo.install

options=(
  !staticlibs
  !libtool
  !strip
)

prepare() {
  unzip "v${pkgver}.zip" "${srcdir}"
}

build() {
  nim build.nims -l
}

package() {
  install -d "$pkgdir/opt/arturo" "${srcdir}/bin"
}
