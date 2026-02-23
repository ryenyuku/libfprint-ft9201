# Maintainer: リェンーゆく <teamworks1732@gmail.com>

pkgname=libfprint-ft9201
pkgver=1.94.4_20250219
pkgrel=1
pkgdesc="Proprietary driver for FocalTech FT9201 fingerprint readers"
arch=('x86_64')
url="https://github.com/ryenyuku/libfprint-ft9201"
license=('unknown')
groups=('fprint')
depends=('gcc-libs' 'glib2' 'glibc' 'libgudev' 'libgusb' 'openssl' 'pixman' 'nss')
makedepends=('tar')
optdepends=('fprintd: D-Bus service to access fingerprint readers')
provides=('libfprint-2.so' 'libfprint=1.94.4')
conflicts=('libfprint')
source=("https://github.com/ryenyuku/libfprint-ft9201/releases/download/1.94.4_20250219/libfprint-2-2_1.94.4+tod1-0ubuntu1.22.04.2_amd64_20250219.deb")
sha256sums=('fe8c5ebb685718075e1fc04f10378c001e149b80c283d2891318a50e0588401a')

prepare() {
  cd "$srcdir"

  # Find the latest debian package by YYYYMMDD format
  latest_deb=$(ls *.deb 2>/dev/null | grep -E '[0-9]{8}' | sed -n 's/.*\([0-9]\{8\}\).*/\1 &/p' | sort -n | tail -1 | cut -d' ' -f2-)

  # Extract the debian package
  ar x "$latest_deb"

  # Extract data archive
  tar -xf data.tar.*

  # Update udev rules for Arch (replace plugdev with uaccess)
  sed -i 's/GROUP="plugdev"/TAG+="uaccess"/' lib/udev/rules.d/60-libfprint-2.rules
}

package() {
  cd "$srcdir"

  # Install library file
  install -Dm755 "usr/lib/x86_64-linux-gnu/libfprint-2.so.2.0.0" \
		"${pkgdir}/usr/lib/libfprint-2.so.2.0.0"

  # Install udev rules
  install -Dm644 "lib/udev/rules.d/60-libfprint-2.rules" \
		"${pkgdir}/usr/lib/udev/rules.d/60-libfprint-2.rules"

  # Create symlink
  ln -s libfprint-2.so.2.0.0 "${pkgdir}/usr/lib/libfprint-2.so.2"
  ln -s libfprint-2.so.2.0.0 "${pkgdir}/usr/lib/libfprint-2.so"
}
