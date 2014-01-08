# Maintainer: Marcel Huber <`echo "moc tknup liamg tä oofrebuhlecram" | rev`>
# Contributor: mathieu.clabaut <mathieu.clabaut@gmail.com>

pkgname=metastore-git
pkgver=0.r55.gd5a3600
pkgrel=1
pkgdesc='Store, compare and retrieve the metadata of files/directories/links in a file tree to/from a separate file'
arch=('i686' 'x86_64')
url="http://david.hardeman.nu/software.php#metastore"
license=('GPL2')
provides=('metastore')
conflicts=('metastore')
source=("$pkgname"::'git+https://github.com/przemoc/metastore.git')
sha256sums=('SKIP')

pkgver() {
  cd "$pkgname"
  if GITTAG="$(git describe --abbrev=0 --tags 2>/dev/null)"; then
    echo "$(sed -e "s/^${pkgname%%-git}//" -e 's/^[-_/a-zA-Z]\+//' -e 's/[_-+]/./g' <<< ${GITTAG}).r$(git rev-list --count ${GITTAG}..).g$(git log -1 --format="%h")"
  else
    echo "0.r$(git rev-list --count master).g$(git log -1 --format="%h")"
  fi
}

build() {
  cd "$srcdir/$pkgname"

  sed -i -e 's+/share/man+/man+' Makefile

  make || return 1
}

package() {
  cd "$srcdir/$pkgname"
  make DESTDIR="$pkgdir" install || return 1
  install -d -m755 examples $pkgdir/usr/share/metastore/examples
  install -m644 examples/* $pkgdir/usr/share/metastore/examples
}

# vim: set sw=2 ts=2 et:
