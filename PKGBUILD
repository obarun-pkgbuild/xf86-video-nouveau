# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/xf86-video-nouveau
# 						Maintainer: Andreas Radke <andyrtr@archlinux.org>
# 						Contributor: buddabrod <buddabrod@gmail.com>

pkgname=xf86-video-nouveau
pkgver=1.0.15
pkgrel=3
pkgdesc="Open Source 2D acceleration driver for nVidia cards"
arch=('x86_64')
url="http://nouveau.freedesktop.org/"
license=('GPL')
depends=('mesa')
makedepends=('xorg-server-devel' 'X-ABI-VIDEODRV_VERSION=23')
conflicts=('xorg-server<1.19' 'X-ABI-VIDEODRV_VERSION<23' 'X-ABI-VIDEODRV_VERSION>=24')
groups=('xorg-drivers')
source=(https://xorg.freedesktop.org/archive/individual/driver/$pkgname-$pkgver.tar.bz2)
sha256sums=('aede10fd395610a328697adca3434fb14e9afbd79911d6c8545cfa2c0e541d4c')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal


build() {
  cd "${pkgname}-${pkgver}"
  
  # Since pacman 5.0.2-2, hardened flags are now enabled in makepkg.conf
  # With them, module fail to load with undefined symbol.
  # See https://bugs.archlinux.org/task/55102 / https://bugs.archlinux.org/task/54845
  export CFLAGS=${CFLAGS/-fno-plt}
  export CXXFLAGS=${CXXFLAGS/-fno-plt}
  export LDFLAGS=${LDFLAGS/,-z,now}

  ./configure --prefix=/usr
  make
}

package() {
  cd "${pkgname}-$pkgver"

  make DESTDIR="$pkgdir" install
}
