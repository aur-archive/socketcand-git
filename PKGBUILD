# Maintainer: Jan-Niklas Meier <dschanoeh@googlemail.com>
pkgname=socketcand-git
pkgver=20120324
pkgrel=1
pkgdesc="Socket CAN daemon"
arch=('i686' 'x86_64')
url="https://github.com/dschanoeh/socketcand"
license=('GPLv2')
groups=()
depends=()
makedepends=(git libconfig)
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=()
noextract=()
md5sums=()

_gitroot=http://github.com/dschanoeh/socketcand.git
_gitname=socketcand

build() {
cd "$srcdir"

msg "Connecting to $_gitroot..."
if [[ -d $_gitname ]]; then
cd $_gitname && git pull origin && cd ..
msg2 "Local files updated"
else
git clone $_gitroot
msg2 "Git checkout done"
fi

rm -rf $_gitname-build
git clone $_gitname $_gitname-build
cd $_gitname-build

msg "Starting configure..."

./configure --enable-rc-script --disable-init-script --mandir=/usr/share/man/man1

msg "Starting make..."
make
}

package() {
cd "$srcdir/$_gitname-build"
mkdir -p $pkgdir/usr/share/man/man1
mkdir -p $pkgdir/etc/rc.d
mkdir -p $pkgdir/usr/local/bin
make install SCRIPT="rc" PREFIX="/usr" DESTDIR="$pkgdir"
chmod +x $pkgdir/etc/rc.d/socketcand
}
