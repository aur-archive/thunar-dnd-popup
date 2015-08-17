# Maintainer: David Couzelis <drcouzelis@gmail.com>
#
# (Added from thunar package)
# Contributor: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: Andrew Simmons <andrew.simmons@gmail.com>

pkgname=thunar-dnd-popup
pkgver=1.6.1
pkgrel=2
pkgdesc="Modern file manager for Xfce with the drag-and-drop menu popup restored"
arch=('i686' 'x86_64')
url="http://thunar.xfce.org"
license=('GPL2' 'LGPL2.1')
groups=('xfce4')
depends=('desktop-file-utils' 'libexif' 'hicolor-icon-theme' 'libnotify'
         'udev' 'gtk2' 'exo' 'libxfce4util' 'libxfce4ui' 'libpng')
makedepends=('intltool' 'gtk-doc' 'xfce4-panel')
optdepends=('gvfs: for trash support, mounting with udisk and remote filesystems'
            'polkit-gnome: for mounting internal partitions (needs root password)'
            'xfce4-panel: for trash applet'
            'tumbler: for thumbnail previews'
            'thunar-volman: manages removable devices'
            'thunar-archive-plugin: create and deflate archives'
            'thunar-media-tags-plugin: view/edit id3/ogg tags')
provides=('thunar')
conflicts=('thunar')
options=('!libtool')
install=$pkgname.install
source=(http://archive.xfce.org/src/xfce/thunar/1.6/Thunar-$pkgver.tar.bz2
        thunar-dnd-popup.patch)
sha256sums=('a81021af558802b8c2c6cd7db47cca262477c4f3d2b6d8cfa8dbba88568048f1'
            '9c55fdcb20cac6b1866337e13ce95dc09a4d960e8f579cb92cd64abcd0f271a4')

build() {
  cd "$srcdir/Thunar-$pkgver"

  patch -p1< "$srcdir/thunar-dnd-popup.patch"

  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --libexecdir=/usr/lib \
    --localstatedir=/var \
    --disable-static \
    --enable-gio-unix \
    --enable-dbus \
    --enable-startup-notification \
    --enable-gudev \
    --enable-notifications \
    --enable-exif \
    --enable-pcre \
    --enable-gtk-doc \
    --disable-debug
  make
}

package() {
  cd "$srcdir/Thunar-$pkgver"

  make DESTDIR=${pkgdir} install
  sed -i 's:x-directory/gnome-default-handler;::' \
    "$pkgdir/usr/share/applications/Thunar-folder-handler.desktop"
}

# vim:set ts=2 sw=2 et:
