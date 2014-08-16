# Maintainer: Hugh Young
# Original by: Jan Frederick Eick <j.f.eick@gmx.de>

pkgname=xf86-input-synaptics-mtpatch
pkgver=1.8.0
pkgrel=1
pkgdesc="Synaptics driver for notebook touchpads patched for pass through of multitouch events"
arch=('i686' 'x86_64')
license=('custom')
url="http://xorg.freedesktop.org/"
depends=('libxtst' 'mtdev')
makedepends=('xorg-server-devel' 'X-ABI-XINPUT_VERSION=21' 'libxi' 'libx11' 'resourceproto' 'scrnsaverproto') 
conflicts=('xorg-server<1.14.0' 'X-ABI-XINPUT_VERSION<21' 'X-ABI-XINPUT_VERSION>=22')
replaces=('synaptics')
provides=('synaptics')
conflicts=('synaptics')
groups=('xorg-drivers' 'xorg')
options=(!libtool)
backup=('etc/X11/xorg.conf.d/10-synaptics.conf')
source=(http://xorg.freedesktop.org/releases/individual/driver/xf86-input-synaptics-${pkgver}.tar.bz2
        https://raw.githubusercontent.com/cotko/archlinux-xf86-input-synaptics-mtpatch/master/send_multitouch_events.patch
        https://raw.githubusercontent.com/cotko/archlinux-xf86-input-synaptics-mtpatch/master/10-synaptics.conf)
sha256sums=('9bf27632aaa6c5e62621ca9c2ca00f9b309c85b039ee33cd592b189fc872c37a'
            'c4083e6006e2a54d2b7d0dacc028ee6e8d786d6c2b071c6b9e30d863639ca8f0'
	    '6d61b3f73db8e5b34d8e461c992280c18b9f11b7d2ee2f336df2ce1d7a4be8d6'
            )

build() {
  cd "${srcdir}/xf86-input-synaptics-${pkgver}"
  patch -Np1 -i ../send_multitouch_events.patch
  ./configure --prefix=/usr
  make
}

package() {
  cd "${srcdir}/xf86-input-synaptics-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -m755 -d "${pkgdir}/etc/X11/xorg.conf.d"
  install -m644 "${srcdir}/10-synaptics.conf" "${pkgdir}/etc/X11/xorg.conf.d/"
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/"

  rm -rf "${pkgdir}/usr/share/X11"
}

