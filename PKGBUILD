# Maintainer: Pfych <contact at pfy dot ch>
pkgname=lr2oraja
pkgver=build6711481041
pkgrel=3
pkgdesc="The latest build of beatoraja, but compiled using LR2 judges and gauges."
arch=('x86_64')
depends=('liberica-jre-8-full-bin' 'portaudio')
makedepend=('unzip')
source=(
  "https://github.com/wcko87/lr2oraja/releases/download/${pkgver}/LR2oraja.zip"
  'https://github.com/pfych/lr2oraja-pkgbuild/releases/download/skin/skin.zip'
  'https://github.com/TNG-dev/tachi-beatoraja-ir/releases/download/v3.0.0/bokutachiIR-3.0.0.jar'
  'libjportaudio.so'
  'beatoraja.sh'
  'lr2oraja-icon.png'
)
sha256sums=(
  '5f6dceccaeb0e786dd1658c1b481e8db114bc90a8a1056bf65753e8936ed3369' # LR2oraja.zip
  'ef23b516537b4f52c306fd61ab9c4197192c06b7202b3b27b63481fec1042a26' # skin.zip
  '3754959d5d6f121dbeed3a78dec2b91a26e915ff4ce68fdee4262b89ad150cb9' # bokutachiIR
  'a65d1290d3ee7710f9327c040e6369bf7587eb3609835ed782caaf0ac02d84ed' # libjportaudio.so
  'fd2638ec66871deec093f736298b5592caadb89b5686648a28e4d082c207bb50' # beatoraja.sh
  '0ec1382690cd847055d1b8e6da36ad6846598b45b25acca5eb5e301a5048da03' # lr2oraja-icon.png
)
license=(
  'GPL3'
  'GPL3'
  'MIT'
  'unknown'
  'unknown'
)

prepare() {
  # Beatoraja will fail to load without a default skin
  unzip -o skin.zip
}

build() {
  unzip -o LR2oraja.zip
}

package() {
  # Create required directories
  cd "$srcdir/"
  mkdir -p "$pkgdir/opt/beatoraja/ir"
  mkdir -p "$pkgdir/usr/lib"
  mkdir -p "$pkgdir/usr/share/applications"
  mkdir -p "$pkgdir/usr/share/pixmaps"

  # Move all required Beatoraja Files
  cp libjportaudio.so "$pkgdir/usr/lib"
  cp beatoraja.jar "$pkgdir/opt/beatoraja/beatoraja.jar" 
  cp -r skin "$pkgdir/opt/beatoraja"
  cp "bokutachiIR-3.0.0.jar" "$pkgdir/opt/beatoraja/ir"
  chmod -R 777 "$pkgdir/opt/beatoraja"

  # Create Desktop entry
  cp lr2oraja-icon.png "$pkgdir/usr/share/pixmaps"
  desktopEntry="$pkgdir/usr/share/applications/lr2oraja.desktop"
  touch "$desktopEntry"
  echo "[Desktop Entry]" >> "$desktopEntry"
  echo "Type=Application" >> "$desktopEntry"
  echo "Terminal=true" >> "$desktopEntry"
  echo "Exec=/usr/bin/beatoraja" >> "$desktopEntry"
  echo "Version=$pkgver" >> "$desktopEntry"
  echo "Name=LR2oraja" >> "$desktopEntry"
  echo "Categories=Game;" >> "$desktopEntry"
  echo "Icon=lr2oraja-icon" >> "$desktopEntry"
  
  if [ -z "$XDG_CONFIG_HOME" ]; then
    XDG_CONFIG_HOME="$HOME/.config"
  fi

  # Create config symlink
  ln -sfn "$pkgdir/opt/beatoraja" "$XDG_CONFIG_HOME/beatoraja"

  # Install LR2oraja
  install -D beatoraja.sh "$pkgdir/usr/bin/beatoraja"
}
