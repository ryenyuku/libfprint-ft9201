# Maintainer: Berkay Yıldırım <berkayildirm@gmail.com>

pkgname=libfprint-ftexx00
pkgver=1.94.4_20250112
pkgrel=1
pkgdesc="Proprietary driver for FocalTech FTE3600, FTE4800, FTE6600 and FTE6900 fingerprint readers"
arch=('x86_64')
url="https://github.com/ftfpteams/ubuntu_spi"
license=('unknown')
groups=('fprint')
depends=('gcc-libs' 'glib2' 'glibc' 'libgudev' 'libgusb' 'openssl' 'pixman' 'nss' 'focaltech-spi-dkms')
makedepends=('git' 'tar')
optdepends=('fprintd: D-Bus service to access fingerprint readers')
provides=('libfprint-2.so' 'libfprint=1.94.4')
conflicts=('libfprint')
source=("git+https://github.com/ftfpteams/ubuntu_spi.git")
sha256sums=('SKIP')

prepare() {
  cd "$srcdir/ubuntu_spi"

  # Find the latest debian package by YYYYMMDD format
  latest_deb=$(ls *.deb 2>/dev/null | grep -E '[0-9]{8}' | sed -n 's/.*\([0-9]\{8\}\).*/\1 &/p' | sort -n | tail -1 | cut -d' ' -f2-)

  # Extract the debian package
  ar x "$latest_deb"

  # Extract data archive
  tar -xf data.tar.*

  # Update udev rules for Arch (replace plugdev with uaccess)
  sed -i 's/GROUP="plugdev"/TAG+="uaccess"/' lib/udev/rules.d/60-libfprint-2.rules

  # Create systemd override file
  cat << 'EOF' > override.conf
[Service]
DeviceAllow=/dev/focal_moh_spi rw
EOF
}

package() {
  cd "$srcdir/ubuntu_spi"

  # Install library file
  install -Dm755 "usr/lib/x86_64-linux-gnu/libfprint-2.so.2.0.0" \
		"${pkgdir}/usr/lib/libfprint-2.so.2.0.0"

  # Install udev rules
  install -Dm644 "lib/udev/rules.d/60-libfprint-2.rules" \
		"${pkgdir}/usr/lib/udev/rules.d/60-libfprint-2.rules"

  # Install systemd override file
  install -Dm644 override.conf \
		"${pkgdir}/etc/systemd/system/fprintd.service.d/override.conf"

  # Create symlink
  ln -s libfprint-2.so.2.0.0 "${pkgdir}/usr/lib/libfprint-2.so.2"
  ln -s libfprint-2.so.2.0.0 "${pkgdir}/usr/lib/libfprint-2.so"
}
