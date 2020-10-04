# Maintainer: tmikey

_pkgname=mos-chinadns
pkgname=$_pkgname
pkgver=1.5.2
pkgrel=2
pkgdesc="Provides a local DNS server that prevents GFW DNS poisoning"
arch=('x86_64' 'aarch64')
url="https://github.com/IrineSistiana/mos-chinadns"
license=('GPL3')
depends=('python-netaddr' 'python-requests')
makedepends=('git' 'go')
provides=("$_pkgname")
conflicts=("$_pkgname")
install=$_pkgname.install
pkgbasename=$_pkgname-$pkgver
source=("$pkgbasename.tar.gz::$url/archive/v$pkgver.tar.gz"
  "$_pkgname.install"
  "$_pkgname.service"
  "$_pkgname.yaml"
  )
sha256sums=('145ff178ecf80cde091f0b99f50cd479132c90f688a01ee744644f2f7bfd5c1f'
            '276f1ed8f96efca5103f3b2e51f5ab50dc7ad921ee2990134c5aa1ff47452804'
            '528d7e95297d0f7e4e03016dbaed382ff4ca6241c63c82ed1ec2d7d5d87eb2cc'
            '3b12eb4b41136391bda12edbb77bf89a89335875aff654677f3f70fe020cd548')

prepare() {
  cd "$pkgbasename"
  python3 scripts/update_chn_ip_domain.py
}

build() {
  cd "$pkgbasename"
  go build -ldflags "-s -w -X main.version=$pkgver" -trimpath -o $_pkgname
}

package() {
  cd "$pkgbasename"
  mkdir -p "$pkgdir/usr/bin"
  mkdir -p "$pkgdir/usr/lib"
  mkdir -p "$pkgdir/usr/share/licenses"
  mkdir -p "$pkgdir/usr/lib/systemd/system"
  install -Dm755 -t "$pkgdir/usr/bin" $_pkgname
  install -Dm644 -t "$pkgdir/usr/lib/$_pkgname" README.md "$srcdir/$_pkgname.yaml" chn.list chn_domain.list
  install -Dm755 -t "$pkgdir/usr/lib/$_pkgname" scripts/update_chn_ip_domain.py
  install -Dm644 -t "$pkgdir/usr/share/licenses/$_pkgname" LICENSE
  install -Dm644 -t "$pkgdir/usr/lib/systemd/system" "$srcdir/mos-chinadns.service"
}

# vim:set ts=2 sw=2 et:
