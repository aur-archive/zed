# Maintainer: Jordan Christiansen <xordspar0@gmail.com>
pkgname=zed
pkgver=1.1.0
pkgrel=1
pkgdesc='A code editor built using web technologies'
arch=('i683' 'x86_64')
conflicts=('zed-git')
options=('!strip')
license=('MIT')
url='http://zedapp.org/'
if [ $CARCH == i686 ]; then
	_arch=32
	md5sums=('43b7912ea9717c0c8946a3921f133e6e')
elif [ $CARCH == x86_64 ]; then
	_arch=64
	md5sums=('3b221d81275c425ed7f2cf1f34a52e05')
fi
source=("http://download.zedapp.org/zed-linux${_arch}-v${pkgver}.tar.gz")

prepare() {
	cd "${srcdir}/${pkgname}"

	# Change the directory that the .desktop file uses for zed and nw.pad
	cp Zed.desktop.tmpl Zed.desktop
	sed -i 's_Exec=%PREFIX%/lib/zed_Exec=/usr/bin_' Zed.desktop
	sed -i 's_Icon=%PREFIX%/lib/zed_Icon=/usr/share/pixmaps_' Zed.desktop

	# Change the directory that the launcher looks for zed-bin and nw.pad
	sed -i 's_DIR=$(dirname $0)_DIR=/usr/share/zed_' zed
}

package() {
	cd "${srcdir}/${pkgname}"

	msg2 "Install editor files"
	install -D -m644 nw.pak "${pkgdir}/usr/share/${pkgname}/nw.pak"

	msg2 "Install launcher and binary"
	install -D -m755 zed "${pkgdir}/usr/bin/zed"
	install -D -m755 zed-bin "${pkgdir}/usr/share/${pkgname}/zed-bin"

	msg2 "Install .desktop file"
	install -D -m644 Zed.desktop "${pkgdir}/usr/share/applications/Zed.desktop"
	install -D -m644 Zed.svg "${pkgdir}/usr/share/pixmaps/Zed.svg"
}
