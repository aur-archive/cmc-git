#Mantainer: M0Rf30
pkgname=cmc-git
pkgver=20121018
pkgrel=1
pkgdesc="Cyanogenmod Compiler"
arch=('i686' 'x86_64')
url="https://github.com/lithid/Cmc-pygtk-backup"
license=('GPL3')
depends=('pygtk' 'python2-notify')
makedepends=('git')
source=(patch)

_gitroot="git://github.com/lithid/Cmc-pygtk-backup.git"
_gitname="cmc"

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
  git clone -l "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"
  patch -Np1 -i ../patch

  mkdir -p $pkgdir/usr/share/cmc/
  mkdir -p $pkgdir/usr/bin/

  cp -r src/* $pkgdir/usr/share/cmc
  mv $pkgdir/usr/share/cmc/cmc $pkgdir/usr/bin/

# Generate bytecode and some fixes
  cd $pkgdir
  find . -type f -exec sed -i s/python/python2/g {} +
  sed -i 's|if i == 256|if i == 254|g' $pkgdir/usr/share/cmc/prog/cmcompiler.py
  python2 -m compileall .
  rm -rf "$srcdir/$_gitname-build"
} 

md5sums=('186863257be8c52fe50db76c644da1c9')
