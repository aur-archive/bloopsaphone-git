pkgname=bloopsaphone-git
pkgver=20120729
pkgrel=1
pkgdesc="A small program and library  for writing chiptune-style
songs in C or Ruby."
arch=('i686' 'x86_64')
url="http://github.com/localhost/bloopsaphone/tree/master"
depends=('portaudio' 'ruby')
makedepends=('ragel')
license=('custom')
_gitroot="git://github.com/localhost/bloopsaphone.git"
_gitname="bloopsaphone"

build() {
 cd "$srcdir"
 msg "Connecting to the bloopsaphone git repository..."

 if [ -d "$srcdir/$_gitname" ] ; then
   cd $_gitname && git pull origin
   msg "The local files are updated."
 else
   git clone $_gitroot
 fi

 msg "GIT checkout done or server timeout"
 msg "Starting make..."

 cd "$srcdir"

 rm -rf $_gitname-build
 git clone $_gitname $_gitname-build
 cd $_gitname-build

 make || return 1
 make ruby || return 1
 install -D ext/ruby/bloops.so \
   "$pkgdir/usr/lib/ruby/site_ruby/1.8/$CARCH-linux/bloops.so" ||
 return 1
 install -D ext/ruby/bloops.so \
   "$pkgdir/usr/lib/ruby/site_ruby/1.9.1/$CARCH-linux/bloops.so" ||
 return 1
 install -D bloopsawhat "$pkgdir/usr/bin/bloopsawhat" || return 1
}
