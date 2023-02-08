pkgname=lr2oraja
pkgver=0.8.4
pkgrel=1
pkgdesc="Cross-platform rhythm game based on Java and libGDX."
arch=('x86_64')
license=('GPL3' 'unknown')
depends=('liberica-jre-8-full-bin')
makedepend=('unzip')
source=(
  'https://github.com/wcko87/lr2oraja/releases/latest/download/LR2oraja.zip'
  'beatoraja.sh'
  'skin.zip'
)
sha256sums=(
  'f2422e1b59d4d8cfe1c75aea5d1bfdd73e7a55c8afa2830681361766d62ea42c'
  'f3b1d2c33297b0572f1a60aee64baf4649c1610f59890db551937fb1cbb1f85f'
  'ef23b516537b4f52c306fd61ab9c4197192c06b7202b3b27b63481fec1042a26'
)

prepare() {
  unzip -o skin.zip
}

build() {
  unzip -o LR2oraja.zip
}

package() {
  cd "$srcdir/"
  mkdir -p "$pkgdir/opt/beatoraja"
  mkdir -p "$pkgdir/usr/lib"

  cp beatoraja.jar "$pkgdir/opt/beatoraja/beatoraja.jar" 
  cp -r skin "$pkgdir/opt/beatoraja"

  chmod -R 777 "$pkgdir/opt/beatoraja"

  install -D beatoraja.sh "$pkgdir/usr/bin/beatoraja"
}
