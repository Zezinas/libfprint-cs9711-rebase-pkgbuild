# Maintainer: Zezinas
# Based on AUR package by reburn <au0228@outlook.com>

pkgname=libfprint-cs9711-rebase-git-zez
_pkgname=libfprint-CS9711
pkgver=1.94.10+1.r1866.20260216.02b285c
pkgrel=1
pkgdesc="libfprint with CS9711 fingerprint driver support (personal fork, cs9711-rebase branch)"
arch=(x86_64)
url="https://github.com/Zezinas/libfprint-CS9711"
license=(LGPL-2.1-or-later)
depends=(
  gcc-libs
  glib2
  glibc
  libgudev
  libgusb
  opencv
  openssl
  pixman
)
makedepends=(
  git
  glib2-devel
  gobject-introspection
  gtk-doc
  meson
  python-cairo
  python-gobject
  systemd
  cmake
  doctest
)
checkdepends=(
  cairo
  umockdev
  doctest
)
provides=("libfprint=${pkgver}" "libfprint-2.so" "libfprint-cs9711")
conflicts=(libfprint)
groups=(fprint)
source=("git+https://github.com/Zezinas/libfprint-CS9711.git#branch=cs9711-rebase")
sha256sums=('SKIP')

pkgver() {
  cd "$_pkgname"
  _ver="$(git describe --tags --long 2>/dev/null | sed -E -e 's|^[vV]||' -e 's|\-g[0-9a-f]*$||' | tr '-' '+')"
  if [ -z "$_ver" ]; then
    _ver="1.94.10+1"
  fi
  _rev="$(git rev-list --count HEAD)"
  _date="$(git log -1 --date=format:'%Y%m%d' --format='%ad')"
  _hash="$(git rev-parse --short HEAD)"
  printf '%s' "${_ver}.r${_rev}.${_date}.${_hash}"
}

build() {
  local meson_options=(
    -D installed-tests=false
  )
  arch-meson "$_pkgname" build "${meson_options[@]}"
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
}
