pkgname=rfidiot-git
_gitname=RFIDIOt
groups=(blackarch blackarch-wireless)
pkgver=0c4c448
pkgrel=2
pkgdesc="An open source python library for exploring RFID devices."
url="http://rfidiot.org"
license=('GPL')
makedepends=('git' 'python2-distribute' 'python2-crypto')
depends=('python2' 'openssl')
arch=('any')
source=('git+https://github.com/AdamLaurie/RFIDIOt')
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/$_gitname"
  git describe --always | sed 's|-|.|'
}

prepare() {
  cd "$srcdir/$_gitname"
  # Fix Python shebang lines.
  find . -type f -name '*.py' -exec sed -i '1s/python\r\?$/python2/' '{}' \;
}

package() {
  cd "$srcdir/$_gitname"
  python2 setup.py install --root="$pkgdir/" --optimize=1

  cd "$pkgdir/usr/bin"

  # Remove test scripts.
  rm -f *.sh

  # Strip extensions and add the 'rfidiot-' prefix.
  for file in *.py ; do
    # Remove extension. Add prefix.
    new_file=rfidiot-$(basename "${file%.*}")
    # '_' -> '-'
    new_file=${new_file/_/-}

    install -Dm755 "$file" "$new_file"
    rm -f "$file"
  done
}
