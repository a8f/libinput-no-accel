pkgname=libinput
pkgver=1.16.4
pkgrel=1
pkgdesc="Input device management and event handling library"
url="https://www.freedesktop.org/wiki/Software/libinput/"
arch=(x86_64)
license=(custom:X11)
depends=('mtdev' 'systemd' 'libevdev' 'libwacom')
provides=('libinput')
conflicts=('libinput')
# upstream doesn't recommend building docs
makedepends=('gtk3' 'meson') # 'doxygen' 'python-sphinx' 'python-recommonmark'
optdepends=('gtk3: libinput debug-gui'
            'python-pyudev: libinput measure'
            'python-evdev: libinput measure')
source=(git+https://github.com/a8f/libinput-no-accel)
sha512sums=('SKIP')
validpgpkeys=('SKIP')

pkgver() {
	cd libinput-no-accel
	git describe --long | sed -r 's/([^-]*-g)/r\1/;s/-/./g'
}

build() {
  arch-meson libinput-no-accel build \
    -Dudev-dir=/usr/lib/udev \
    -Dtests=false \
    -Ddocumentation=false
  ninja -C build
}

package() {
  DESTDIR="$pkgdir" ninja -C build install
}
