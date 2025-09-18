# Maintainer: https://github.com/nathanielx

pkgname=logiops
pkgver=0.3.5
pkgrel=1
pkgdesc="An unofficial userspace driver for HID++ Logitech devices"
arch=('x86_64' 'i686' 'aarch64' 'armv7h')
url="https://github.com/PixlOne/logiops"
license=('GPL3')
depends=('libevdev' 'libconfig' 'systemd-libs' 'glib2')
makedepends=('cmake' 'git')
backup=('etc/logid.cfg')
install="$pkgname.install"
source=("$pkgname::git+https://github.com/PixlOne/logiops.git#tag=v$pkgver")
sha256sums=('SKIP')

prepare() {
    cd "$pkgname"
    git submodule update --init --recursive
}

build() {
    cd "$pkgname"
    
    cmake -B build -S . \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=lib
    
    cmake --build build
}

package() {
    cd "$pkgname"
    
    DESTDIR="$pkgdir" cmake --install build
    
    install -Dm644 logid.example.cfg "$pkgdir/usr/share/doc/$pkgname/logid.example.cfg"
    install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
    install -Dm644 TESTED.md "$pkgdir/usr/share/doc/$pkgname/TESTED.md"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
