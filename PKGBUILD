# $Id$
# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgname=npm
pkgver=5.1.0
pkgrel=1
pkgdesc='A package manager for javascript'
arch=('any')
url='https://www.npmjs.com/'
license=('custom:Artistic')
depends=('nodejs' 'semver')
provides=('nodejs-node-gyp')
makedepends=('procps-ng' 'marked-man')
optdepends=('python2: for node-gyp')
options=('!emptydirs')
source=("$pkgname-$pkgver.tar.gz::https://github.com/npm/npm/archive/v$pkgver.tar.gz")
sha512sums=('c0412646dd09ed75932d3c530a0ba22ad5b8162449aa5c5dcd7882063480970d9473276b841f24e6918e2e47912f3e4542c08a8dc8e342cf45bc21378496885d')

prepare() {
  cd npm-$pkgver
  ln -s /usr/bin/marked{,-man} node_modules/.bin/
}

build() {
  cd npm-$pkgver
  make
}

package() {
  cd npm-$pkgver
  make NPMOPTS="--prefix=\"$pkgdir/usr\"" install

  # Why 777? :/
  chmod -R u=rwX,go=rX "$pkgdir"

  # Fix files owned by nobody:
  chown -R root "$pkgdir"/usr/lib/node_modules

  # Fix wrong symlinks
  rm "$pkgdir/usr/lib/node_modules/npm"
  cp -r . "$pkgdir/usr/lib/node_modules/npm"

  # Provide node-gyp executable
  cp "$pkgdir"/usr/lib/node_modules/npm/bin/node-gyp-bin/node-gyp "$pkgdir"/usr/bin/node-gyp
  sed -i 's|"`dirname "$0"`/../../|"`dirname "$0"`/../lib/node_modules/npm/|' "$pkgdir"/usr/bin/node-gyp

  # Experimental dedup
  cd "$pkgdir"/usr/lib/node_modules/$pkgname/node_modules
  for dep in semver; do
    rm -r $dep;
    node "$srcdir"/npm-$pkgver/bin/npm-cli.js link $dep;
  done

  install -Dm644 "$srcdir"/npm-$pkgver/LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
