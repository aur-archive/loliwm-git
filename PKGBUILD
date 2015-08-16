pkgname=loliwm-git
pkgver=r233.1e6a1de
pkgrel=3

pkgdesc='A dynamic window manager and wayland compositor based on the wlc.'
url='https://github.com/Cloudef/loliwm'
arch=('i686' 'x86_64')
license=('GPL')

depends=('pixman' 'libxkbcommon' 'wlc-git')
makedepends=('git' 'cmake')
optdepends=('weston: To test weston clients in loliwm.'
            'bemenu: Dynamic menu similar to dmenu for launching programs.')

provides=('loliwm')
conflicts=('loliwm')

source=('git://github.com/Cloudef/loliwm')
        # 'git://github.com/Cloudef/chck')

md5sums=('SKIP')

# Once this software becomes more stable these requirements will be dropped but
# for the time being I recommend leaving them enabled so you may contribute
# useful backtraces to the developer and help remove any errors.
options=('debug' '!strip')

pkgver() {
    cd loliwm
    printf 'r%s.%s' "$(git rev-list --count HEAD)" "$(git describe --always)"
}

# prepare() {
#     cd loliwm
#     git submodule init
#     git config submodule.chck.url "$srcdir"/chck
#     git submodule update chck
# }

build() {
    cd loliwm
    cmake -DCMAKE_INSTALL_PREFIX=/usr
    make
}

package() {
    cd loliwm
    make DESTDIR="$pkgdir" install

    # 2014-11-09: Now needs to setuid for VT switching.  loliwm itself drops
    # permissions ASAP but this is still undesirable and should be unnecessary
    # once logind support lands.
    chmod 6755 -- "$pkgdir"/usr/bin/loliwm
}
