#-----------------------------------------------------------------------------#
#                                                                             #
# Maintainers: Arturo Programming Language <https://github.com/arturo-lang>   #
#                                                                             #
# We keep a reference repository for this package at                          #
# https://github.com/arturo-lang/mingw64.                                     #
#                                                                             #
# In that repository, we build the package via CI to make sure everything     #
# is working before submiting a new update here.                              #
#                                                                             #
#-----------------------------------------------------------------------------#

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
  mingw-w64-x86_64-gcc-libs
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

  # Build Nim compiler from source
  git clone https://github.com/nim-lang/Nim "$srcdir/Nim"
  cd "$srcdir/Nim"
  git checkout v2.2.6
  cmd //C build_all.bat

}

build() {
  cd "$srcdir/arturo-$pkgver"
  # Using dev flag to build webview DLLs
  ../Nim/bin/nim build.nims -l --dev
}

package() {
  install -d "$pkgdir/opt/arturo" 
  cp -r "$srcdir/arturo-$pkgver/bin" "$pkgdir/opt/arturo"

  # Bundle runtime DLLs so arturo.exe works without relying on system PATH
  local bindir="$pkgdir/opt/arturo/bin"
  local dlls=(
    libgcc_s_seh-1.dll
    libgmp-10.dll
    libmpfr-6.dll
    libwinpthread-1.dll
    libsqlite3-0.dll
  )

  for dll in "${dlls[@]}"; do
    if [ -f "/mingw64/bin/$dll" ]; then
      cp "/mingw64/bin/$dll" "$bindir/"
    fi
  done

  # Rename sqlite3 DLL
  mv "$bindir/libsqlite3-0.dll" "$bindir/sqlite3_64.dll"
  cp "$srcdir/arturo-$pkgver/src/extras/webview/deps/dlls/x64/webview.dll" "$bindir/"
  cp "$srcdir/arturo-$pkgver/src/extras/webview/deps/dlls/x64/WebView2Loader.dll" "$bindir/"

}