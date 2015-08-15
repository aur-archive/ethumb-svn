# Maintainer: Doug Newgard <scimmia22 at outlook dot com>
# Contributor: Ronald van Haren <ronald.archlinux.org>

pkgname=ethumb-svn
pkgver=82132
pkgrel=1
pkgdesc="Thumbnail generation library in EFL"
arch=('i686' 'x86_64')
url="http://www.enlightenment.org"
license=('LGPL2.1')
depends=('libexif' 'efl-svn')
makedepends=('subversion')
conflicts=('ethumb')
provides=('ethumb')
options=('!libtool' '!strip')

_svntrunk="http://svn.enlightenment.org/svn/e/trunk/ethumb"
_svnmod="ethumb"

build() {
  cd "$srcdir"

  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  svn export "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  ./autogen.sh --prefix=/usr \
	--libexecdir=/usr/lib/$_svnmod
  make
}

package(){
  cd "$_svnmod-build"
  make DESTDIR="$pkgdir" install

  rm -r "$srcdir/$_svnmod-build"
}
