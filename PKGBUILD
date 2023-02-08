pkgname=lr2oraja
pkgver=build1696491429
pkgrel=1
pkgdesc="The latest build of beatoraja, but compiled using LR2 judges and gauges."
arch=('x86_64')
depends=('liberica-jre-8-full-bin')
makedepend=('unzip')
source=(
  "https://github.com/wcko87/lr2oraja/releases/download/${pkgver}/LR2oraja.zip"
  'beatoraja.sh'
  'skin.zip'
)
sha256sums=(
  'f2422e1b59d4d8cfe1c75aea5d1bfdd73e7a55c8afa2830681361766d62ea42c'
  'f3b1d2c33297b0572f1a60aee64baf4649c1610f59890db551937fb1cbb1f85f'
  'ef23b516537b4f52c306fd61ab9c4197192c06b7202b3b27b63481fec1042a26'
)
license=('GPL3' 'unknown' 'GPL3')

prepare() {
  unzip -o skin.zip
}

build() {
  unzip -o LR2oraja.zip
}

package() {
  rajadir="$pkgdir/opt/beatoraja"

  cd "$srcdir/"
  mkdir -p "$rajadir"
  mkdir -p "$pkgdir/usr/lib"
  mkdir -p "$pkgdir/usr/share/applications"
  mkdir -p "$pkgdir/usr/share/pixmaps"

  # Move all required Beatoraja Files
  cp beatoraja.jar "$rajadir/beatoraja.jar" 
  cp -r skin "$rajadir"
  mkdir -p "$rajadir/screenshot" "$rajadir/bgm"
  chmod -R 777 "$pkgdir/opt/beatoraja"

  # Create Desktop entry
  cp ./lr2oraja-icon.png "$pkgdir/usr/share/pixmaps"
  desktopEntry="$pkgdir/usr/share/applications/lr2oraja.desktop"
  touch "$desktopEntry"
  echo "[Desktop Entry]" >> "$desktopEntry"
  echo "Type=Application" >> "$desktopEntry"
  echo "Terminal=true" >> "$desktopEntry"
  echo "Exec=$pkgdir/usr/bin/beatoraja" >> "$desktopEntry"
  echo "Version=$pkgver" >> "$desktopEntry"
  echo "Name=LR2oraja" >> "$desktopEntry"
  echo "Categories=Games;" >> "$desktopEntry"
  echo "Icon=lr2oraja-icon" >> "$desktopEntry"

  # Install LR2oraja
  install -D beatoraja.sh "$pkgdir/usr/bin/beatoraja"
}
