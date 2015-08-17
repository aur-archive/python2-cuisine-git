# Maintainer: Matmas <matmas@matmas.net>
pkgname=python2-cuisine-git
pkgver=20141206
pkgrel=1
pkgdesc="Chef-like functionality for Fabric"
arch=(any)
url="https://github.com/sebastien/cuisine"
license=('BSD')
depends=('python2' 'fabric')
makedepends=('git' 'python2')
optdepends=()
provides=('python2-cuisine')
conflicts=('python2-cuisine')
options=(!emptydirs)

_gitroot="git://github.com/sebastien/cuisine.git"
_gitname="cuisine"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server..."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone --depth=1 $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"

  cd "$srcdir/$_gitname"
  git clean -fdx

  msg "Starting make..."
  python2 setup.py build
}

package() {
  cd "$srcdir/$_gitname"
  python2 setup.py install --prefix=/usr --root=$pkgdir/ --optimize=1

  install -Dm644 "$srcdir/$_gitname/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
