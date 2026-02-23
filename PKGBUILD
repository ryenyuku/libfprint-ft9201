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
source=("libfprint-2.so.2.0.0" "libgusb.so.2" "60-libfprint-2.rules")
sha256sums=('33be46c6ed984a81380d3dfb80f88cdde0057043992e3d86767501bf4a6698ed'
            '04af98a8a9c2528966c93cea3c3fd5c1b67b002a65a2e875e70e025d28419da6'
            '34cc642650e74033f6ac4199b6a27f15e792252779e015248e8725ba36324f1a')

package() {
  cd "$srcdir"

  # Install library file
  install -Dm755 "libfprint-2.so.2.0.0" \
		"${pkgdir}/usr/lib/libfprint-2.so.2.0.0"

  # Install libgusb from Ubuntu 22.04
  install -Dm755 "libgusb.so.2" \
                "${pkgdir}/opt/libfprint-ft9201/libgusb.so.2"

  # Install udev rules
  install -Dm644 "60-libfprint-2.rules" \
		"${pkgdir}/usr/lib/udev/rules.d/60-libfprint-2.rules"

  # Create symlink
  ln -s libfprint-2.so.2.0.0 "${pkgdir}/usr/lib/libfprint-2.so.2"
  ln -s libfprint-2.so.2.0.0 "${pkgdir}/usr/lib/libfprint-2.so"
}
