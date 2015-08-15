# Maintainer: oke3 < Sekereg [at] gmx [dot] com >
# Contributor: neuromante <lorenzo.nizzi.grifi@gmail.com>

pkgname=gkeyfile-sharp-git
pkgver=20120109
pkgrel=1
pkgdesc="Mono bindings for GLib’s GKeyFile"
arch=('any')
url="http://github.com/mono/gkeyfile-sharp"
license=('LGPL')
depends=('gtk-sharp-2')
makedepends=('git')
provides=('gkeyfile-sharp')
conflicts=('gkeyfile-sharp')
options=('!makeflags')

_gitroot="git://github.com/mono/gkeyfile-sharp.git"
_gitname="gkeyfile-sharp"

build() {
    cd "$srcdir"
    msg "Connecting to GIT server...."

    if [[ -d "$_gitname" ]]; then
        cd "$_gitname" && git pull origin
        msg "The local files are updated."
    else
        git clone "$_gitroot" "$_gitname"
    fi

    msg "GIT checkout done or server timeout"
    msg "Starting make..."

    rm -rf "$srcdir/$_gitname-build"
    git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
    cd "$srcdir/$_gitname-build"

    ./autogen.sh --prefix=/usr --sysconfdir=/etc --localstatedir=/var

    make
}

package() {
    cd "$srcdir/$_gitname-build"

    make DESTDIR="$pkgdir" install
}
