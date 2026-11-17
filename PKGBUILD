# Maintainer: Evangelos Foutras <foutrelis@archlinux.org>
# Maintainer: T.J. Townsend <blakkheim@archlinux.org>
# Maintainer: Robin Candau <antiz@archlinux.org>
# Contributor: Andrew Simmons <andrew.simmons@gmail.com>

pkgname=thunar
pkgver=4.20.10
pkgrel=1.4
pkgdesc="PATCHED-Modern, fast and easy-to-use file manager for Xfce"
arch=('x86_64')
url="https://docs.xfce.org/xfce/thunar/start"
license=('GPL-2.0-or-later' 'LGPL-2.1-only')
groups=('xfce4')
depends=('desktop-file-utils' 'libexif' 'hicolor-icon-theme' 'libnotify'
         'pcre2' 'libgudev' 'exo' 'libxfce4util' 'libxfce4ui')
makedepends=('git' 'glib2-devel' 'gobject-introspection' 'xfce4-panel' 'xfce4-dev-tools')
optdepends=('catfish: file searching'
            'gvfs: trash support, mounting with udisk and remote filesystems'
            'tumbler: thumbnail previews'
            'thunar-volman: removable device management'
            'thunar-archive-plugin: archive creation and extraction'
            'thunar-media-tags-plugin: view/edit ID3/OGG tags')
source=("git+https://gitlab.xfce.org/xfce/thunar.git#tag=$pkgname-$pkgver"
        'thunar-preferences-wayland-parent.patch'
        'thunar-rename-dialog-parent.patch'
        'thunar-bulk-rename-wayland.patch')
sha256sums=('535214e04df1a56b94233e7b6f231f30f39eafe7a67bb235b0c3b4931edd10b6'
            '6a21876a33fda75345fa5387f9f1a8571d8b6c5f00fd10f556e884d376ac1c33'
            '1c040e7e02c6a36c78b01b95c9f31389f5492018569924904a99e04fa979887f'
            '236e2bc0f7f6c7c0feea60e9461a683927bc5436a003fdb14428fec3ec2ffdbb')

prepare() {
  cd "$pkgname"
  git apply "$srcdir/thunar-preferences-wayland-parent.patch" "$srcdir/thunar-rename-dialog-parent.patch" "$srcdir/thunar-bulk-rename-wayland.patch"
  NOCONFIGURE=1 ./autogen.sh
}

build() {
  cd $pkgname
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --enable-gio-unix \
    --enable-gudev \
    --enable-notifications \
    --enable-exif \
    --enable-gtk-doc \
    --disable-debug \
    --enable-maintainer-mode
  make
}

package() {
  cd $pkgname
  make DESTDIR="$pkgdir" install
}

# vim:set ts=2 sw=2 et:
