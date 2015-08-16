pkgname=nesicide-git
pkgver=20130421
pkgrel=1
pkgdesc="IDE for the Nintendo NES"
arch=('i686' 'x86_64')
url="http://www.nesicide.com"
license=('custom')
depends=('qt4' 'sdl_sound' 'lua' 'cc65-git')
makedepends=('git')
provides=()
conflicts=()
install=
source=()
md5sums=()

_gitroot="git://github.com/christopherpow/nesicide.git"
_gitname="nesicide-git"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"

  for d in libs/nes libs/c64 apps/nes-emulator apps/ide; do
    msg "Making in $d"
    cd "$srcdir/$_gitname-build/$d" && PREFIX="$pkgdir/usr" qmake && make
  done
}

package() {
  cd "$srcdir/$_gitname-build"
  mkdir -p "$pkgdir/usr/lib"
  mkdir -p "$pkgdir/usr/bin"

  for d in libs/nes libs/c64 apps/nes-emulator apps/ide; do
    msg "Installing in $d"
    cd "$srcdir/$_gitname-build/$d" && make install
  done
}
