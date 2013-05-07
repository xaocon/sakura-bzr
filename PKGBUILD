# Maintainer: Evan Pitstick <nerdx00 NOSPAM gmail DOT com>
# Based on: https://www.archlinux.org/packages/community/x86_64/sakura/

pkgname=sakura-bzr
_name=sakura
pkgver=433
pkgrel=1
pkgdesc="A terminal emulator based on GTK and VTE"
arch=('i686' 'x86_64')
url="https://launchpad.net/sakura"
license=('GPL')
depends=('vte3' 'libxft' 'desktop-file-utils')
makedepends=('cmake' 'bzr')
provides=('sakura')
conflicts=('sakura')
source=("${pkgname}::bzr+https://launchpad.net/${_name}/trunk")
install=${pkgname}.install
sha1sums=('SKIP')

pkgver() {

	cd ${srcdir}/${pkgname}
	bzr revno

}

prepare() {

	# Set default font to something more generic
	sed -i 's|#define DEFAULT_FONT "Ubuntu Mono,monospace 13"|#define DEFAULT_FONT "Monospace 10"|g' \
		${srcdir}/${pkgname}/src/sakura.c

}

build() {
	
	cd ${srcdir}/${pkgname}

 	# build & install
	cmake -DCMAKE_INSTALL_PREFIX=/usr .
	make

}

package() {
	
	cd ${srcdir}/${pkgname}

	make DESTDIR=${pkgdir} install
	# extract the keybindings from the installed documentation, rest is only relevant during build time
	awk '/^Keybindings/{f="'${pkgdir}'/usr/share/doc/'${_name}'/KEYBINDINGS"} f{print > f} /^END/' \
		${pkgdir}/usr/share/doc/${_name}/INSTALL
	rm ${pkgdir}/usr/share/doc/${_name}/INSTALL
	
}

# vim: ts=4 sts=4 sw=4 noet
